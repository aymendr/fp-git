
# 🧑‍🏫 Plan de cours : Git avec Bitbucket

## 🗓️ Durée : 3h30 – 4h

## 👥 Public : Développeurs débutants à intermédiaires

## 📦 Prérequis : Git installé, compte Bitbucket, éditeur de code

---

## 🔹 Partie 1 : Introduction à Git (30 min)

### 🔍 Objectifs :

* Comprendre le rôle de Git dans le développement collaboratif
* Maîtriser les commandes de base de Git en local

### 🧑‍💻 Activité 1 : Premier dépôt Git local

#### **Instructions :**

```bash
mkdir projet-demo
cd projet-demo
git init
echo "Hello Git" > README.md
git status
git add README.md
git commit -m "Premier commit"
git log
```

#### ✅ Correction :

Vérifiez que le commit est bien enregistré avec `git log`.

---

## 🔹 Partie 2 : Branches et fusion (30 min)

### 🔍 Objectifs :

* Créer et basculer entre des branches
* Fusionner des branches

### 🧑‍💻 Activité 2 : Création et fusion de branches

#### **Instructions :**

```bash
git checkout -b feature-hello
echo "Hello depuis feature" >> README.md
git commit -am "Ajout message dans feature"
git checkout main
git merge feature-hello
```

#### ✅ Correction :

Vérifiez que le message de la branche feature est présent dans `README.md`.

---
## 🔹 Partie 3 : Merge et Rebase

### 🔍 Objectifs :

* Créer et basculer entre des branches
* Fusionner des branches

### 🧑‍💻 Activité 3 : Création et fusion de branches

#### **Instructions :**

```bash
git checkout -b feature-hello
echo "Hello depuis feature" >> README.md
git commit -am "Ajout message dans feature"
git checkout main
git merge feature-hello
```

#### ✅ Correction :

Vérifiez que le message de la branche feature est présent dans `README.md`.

---

## 🔹 Partie 4 : Introduction à Bitbucket (20 min)

### 🔍 Objectifs :

* Créer un dépôt distant sur Bitbucket
* Lier le dépôt local à Bitbucket

### 🧑‍💻 Activité 4 : Lien dépôt local ↔ distant

#### **Instructions :**

1. Créez un dépôt vide sur Bitbucket (sans README).
2. Connectez-le :

```bash
git remote add origin https://bitbucket.org/<votre-utilisateur>/projet-demo.git
git push -u origin main
```

#### ✅ Correction :

Sur Bitbucket, vérifiez que les fichiers ont bien été poussés.

---

## 🔹 Partie 5 : Collaboration avec Bitbucket (1h)

### 🔍 Objectifs :

* Créer une branche distante
* Faire une pull request (PR)
* Gérer une revue de code

### 🧑‍💻 Activité 5 : Travailler avec une PR

#### **Instructions :**

1. Créez une branche :

```bash
git checkout -b feature-footer
echo "<footer>Site Web</footer>" > footer.html
git add footer.html
git commit -m "Ajout du footer"
git push -u origin feature-footer
```

2. Allez sur Bitbucket ➜ Créez une Pull Request de `feature-footer` vers `main`

3. Un binôme ou vous-même commentez et validez la PR, puis la fusionnez.

#### ✅ Correction :

Vérifiez que `footer.html` est bien intégré dans `main`.

---

## 🔹 Partie 6 : Résolution de conflits (30 min)

### 🔍 Objectifs :

* Gérer les conflits de fusion
* Comprendre les causes et solutions

### 🧑‍💻 Activité 6 : Simuler un conflit

#### **Instructions :**

1. Sur `main` :

```bash
echo "Version A" > conflit.txt
git add .
git commit -m "Version A"
```

2. Sur une branche :

```bash
git checkout -b conflit-branch
echo "Version B" > conflit.txt
git add .
git commit -m "Version B"
```

3. Retour sur `main`, puis :

```bash
git merge conflit-branch
```

4. Résolvez le conflit manuellement dans `conflit.txt`, puis :

```bash
git add conflit.txt
git commit
```

#### ✅ Correction :

Le fichier doit contenir la version fusionnée manuellement.

---

## 🔹 Partie 7 : Bonnes pratiques (10 min)

* Une branche = une fonctionnalité
* Commits clairs et fréquents
* PRs petites et faciles à relire
* Toujours pull avant de commencer

---

## 📁 Livrables fournis :

* ✔️ Fichier `README.md` initial
* ✔️ Script des commandes utilisées
* ✔️ Corrections des exercices
* ✔️ Bonus : fiche mémo Git (cheat sheet)

