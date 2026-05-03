# PV d'Initialisation et de Gestion de Crise — Board ADVA

**Date :** 3 mai 2026
**De :** Gérard (Actionnaire Stratégique)
**À :** Josselin (Chef d'Orchestre) & Michel (CTO)

## 1. Décisions stratégiques actées

- **Gel des chantiers cosmétiques :** toute refonte de template (Chantier 2) ou de page de synthèse (Chantier 8) est suspendue. La robustesse du système prime sur l'esthétisme.
- **Validation du Chantier 0 en urgence absolue :** la faille de contamination des données inter-clients est identifiée comme un risque de mort subite (litige légal garanti). Le correctif technique est la seule priorité.
- **Métriques de réussite définies :**
  - 31 mai (technique) : le pipeline encaisse 2 tests à blanc de bout en bout sans intervention manuelle.
  - 15 juin (marché) : validation transactionnelle du rapport par un pair (acheteur industriel en poste).

## 2. Architecture & processus (organisation de l'équipe)

Architecture organisationnelle en étoile pour maximiser le levier technologique et éviter la dilution de l'information. Josselin centralise et orchestre le Board composé de trois entités hermétiques :

- **Michel (Claude)** — l'Opérateur : exécution technique, code, paramétrage Make/Notion/Sheets.
- **Gérard (Gemini)** — le Risk Manager : validation architecturale, traque de la dette technique, évitement des risques de ruine.
- **Le Chasseur (Copilot)** — le Stratège Commercial : nouveau membre acté. Orienté acquisition, nourri avec un contexte expurgé (uniquement cible, pricing, règles juridiques strictes) pour garantir un copywriting anti-bullshit et sourcé.

## 3. Risques identifiés et évités

- **Risque d'écrasement des données (Make vers Sheets) :** correction architecturale apportée par le Board — déploiement de l'En-tête Blindé `={"TITRE"; ARRAYFORMULA(...)}` pour empêcher le module "Add a Row" de Make d'écraser les formules de calcul.
- **Risque légal (vocabulaire) :** confirmation de l'élagage strict. ADVA est un outil de structuration déclarative. Maintien de l'interdiction absolue des termes "certifié", "conforme", "audit".
- **Risque de bruit informationnel :** validation du compartimentage. L'IA commerciale (Le Chasseur) n'aura jamais accès à l'ingénierie interne pour éviter les hallucinations.

## 4. Prochaine étape opérationnelle (jalon binaire)

Exécution et validation définitive du Chantier 0.

**Action attendue :** lancement successif des soumissions TEST ALPHA (dossier parfait) et TEST BETA (décès + condamnation) à travers le pipeline Make mis à jour (Add Row + En-têtes blindés).

**Critère de succès :** génération de deux rapports hermétiques, prouvant l'étanchéité absolue de la base de données.
