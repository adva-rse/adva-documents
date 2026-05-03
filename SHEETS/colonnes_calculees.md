# Inventaire des colonnes calculées Google Sheets `Calculs`

Document de référence pour toutes les ARRAYFORMULA en en-tête. Toute modification d'une formule doit être reportée ici.

## Principe architectural

**Make écrit uniquement les colonnes A à V (RESPONSE_ID + 21 colonnes brutes Tally).** Tout le reste est calculé par ARRAYFORMULA en ligne 1, qui propage automatiquement à toute nouvelle ligne ajoutée par Make.

Les facteurs ADEME (prix/litre, kWh/litre, facteurs d'émission) sont stockés dans la feuille `Make_Import` et lus via `INDEX(Make_Import!$2:$2; MATCH("FACTEUR"; Make_Import!$1:$1; 0))`. Mise à jour annuelle = modification d'une cellule Make_Import, propagation automatique.

## Colonnes A à V — Données brutes Tally (écrites par Make Add Row 49)

| Col | Nom | Source Tally | Type |
|-----|-----|--------------|------|
| A | RESPONSE_ID | submissionId Tally | Texte (clé unique) |
| B | ELEC_KWH | Q1 Énergie | Nombre |
| C | GAZ_KWH | Q4 Énergie | Nombre |
| D | FIOUL_EUR | Q5 Énergie | Nombre |
| E | DIESEL_EUR | Q6 Énergie | Nombre |
| F | ESSENCE_EUR | Q7 Énergie | Nombre |
| G | GPL_EUR | Q8 Énergie | Nombre |
| H | BOIS_EUR | Q9 Énergie | Nombre |
| I | EFFECTIF | Effectif exact ETP | Nombre |
| J | CA_EUROS | Chiffre d'affaires | Nombre |
| K | EAU_M3 | Q1 Eau | Nombre |
| L | SURFACE_M2 | Q3 Biodiversité | Nombre |
| M | NB_AT | Q1 Santé Sécurité | Nombre |
| N | DEPARTS | Effectif (turnover) | Nombre |
| O | DECHETS_ND_T | Q2 Économie circulaire | Nombre |
| P | DECHETS_D_T | Q3 Économie circulaire | Nombre |
| Q | DECHETS_RECYCLE_T | Q4 Économie circulaire | Nombre |
| R | HOMMES | Effectif par genre | Nombre |
| S | FEMMES | Effectif par genre | Nombre |
| T | FORMATION_H | Heures formation | Nombre |
| U | CDI | Effectifs par contrat | Nombre |
| V | CDD | Effectifs par contrat | Nombre |

## Colonnes W à AY — Calculs énergie / GES / sociaux

Toutes en ARRAYFORMULA (en-tête blindé). Validées sur RWDvrpl en session 11.

### Énergie en MWh

| Col | Nom | Formule (résumée) |
|-----|-----|-------------------|
| W | ELEC_MWH | `B/1000` |
| X | GAZ_MWH | `C/1000` |
| Y | FIOUL_LITRES | `D/PRIX_FIOUL_L` |
| Z | DIESEL_LITRES | `E/PRIX_DIESEL_L` |
| AA | ESSENCE_LITRES | `F/PRIX_ESSENCE_L` |
| AB | GPL_LITRES | `G/PRIX_GPL_L` |
| AC | ENERGIE_TOTALE_MWH | `W+X+somme combustibles MWh` |

### CO2 et Scopes

| Col | Nom | Formule (résumée) |
|-----|-----|-------------------|
| AD | CO2_GAZ | `C * FE_GAZ_KWH / 1000` |
| AE | CO2_FIOUL | `Y * FE_FIOUL_L / 1000` |
| AF | CO2_DIESEL | `Z * FE_DIESEL_L / 1000` |
| AG | CO2_ESSENCE | `AA * FE_ESSENCE_L / 1000` |
| AH | CO2_GPL | `AB * FE_GPL_L / 1000` |
| AI | SCOPE1_TCO2 | `AD+AE+AF+AG+AH` |
| AJ | SCOPE2_TCO2 | `B * FE_ELEC_KWH / 1000` |
| AK | SCOPE12_TCO2 | `AI+AJ` |
| AL | INTENSITE_CARBONE | `AK / (J/1000000)` |

### Déchets et ratios sociaux

| Col | Nom | Formule (résumée) |
|-----|-----|-------------------|
| AM | DECHETS_TOTAL_T | `O+P` |
| AN | TAUX_RECYCLAGE | `Q/AM*100` |
| AO | TAUX_TURNOVER | `N/I*100` |
| AP | TAUX_FEMMES | `S/(R+S)*100` |
| AQ | TAUX_FREQ_AT | `M*BASE_TAUX_FREQ/(I*HEURES_TRAVAIL_AN)` |
| AR | EAU_PAR_ETP | `K/I` |
| AS | SURFACE_HA | `L/10000` |

### Conversions combustibles MWh (pour template B3)

| Col | Nom | Formule (résumée) |
|-----|-----|-------------------|
| AT | FIOUL_MWH | `Y * CONV_FIOUL_KWH_L / 1000` |
| AU | DIESEL_MWH | `Z * CONV_DIESEL_KWH_L / 1000` |
| AV | ESSENCE_MWH | `AA * CONV_ESSENCE_KWH_L / 1000` |
| AW | GPL_MWH | `AB * CONV_GPL_KWH_L / 1000` |
| AX | BOIS_MWH | `(H/PRIX_BOIS_KWH)/1000` |
| AY | COMB_TOTAL_MWH | `AT+AU+AV+AW+AX` |

## Colonnes AZ à BJ — Contrôles de cohérence

Le Router Make doit pointer sur BI (CTRL_GLOBAL).

| Col | Nom | Sortie |
|-----|-----|--------|
| AZ | CTRL_EFFECTIF | "OK" ou "ERREUR" si CDI+CDD > 110% effectif |
| BA | CTRL_GENRE | "OK" ou "ERREUR" si écart Hommes+Femmes vs effectif > 10% |
| BB | CTRL_DECHETS | "OK" ou "ERREUR" si recyclés > total |
| BC | CTRL_AT_MASSIF | "OK" ou message si taux fréquence AT hors bornes |
| BD | CTRL_INTENSITE | "OK" ou message si intensité carbone hors plausibilité |
| BE | CTRL_TURNOVER | "OK" ou message si turnover hors bornes |
| BF | CTRL_EAU | "OK" ou message si conso eau/ETP hors bornes |
| BG | CTRL_FORMATION | "OK" ou message si heures formation hors bornes |
| BH | CTRL_DECES | "OK" forcé temporairement (en attente NB_DECES) |
| BI | **CTRL_GLOBAL** | **"OK" si AZ+BA+BB tous OK, "ERREUR" sinon** — lu par Router Make |
| BJ | CTRL_DETAIL | Concaténation des messages d'erreur pour le mail client |

## Règles d'or applicables (n°1 à n°12)

1. Le LLM ne calcule rien — tous les chiffres viennent de Sheets
2. Les agrégations restent dans Sheets, jamais dans Gemini
3. Les unités sont dans le template Word, pas dans le LLM
4. JSON strict en sortie Gemini, jamais de backticks
5. Variables techniques par ID Tally (question_xxx), jamais par label
6. ifempty() sur les variables sensibles (décès, condamnations)
7. Sleep entre Make et Sheets pour éviter les race conditions
8. Toutes formules Sheets en ARRAYFORMULA dans en-tête (méthode Gérard)
9. Conversions ADEME par ARRAYFORMULA Sheets via INDEX/MATCH sur Make_Import, jamais dans Make
10. Locale française : virgule décimale obligatoire dans toutes les formules
11. IFERROR systématique sur opérations numériques pour éviter contamination silencieuse
12. N() n'est pas vectorisée — utiliser `IFERROR(plage*1; 0)` à la place
