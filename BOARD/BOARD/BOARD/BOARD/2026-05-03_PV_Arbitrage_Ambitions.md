# PV d'Arbitrage Stratégique — Validation des Ambitions et Disciplines Architecturales

**Date :** 3 mai 2026
**De :** Gérard (Actionnaire Stratégique)
**À :** Michel (CTO) & Josselin (Fondateur)
**Objet :** Réponse à la lettre Michel du 3 mai 2026

## Préambule

Ce courrier de Michel est la preuve que le Board en étoile fonctionne. Il anticipe la charge que l'architecture devra supporter dans 2 ans. Analyse chirurgicale de la différence entre un cash-flow business (Ambition B) et un actif productif SaaS (Ambition C).

## Point 1 — Arbitrage des ambitions (B vs C)

**Validation formelle :** Ambition B = MVP exclusif. Ambition C = vision long terme.

C'est le principe même du Skin in the Game : on ne construit pas une cathédrale (SaaS à abonnement) tant qu'on n'a pas prouvé que les gens étaient prêts à payer pour la première brique (le rapport VSME one-shot). L'Ambition B finance et valide l'Ambition C.

**Consigne stricte pour Josselin :** interdiction absolue de commencer à maquetter Ambition C (interfaces web, dashboards) avant d'avoir encaissé les 10 premières factures de l'Ambition B. Le focus reste l'exécution des Chantiers 0 à 7.

## Point 2 — Disciplines architecturales (le vrai pivot)

**Discipline 2 (Sheets = BDD, Word = Vue) :** validée à 100%. Base de toute ingénierie de la donnée saine.

**Discipline 1 (Response ID = identifiant permanent) :** validée avec mise en garde critique sur la charge Google Sheets.

**Arbitrage technique critique :** vous ne purgez pas les données client. Le `Response ID` devient l'ancre du client. Cependant, à partir du 50ème client, vous devrez impérativement créer une automatisation qui copie la "ligne résultat" (figée) vers une **Base de Données Froide** (autre fichier Sheets ou Airtable) et qui efface la ligne du fichier `Calculs`. Le fichier `Calculs` (avec les ARRAYFORMULA) ne doit servir que de processeur chaud, pas d'archive morte, sinon il plantera.

→ Création du **Chantier BDD-Froide** en backlog, déclenchement à 40 clients facturés (anticipation 10 clients avant le seuil critique).

## Point 3 — Étude de marché des 10 premiers clients

**Validation totale.** Un client qui paie 990€ est un client qui a mal. S'il a mal, il est prêt à dire pourquoi et comment il compte utiliser le pansement.

**Action requise :** Le Chasseur sera impliqué. Une fois les 10 premiers rapports livrés, c'est au Chasseur de rédiger l'interview post-livraison pour extraire l'information stratégique (qui est le pilote ? Comment est géré le cycle EcoVadis en interne ?).

## Sur le Risque 3 — La démission prématurée

Michel a touché un point sensible. En tant qu'actionnaire du temps de Josselin :

**L'emploi salarié actuel est ton laboratoire de R&D gratuit.** L'entreprise qui te paie est ta cible exacte. Quitter ce poste aujourd'hui, c'est comme un chercheur qui brûlerait son microscope juste avant de lancer son expérience.

**Tu ne quittes pas ce poste tant que :**
1. L'Ambition B ne génère pas un flux de trésorerie régulier
2. ET l'Ambition C n'est pas techniquement amorcée

**Ton salaire finance ton risque.**

## Conclusion

Alignement parfait. Michel a validation pour documenter ces décisions dans Notion (avec la nuance Base de Données Froide pour la Discipline 1).

Josselin a son cap pour les 12 prochains mois. **Retour au Chantier 0.**
