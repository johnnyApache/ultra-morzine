# Ultra Morzine — app de suivi d'entraînement

## Contexte
Application mobile de suivi d'entraînement pour préparer le **Spartan Ultra World Championship de Morzine-Avoriaz, le vendredi 2 juillet 2027** (50 km, 60 obstacles, sommet à la pointe de Nyon).
L'app est destinée à son créateur et à un petit groupe d'amis qui préparent la même course. Chacun a son plan personnel et peut suivre la progression des autres.

Le créateur n'est pas développeur : explique chaque étape simplement, propose avant d'installer ou de supprimer quoi que ce soit, et privilégie les solutions gratuites et simples à maintenir.

## État actuel (version A)
- `ultra-morzine.html` : application d'un seul fichier (JS vanilla), actuellement publiée dans claude.ai.
- Stockage : localStorage + base partagée de la plateforme claude.ai. Les amis doivent avoir un compte Claude.
- Tout l'accès au stockage passe par l'objet `Store` (`init`, `loadMine`, `saveMine`, `publish`, `subscribe`). **C'est le seul endroit à remplacer pour migrer.**

## Objectif (version B)
Une vraie **PWA** :
1. Installable sur l'écran d'accueil du téléphone, avec un service worker et un fonctionnement hors ligne (sorties longues en montagne sans réseau).
2. Hébergée gratuitement (Netlify, Vercel ou GitHub Pages).
3. Base de données en ligne gratuite (Supabase ou Firebase) pour la vue de groupe.
4. Accès des amis **sans compte Claude** : un lien et une connexion simple (email avec lien magique, ou pseudo + code). À décider avec le créateur.
5. Synchronisation entre appareils, et sauvegarde/export des données conservés.

## Fonctionnalités à conserver
- Profil : pseudo, plus longue course sans arrêt, km par semaine, jours disponibles, limite éventuelle.
- Plan de 39 semaines du lundi 5 octobre 2026 au 2 juillet 2027, 5 phases : Base (S1-10), Volume (S11-21), Spécifique (S22-30), Pic (S31-36), Affûtage (S37-39, S39 = semaine de course). Générateur : fonction `buildPlan` (croissance géométrique du volume, semaine allégée toutes les 4 semaines, plafonds de sortie longue par phase).
- Journal par séance : fait, durée, km, D+, effort (1-10), fatigue (1-10), douleur, note.
- Alerte : proposer −20 % de volume si la semaine précédente montre fatigue moyenne ≥ 8, douleur signalée, ou moins de 50 % des séances faites.
- Bouton « retour de la semaine » : texte à copier-coller dans une conversation avec Claude pour ajuster la suite.
- Graphique « profil de montagne » : volume prévu contre réalisé.
- Vue de groupe : plan et progression des amis, navigation par semaine.

## Confidentialité (règle forte)
- **Partagé avec le groupe** : pseudo, paramètres du plan, séances faites, durées, km, D+.
- **Jamais partagé** : douleurs, fatigue, notes, limites. Chacun peut désactiver son partage.
- Chaque personne ne peut modifier que ses propres données (règles de sécurité côté base, pas seulement côté interface).
- Pas de secrets ni de clés privées dans le code côté navigateur.

## Avertissement santé
L'app donne un cadre général d'entraînement, pas un avis médical. Garder le message qui invite à consulter un médecin en cas de pathologie ou de douleur persistante.

## Première tâche proposée
1. Ouvrir `ultra-morzine.html` en local, vérifier qu'il s'affiche et lire le code.
2. Proposer un plan de migration en étapes courtes (structure du projet, choix de la base, authentification, PWA, déploiement) et me le soumettre avant de coder.
3. Commencer par une version locale qui fonctionne hors ligne, puis ajouter la base de données et le groupe.

## Style
- Interface en français, pensée pour le téléphone (cibles tactiles de 44 px minimum), mode clair et sombre.
- Code simple et commenté, sans dépendances inutiles.
