# Chantier — Refonte des prompts Gemini en ton froid factuel

**Statut :** Backlog
**Estimation :** 4-6h
**Priorité :** BLOQUANT avant prospection commerciale, non bloquant pour fin Chantier 0
**Prérequis :** Chantier 0 clôturé (test ALPHA/BETA OK)
**Date de création :** 4 mai 2026 (Session 12)

## Risque adressé

Greenwashing actif. Les 6 prompts Gemini actuels produisent un contenu valorisant et de mise en scène explicitement interdit par le PV Réalignement Produit Gérard du 3 mai 2026.

## Constat factuel — Session 12

Lecture du prompt Gemini 15 actuel révèle des consignes officiellement valorisantes :

- Au lieu de "faible turnover" : "stabilité des équipes maîtrisée"
- Au lieu de "n'a pas d'objectif chiffré" : "objectifs en cours de chiffrage"
- Au lieu de "manque de formation" : "axe de développement à renforcer"
- Au lieu de "absence de politique" : "axe de structuration à venir"

Le JSON produit par Gemini 15 lors du premier test confirme l'effet : "démontrant son engagement", "orientation progressive vers une gestion plus durable", "offrant un cadre clair", "soulignant une orientation".

C'est exactement le piège de la séduction explicitement interdit. Citation PV Gérard : "Un document qui enrobe ou flatte détruit la confiance d'un auditeur (donneur d'ordres ou banquier)."

## Plan de refonte

### 1. Refonte du system prompt commun

- Suppression des consignes valorisantes
- Instauration d'un ton déclaratif strict (donnée + unité + contexte sectoriel factuel)
- Exemple cible : "Le turnover est de 15%, contre une référence sectorielle déclarative INSEE de 12%" (pas "stabilité maîtrisée")
- Le LLM ne qualifie jamais une donnée comme bonne, mauvaise, faible, élevée, structurée, en progrès. Il rapporte les chiffres.

### 2. Banque de termes à interdire (élargie)

Termes actuels déjà bannis : conforme, certifié, audité, garantit, expert RSE, faible, insuffisant, défaillant, manquant, problème, défaut.

À ajouter en interdiction :
- "démontrant", "soulignant", "reflétant", "illustrant"
- "engagement", "orientation progressive", "démarche structurée"
- "stabilité maîtrisée", "axe de développement", "axe de structuration"
- "valorise", "met en scène"
- Adjectifs qualificatifs de l'effort : "actif", "dynamique", "engagé", "rigoureux"

### 3. Banque de formulations préférées

- Phrases déclaratives simples : sujet + verbe d'état + donnée + unité
- Si comparaison : "X versus référence sectorielle Y (source : INSEE / DARES / CNAM / ADEME)"
- Si donnée absente : "Donnée non communiquée" (point, sans euphémisme)
- Si politique absente : "Politique non formalisée à ce jour" (factuel, pas "axe à venir")

### 4. Spécialisation par section

Chaque prompt sectionnel (B3 énergie, B8-B10 social, B11 éthique) doit avoir des consignes métier spécifiques en plus du system prompt commun. Idée déjà notée en V2 dans la mémoire projet ADVA.

### 5. Test de validation

- Génération sur les 2 datasets ALPHA (dossier parfait) et BETA (décès + condamnation)
- Audit ligne par ligne : aucune phrase ne doit pouvoir gêner un dirigeant lisant son rapport à voix haute à son acheteur Safran
- Validation croisée par Le Chasseur (Copilot) — audit impitoyable du contenu produit

## Critère de validation

Un rapport généré doit pouvoir être lu à voix haute par un dirigeant à son banquier sans aucune phrase qui paraisse "arrangée" ou "marketing". Le test du dirigeant : si une phrase nécessite que le dirigeant se justifie, elle est greenwashing.

## Livrables

- 1 system prompt commun refondu (`PROMPTS/system_prompt_common_v2.md`)
- 6 prompts sectionnels spécialisés (`PROMPTS/section_B*_v2.md`)
- 1 grille d'audit anti-greenwashing (`PROMPTS/grille_audit_greenwashing.md`)
- Application des 6 prompts dans Make
- Test ALPHA + BETA validé

## Pourquoi non bloquant pour Chantier 0

Le Chantier 0 vise la robustesse technique du pipeline (étanchéité données, contrôles cohérence, passage de bout en bout). Le ton du contenu Gemini est orthogonal. Un rapport peut sortir techniquement parfait avec un contenu greenwashing — le pipeline est valide, le contenu ne l'est pas.

Cette séparation permet de valider Gérard sur la métrique technique 31 mai (pipeline encaisse 2 tests à blanc) sans attendre la refonte qualitative.

## Pourquoi bloquant avant prospection

La métrique Gérard 15 juin (validation transactionnelle par un acheteur industriel) ne peut pas se faire avec les prompts actuels. Un acheteur Safran qui lit "démontrant son engagement" perd confiance immédiatement. Donc refonte → test ALPHA/BETA sur le contenu → validation Gérard → prospection.
