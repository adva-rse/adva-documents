# Chantier 0 — Étanchéité absolue des données client

## Objectif

Garantir que le système est techniquement incapable de mélanger les données 
de deux soumissions client. Directive Gérard, priorité absolue.

## Architecture cible

| Élément | Avant | Après |
|---|---|---|
| Sheets 11 | Update Row sur ligne 2 fixe | Add Row, nouvelle ligne par soumission |
| Colonne A | ELEC_KWH | RESPONSE_ID (clé unique Tally) |
| Sheets 48 | Recherche dernière ligne | Filtre strict RESPONSE_ID = {{1.responseId}} |
| Sleep | 1s | 3s (latence formules de calcul) |
| Formules calcul | Ligne 2 fixe | ARRAYFORMULA sur toute la colonne |

## Règle d'or n°8 ajoutée

**Toutes les formules calculées Google Sheets DOIVENT être en ARRAYFORMULA.**

Sinon, quand Make Add Row crée une nouvelle ligne, aucun calcul ne se déclenche
sur cette ligne. Les rapports sortent avec 0 partout.

Format type :
=ARRAYFORMULA(IF(B2:B="";"";<formule avec références en plage X2:X>))

## 11 formules converties en ArrayFormula

- AD (CO2_GAZ), AE (CO2_FIOUL), AF (CO2_DIESEL), AG (CO2_ESSENCE), AH (CO2_GPL)
- AI (SCOPE1_TCO2)
- AJ (SCOPE2_TCO2)
- AK (SCOPE12_TCO2)
- AL (INTENSITE_CARBONE)
- AM (DECHETS_TOTAL_T) — bug bonus corrigé : formule était un copier-coller faussé
- AN (TAUX_RECYCLAGE)
- AO (TAUX_TURNOVER) — piège ROUND/IF résolu
- AP (TAUX_FEMMES)
- AQ (TAUX_FREQ_AT)
- AR (EAU_PAR_ETP)
- AS (SURFACE_HA)
- BP (COMB_TOTAL_MWH)

## Bug bonus découvert

Formule AM (DECHETS_TOTAL_T) était `=ROUND(IF(J2>0; AK2/(J2/1000000); 0); 1)` 
— c'est-à-dire un copier-coller de l'intensité carbone (AL). Présent dans la 
feuille depuis le départ. Tous les rapports précédents ont calculé 
DECHETS_TOTAL_T comme l'intensité carbone. Corrigé en `=O2:O+P2:P`.

## Statut

Architecture en place. Test de validation 2 soumissions distinctes en attente.

## Bug séparé identifié

Module HTTP du Scénario 1 (envoi prep sheet PDF après saisie SIREN) ne fonctionne plus.
À traiter session séparée. Sans impact sur Chantier 0.
