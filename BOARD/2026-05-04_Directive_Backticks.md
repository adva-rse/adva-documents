# Directive Technique — Résolution backticks Gemini & Plan d'exécution Session 13

**Date :** 4 mai 2026
**Émetteur :** Gérard (Actionnaire Stratégique)
**Destinataires :** Michel (CTO), Josselin (Fondateur)
**Statut :** Validé après contradiction technique du CTO

## Contexte

Suite à la Session 12, le pipeline Make franchit le Router pour la première fois mais plante immédiatement au Parse JSON 38. Cause : Gemini 15 entoure son JSON de backticks markdown malgré l'instruction du system prompt.

Première directive Gérard reçue avec une syntaxe regex JavaScript-style et un post-mortem reposant sur une lecture erronée du correctif Session 12 (formatage du journal ayant avalé les backticks à l'affichage).

## Contradiction technique du CTO

Michel a soulevé 4 points :

1. La citation du correctif Session 12 dans la directive initiale était inexacte — les backticks étaient bien présents dans la proposition originale, mais avaient été masqués par le formatage du journal.
2. La syntaxe regex `/pattern/flags` proposée n'est pas supportée par le moteur regex natif de Make. Syntaxe correcte Make : `(?i)```(json)?`.
3. L'incohérence apparente entre "verrouillage des 6 prompts" et "applique uniquement sur le premier bloc" devait être tranchée.
4. Question d'opportunité : profiter de l'ouverture des 6 prompts pour la refonte ton froid factuel acté le 3 mai.

## Arbitrages Gérard

### Sur le post-mortem et la syntaxe regex (points 1 & 2)

Reconnaissance de l'erreur de diagnostic initiale (formatage journal). Validation formelle de la syntaxe `(?i)```(json)?`. Fallback autorisé en double `replace` uniquement si la regex échoue lors du test sur Gemini 15.

### Sur la séquence d'application (point 3)

L'Étape A (consigne anti-markdown dans le prompt) est sans risque technique → déploiement sur les 6 d'un coup. L'Étape B (filet regex Tools) modifie le traitement de la donnée → isolation sur le premier bloc Gemini 15 d'abord, validation, puis généralisation.

### Sur la tentation de la refonte produit (point 4) — VETO ABSOLU

Si modification simultanée tuyauterie (backticks) + produit (ton), un plantage devient indiagnostiquable. Discipline > opportunisme.

Le Chantier Refonte-Prompts-Gemini reste strictement cantonné au backlog tant que le Chantier 0 n'est pas refermé par un test ALPHA/BETA vert de bout en bout.

### Sur le plan d'exécution

Plan en 5 étapes proposé par Michel validé tel quel.

## Plan d'exécution Session 13 (validé Board)

**Étape 1 — Verrouillage des 6 prompts Gemini (10 min)**

Ajouter en fin de chaque system prompt (Gemini 15, 16, 18, 19, 20, 21) :

> CRITIQUE : Ne génère AUCUN formatage Markdown. Ne commence pas ta réponse par triple-backtick-json et ne la termine pas par triple-backtick. Ta réponse doit commencer directement par { et finir directement par }.

**Étape 2 — Filet regex sur Tools 37 uniquement (10 min)**

Valeur de la variable `Gemini15_clean` : {{replace(15.result; "(?i)```(json)?"; "")}}

**Étape 3 — Généralisation sur les 5 autres Tools (15 min)**

Uniquement si Étape 2 valide. Modifier Tools 39, 36, 41, 43, 46 avec la même syntaxe (en adaptant le numéro de bulle Gemini).

**Étape 4 — Coller les 4 contrôles CTRL_* corrigés (5 min)**

CTRL_AT_MASSIF, CTRL_INTENSITE, CTRL_TURNOVER, CTRL_EAU avec `*1` forcé. Formules dans `JOURNAL/session_12_2026-05-04.md`.

**Étape 5 — Test ALPHA + BETA complet (5 min si tout passe)**

Si rapport sort jusqu'à Gmail → Chantier 0 clôturé. Validation Gérard métrique 31 mai.

## Leçons consignées

**Discipline du Board.** La contradiction factuelle d'un CTO sur une directive techniquement imprécise n'est pas une insubordination — c'est exactement la fonction protective d'un CTO. La directive initiale Gérard contenait une syntaxe regex inadaptée à Make ; sans la contradiction de Michel, l'exécution aveugle aurait fait perdre une session entière.

**Format de documentation.** Les backticks markdown doivent être documentés autrement dans les journaux pour éviter le malentendu Session 12 → directive Gérard. Trois options : échappement explicite, bloc de code dédié, description en toutes lettres ("triple accent grave"). À standardiser dans les prochaines sessions.

**Séparation tuyauterie / produit.** Le veto absolu de Gérard sur la refonte ton est doctrinalement important. Modifier deux choses simultanément (backticks + ton) rend tout plantage indiagnostiquable. Toujours isoler les modifications.
