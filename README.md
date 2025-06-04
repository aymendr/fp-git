#### **Merge VS Rebase**

- créer une nouvelle branche
```bash
git checkout -b feature_1
```
- Ajouter 3 modifications, commiter et pousser le code vers le remote à chaque fois
```bash
git add . && git commit -m "am 1" && git push
git add . && git commit -m "am 2" && git push
git add . && git commit -m "am 3" && git push
```

- Basculer sur master et rajouter un commit
```bash
git checkout master
git add . && git commit -m "am 1 user2" && git push
```

- Basculer sur feature_1 et faire un rebase
```bash
git checkout feature_1
git rebase master
```

- Resoudre les conflits et faire un rebase --continue
```bash
git add . && git rebase --continue
```

- Une fois le rebase réussi sur la branche feature_1 on bascule sur master et on fait un merge de la feature_1
```bash
git checkout master
git merge feature_1
```

- on pousse le code final vers le remote
```bash
git push
```