# Session Chantier 1 — 30 avril 2026

## Diagnostic du bug "scénario en boucle"

L'erreur du 27 avril 02:02 n'était pas une boucle infinie — c'était un échec en queue d'erreur après un `BundleValidationError: Missing value of required parameter 'json'` sur Parse JSON 47 (Gemini 33).

**Cause racine :** Tools 46 (variable `Gemini33_clean`) sortait vide parce que le mapping pointait sur `33.Candidates[]` (array d'objets) au lieu de `33.result` (string JSON).

**Correction :** remplacement du contenu de Variable value de Tools 46 par `{{33.result}}` directement, sans `replace()` ni accès à `Candidates[]`.

## Data Structures créées

| Module | Data Structure | Couverture |
|--------|---------------|------------|
| JSON 42 | `Gemini19_B11_C1_C3_C4` | B11 + C1 + C3 + C4 |
| JSON 44 | `Gemini20_Scoring_Reco` | Scores + positionnement + recommandations |
| JSON 47 | `Gemini33_C2_C6_C7_C8` | C2 + C6 + C7 + C8 |

## État Chantier 1

Tools + Parse JSON installés sur les 6 Gemini. Toutes les Data Structures assignées. Reste :

- Validation bout en bout quand Gemini sera dispo (503 en cours côté Google)
- Triangle orange persistant Gemini 18 (probablement 503, à confirmer)
- Modifier les références croisées dans les prompts (Gemini 33 et Gemini 20)

## Risque opérationnel à traiter

Les 503 Gemini en plein traitement client sont un risque réel de production. **Action ajoutée au Chantier 5** : activer le retry automatique (3 tentatives, intervalle 60s) sur chaque module Gemini.
