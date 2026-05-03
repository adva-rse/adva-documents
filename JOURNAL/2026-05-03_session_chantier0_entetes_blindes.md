# Session 3 mai 2026 — Chantier 0, méthode en-têtes blindés

## Méthode Gérard appliquée

Formules ArrayFormula déplacées dans les en-têtes (ligne 1).
Make n'écrase jamais la ligne 1 — formules indestructibles.
17 en-têtes transformés : AD à AS + BP.

## Bug restant

Colonnes W (GAZ_MWH), X (FIOUL_LITRES), Y (DIESEL_LITRES),
Z (ESSENCE_LITRES), AA (GPL_LITRES), AC (ENERGIE_TOTALE_MWH)
vides dans Add Row 49.

Ces valeurs sont calculées dans Make (Tools 32 ?), pas dans Tally.
À mapper dans Add Row 49 depuis les bonnes bulles Make.

## À faire session suivante

1. Identifier module source de W à AC dans Make
2. Ajouter mappings dans Add Row 49
3. Test soumission + validation formules
4. Test étanchéité 2 soumissions distinctes
5. Si OK → Chantier 0 clos → Chantier 5
