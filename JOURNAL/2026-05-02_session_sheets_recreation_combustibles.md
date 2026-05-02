# Session 2 mai 2026 — Recréation Sheets 14 + combustibles fonctionnels

## Milestone

Pipeline B3 (combustibles) fonctionnel de bout en bout pour la première fois.
Tally → Google Sheets → Gemini 16 → Google Docs affiche enfin les valeurs.

## Règle d'architecture gravée dans le marbre

**Tous les Tools pointent sur `XX.result`. Tous les Parse JSON pointent sur la variable `GeminiXX_clean` du Tools correspondant. Ne plus jamais changer.**

| Parse JSON | JSON string | Tools | Variable value |
|---|---|---|---|
| JSON 38 | `37. Gemini15_clean` | Tools 37 | `15. Result` |
| JSON 40 | `39. Gemini16_clean` | Tools 39 | `16. Result` |
| JSON 35 | `36. Gemini18_clean` | Tools 36 | `18. Result` |
| JSON 42 | `41. Gemini19_clean` | Tools 41 | `19. Result` |
| JSON 44 | `43. Gemini20_clean` | Tools 43 | `20. Result` |
| JSON 47 | `46. Gemini33_clean` | Tools 46 | `33. Result` |

Plusieurs heures perdues à alterner entre les deux architectures.
La bonne est celle ci-dessus. Le filet `replace()` n'est pas optionnel,
c'est une couche de robustesse contre l'inconstance de Gemini sur le format JSON.

## Bug Sheets 14 → recréation Sheets 48

Sheets 14 lisait Column range A-BZ mais ne retournait que jusqu'à BJ.
Cause : Make avait mis en cache la structure de la feuille à la création du module,
avant l'ajout des colonnes BK-BO.

Solution : suppression de Sheets 14, recréation → Sheets 48.
Bulles `{{14.XXX}}` cassées dans Gemini 16/18/19/20 → remap vers `{{48.XXX}}`.

## Erreur formule Google Sheets

BO2 (COMB_TOTAL_MWH) avait `=W2+V2*0,01+...` (V = ELEC_MWH, mauvais).
Corrigé en `=W2+X2*0,01+Y2*0,01+Z2*0,009+AA2*0,00741`.

## Bugs restants

1. DATE_RAPPORT placeholder s'affiche en clair (retaper manuellement)
2. Unités dupliquées B3/B6/B7 (règle absolue à ajouter dans Gemini 16 et 20)
3. B4 "nos activités" (règle 3e personne à propager Gemini 16)
4. B10 couverture sans % (template à ajuster)
5. Synthèse globale qualifie positivement la sécurité malgré décès
   (règle Gemini 20 à renforcer)
