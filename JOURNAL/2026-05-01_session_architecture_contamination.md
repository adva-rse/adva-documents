# Session 1er mai 2026 (après-midi) — Architecture + contamination inter-clients

## Architecture Make — décision

6 Gemini conservés pour le MVP. Consolidation en 3-4 reportée en V2 (benchmark 20+ rapports réels).
6 modules Tools anti-backticks conservés comme filet de sécurité MVP.

## Bug architectural — contamination inter-clients

Google Sheets 11 (Update Row) écrase la même ligne à chaque soumission.
Si un champ n'est pas rempli par le nouveau client, l'ancienne valeur persiste.
Risque : rapport Frankenstein (données mélangées entre deux clients).

### Solution définitive (Chantier 4)
Passer de Update Row à Add Row + filtrage par `responseId` Tally.
Chaque client = sa propre ligne. Zéro contamination.

### Solution intermédiaire
Module de vidage de la feuille au DÉBUT du scénario (après trigger Tally, avant Tools 32).
Chaque soumission part d'une feuille vierge.

Ne PAS mettre le vidage à la fin — si le scénario plante, le vidage ne s'exécute pas
et le prochain client hérite des données partielles.
