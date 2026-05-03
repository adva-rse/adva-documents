# Changelog Template v2 — 3 mai 2026

Application directe du PV Réalignement Produit Gérard (3 mai 2026 matin) suite à arbitrage Ambitions B/C.

## Suppressions

### Section 19 — "Synthèse et Scoring ADVA"

Bloc complet supprimé du template :

- Titre "Synthèse et Scoring ADVA"
- Phrase "Le scoring ADVA est un indicateur interne, inspiré des données déclaratives collectées selon le cadre VSME"
- Tableau scoring 4 lignes : SCORE_ENV, SCORE_SOCIAL, SCORE_GOUV, SCORE_GLOBAL

Raison : risque juridique de requalification en organisme de notation ESG non habilité. Décision Gérard formelle, non négociable.

### Tableau positionnement sectoriel — Colonne "Écart"

Tableau positionnement passé de 4 à 3 colonnes :

- Suppression colonne "Écart"
- Suppression des balises POS_CARBONE_ECART, POS_AT_ECART, POS_FORM_ECART, POS_RECYCL_ECART, POS_TURN_ECART, POS_EAU_ECART
- Largeur tableau réduite proportionnellement

Raison : un "écart à la médiane" peut être requalifié en notation comparative, même sans le mot "score". Position défensive juridique.

## Renommages

| Ancien | Nouveau |
|--------|---------|
| Titre H1 "19. Synthèse et Scoring ADVA" | "19. Positionnement sectoriel" |
| "Médiane" (entête tableau) | "Référence sectorielle déclarative" |
| Titre H2 "Recommandations prioritaires" | "Axes de structuration identifiés" |
| Titre H2 "Synthèse globale" | "Synthèse factuelle" |

Raison : lexique outil de structuration de données déclaratives, pas outil de conseil ou de notation.

## Ajouts

### Phrase italique sous tableau positionnement

> *Sources des références sectorielles déclaratives : INSEE EACEI (énergie), CNAM (accidentologie), DARES (formation, turnover), ADEME (recyclage). Ces valeurs sont fournies à titre informatif pour permettre au lecteur de situer les données déclarées par l'entreprise dans leur contexte sectoriel. Aucune notation ni évaluation comparative n'est effectuée par ADVA.*

Format : italique, taille 9pt, couleur #595959.

### Phrase italique sous "Axes de structuration identifiés"

> *Les axes ci-dessous résultent d'une lecture structurée des données déclarées selon les recommandations méthodologiques du référentiel VSME. Ils ne constituent ni des préconisations professionnelles ni un audit organisationnel.*

Format : italique, taille 9pt, couleur #595959.

### Tableau "Détail des combustibles" dans section B3

Nouveau tableau inséré juste après le tableau "Consommation énergétique" et avant le tableau "Émissions de gaz à effet de serre" :

| Combustible | Consommation (MWh) |
|-------------|--------------------|
| Fioul domestique | {{B3_fioul_mwh}} |
| Diesel | {{B3_diesel_mwh}} |
| Essence | {{B3_essence_mwh}} |
| GPL / Propane | {{B3_gpl_mwh}} |
| Bois / Biomasse | {{B3_bois_mwh}} |
| **TOTAL combustibles** | **{{B3_comb_total_mwh}}** |

6 nouvelles balises Gemini : B3_fioul_mwh, B3_diesel_mwh, B3_essence_mwh, B3_gpl_mwh, B3_bois_mwh, B3_comb_total_mwh.

Raison : valeur ajoutée client (mix énergétique détaillé pour identifier les leviers de réduction). Demande Gérard explicite.

## Conversion Google Doc

Méthode utilisée : upload Word v2 dans Drive → clic droit → Ouvrir avec Google Docs → vérification manuelle des balises → remplacement du template Make.

Validation finale : test sur ligne RWDvrpl à effectuer après reconstruction Sheets complète (Chantier 0).

## Validation XML

Template v2 packé via `pack.py` du skill docx — validation PASSED. Attribut `gutter="0"` ajouté manuellement sur `pgMar` (oubli python-docx).

## Mise à jour prompts Gemini

Les prompts Gemini doivent être mis à jour pour refléter le nouveau ton :

- Section 19 (anciennement scoring) : prompt à supprimer entièrement
- Section "Synthèse factuelle" (anciennement "Synthèse globale") : prompt à reformuler vers un ton de résumé factuel sans qualification ("L'entreprise présente une consommation énergétique de X MWh, dont Y% renouvelable") plutôt que valorisant ("L'entreprise affiche une démarche énergétique structurée").
- Section "Axes de structuration identifiés" (anciennement "Recommandations prioritaires") : prompt à reformuler vers une lecture méthodologique du VSME ("Le référentiel VSME suggère d'examiner les axes suivants au regard de vos données") plutôt qu'une recommandation directe ("Nous vous recommandons de").

À traiter dans une session dédiée post-clôture Chantier 0.
