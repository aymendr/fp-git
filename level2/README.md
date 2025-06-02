# Atelier Git avec Bitbucket - Scénarios Professionnels Avancés

Voici plusieurs scénarios professionnels avancés pour un atelier Git avec Bitbucket, incluant des exemples pratiques et leurs corrections.

## Scénario 1 : Gestion d'une Feature Complexe avec Branches et Pull Requests

**Situation** : Vous devez développer une nouvelle fonctionnalité de paiement qui comprend:
1. Intégration avec une nouvelle API de paiement
2. Modification du panier
3. Mise à jour du backend

**Exercice** :
1. Créez une branche `feature/payment-integration` depuis `main`
2. Créez des sous-branches pour chaque composant:
   - `feature/payment-api`
   - `feature/cart-update`
   - `feature/backend-update`
3. Fusionnez les sous-branches dans `feature/payment-integration` via des pull requests
4. Résolvez les conflits éventuels

**Correction** :
```bash
# 1. Création de la branche principale de la feature
git checkout main
git pull origin main
git checkout -b feature/payment-integration

# 2. Création des sous-branches
git checkout -b feature/payment-api
# Faire les modifications et commits pour l'API
git add .
git commit -m "Intégration de l'API de paiement"
git push origin feature/payment-api

# Créer une pull request dans Bitbucket pour merger feature/payment-api dans feature/payment-integration

# Répéter pour les autres sous-branches
git checkout feature/payment-integration
git checkout -b feature/cart-update
# Modifications...
```

## Scénario 2 : Gestion des Hotfixes en Production

**Situation** : Une erreur critique a été découverte en production alors que vous travaillez sur une nouvelle feature.

**Exercice** :
1. Stash vos changements en cours
2. Créez une branche hotfix depuis main
3. Corrigez le bug et créez un tag de version
4. Revenez à votre travail initial

**Correction** :
```bash
# 1. Stash des changements en cours
git stash save "travail en cours sur la feature X"

# 2. Création de la branche hotfix
git checkout main
git pull origin main
git checkout -b hotfix/login-issue

# 3. Correction du bug, commit et tag
# Faire les modifications nécessaires
git add .
git commit -m "Correction du bug de login"
git tag -a v1.0.1 -m "Correctif pour le bug de login"
git push origin hotfix/login-issue --tags

# 4. Retour au travail initial
git checkout feature/ma-feature-en-cours
git stash pop
```

## Scénario 3 : Refactoring avec Rebase Interactif

**Situation** : Vous avez fait plusieurs commits pour un refactoring mais ils contiennent des messages peu clairs et des petits bugs.

**Exercice** :
1. Utilisez rebase interactif pour:
   - Combiner certains commits
   - Modifier des messages de commit
   - Supprimer un commit inutile
2. Force push vers la branche distante

**Correction** :
```bash
# Voir les derniers commits
git log --oneline -n 10

# Lancer le rebase interactif
git rebase -i HEAD~5

# Dans l'éditeur qui s'ouvre:
# - Changer 'pick' en 'squash' pour les commits à combiner
# - Changer 'pick' en 'reword' pour les messages à modifier
# - Supprimer la ligne pour les commits à supprimer

# Après avoir sauvegardé, Git ouvrira d'autres éditeurs pour les nouveaux messages

# Force push (attention, seulement si vous êtes seul sur la branche)
git push origin ma-branche --force-with-lease
```

## Scénario 4 : Gestion des Conflits Complexes

**Situation** : Votre pull request a des conflits avec la branche principale après une longue période de développement.

**Exercice** :
1. Récupérez les derniers changements de main
2. Faites un merge de main dans votre branche
3. Résolvez les conflits dans:
   - Un fichier de configuration
   - Un composant partagé
4. Continuez le rebase après résolution

**Correction** :
```bash
git checkout ma-branche
git fetch origin
git merge origin/main

# Git indiquera les fichiers en conflit
# Ouvrez chaque fichier et recherchez les marqueurs <<<<<<<, =======, >>>>>>>

# Après résolution des conflits:
git add fichier_resolu.ext
git commit -m "Résolution des conflits avec main"

# Continuer le développement ou pousser les changements
git push origin ma-branche
```

## Scénario 5 : Utilisation des Hooks Git pour le Contrôle Qualité

**Situation** : Vous voulez implémenter des vérifications automatiques avant commit et push.

**Exercice** :
1. Créez un pre-commit hook pour:
   - Empêcher les commits sur main
   - Vérifier la syntaxe des messages de commit
2. Créez un pre-push hook pour:
   - Lancer les tests unitaires
   - Vérifier la couverture de code

**Correction** :
```bash
# Dans le dossier .git/hooks/

# pre-commit
#!/bin/sh
branch=$(git rev-parse --abbrev-ref HEAD)
if [ "$branch" = "main" ]; then
  echo "Les commits directs sur main sont interdits."
  exit 1
fi

# pre-push
#!/bin/sh
npm run test && npm run coverage
if [ $? -ne 0 ]; then
  echo "Les tests ont échoué ou la couverture est insuffisante"
  exit 1
fi

# Rendre les scripts exécutables
chmod +x pre-commit pre-push
```

## Scénario 6 : Travail avec les Submodules

**Situation** : Votre projet dépend d'une librairie interne stockée dans un autre dépôt.

**Exercice** :
1. Ajoutez le dépôt de la librairie comme submodule
2. Mettez à jour le submodule vers une nouvelle version
3. Initialisez et mettez à jour le submodule après un clone frais

**Correction** :
```bash
# 1. Ajout du submodule
git submodule add https://bitbucket.org/entreprise/lib-interne.git libs/lib-interne
git commit -m "Ajout du submodule lib-interne"
git push

# 2. Mise à jour du submodule
cd libs/lib-interne
git checkout v2.0.0
cd ../..
git add libs/lib-interne
git commit -m "Mise à jour de lib-interne vers v2.0.0"

# 3. Après un clone frais
git clone https://bitbucket.org/entreprise/projet-principal.git
cd projet-principal
git submodule init
git submodule update
```

## Scénario 7 : Utilisation de Git Flow avec Bitbucket

**Situation** : Vous adoptez Git Flow pour la gestion des branches dans votre projet.

**Exercice** :
1. Initialisez Git Flow dans votre dépôt
2. Commencez une nouvelle feature
3. Publiez la feature
4. Terminez la feature

**Correction** :
```bash
# 1. Initialisation
git flow init
# Accepter les valeurs par défaut ou les adapter

# 2. Commencer une feature
git flow feature start ajout-panier

# 3. Publier la feature
git flow feature publish ajout-panier

# 4. Terminer la feature
git flow feature finish ajout-panier
git push origin develop
```
