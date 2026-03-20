# Workshop GitHub

> Afin de bien commencer, veuillez cloner le repo GitHub de l'organisation correspondant à votre position dans la liste de l'intra (ex : si vous êtes en premier, prenez le repo n°1).

---

## Sommaire

1. [Add](#add)
2. [Commit](#commit)
3. [Push](#push)
4. [Les branches](#les-branches)
5. [Stash](#stash)
6. [Les fonctionnalités de GitHub](#les-fonctionnalités-de-github)

---

##  Add

Pour ajouter du code, on va utiliser la commande `git add`. On peut lui ajouter des fonctionnalités qui permettront un choix plus précis des fichiers à inclure, en créant un fichier `.gitignore`.

### À quoi sert un `.gitignore` ?

On peut spécifier un type de fichier, un dossier, ou même un fichier précis.  
Imaginons que nous avons un dossier `tmp` que nous ne voulons pas ajouter avec `git add` ; il suffit de mettre ceci dans le fichier `.gitignore` :

```gitignore
tmp/
```

Cela permettra automatiquement de ne pas inclure le dossier `tmp`, même si vous utilisez la commande `git add .` qui ajoute tous les fichiers présents dans le scope actuel dans la **zone d'ajout**.

>  La **zone d'ajout** désigne simplement tous les fichiers sélectionnés à être poussés sur le repo GitHub.

### `git reset`

On peut aussi utiliser la commande `git reset`. Son objectif est de revenir en arrière tout en laissant les fichiers modifiés dans la zone d'ajout. Elle peut également être utilisée pour **unadd** un fichier.

---

##  Commit

Créez un fichier texte `workshopGithub.txt` et committez-le.

### Méthodes de commit

```bash
git commit
git commit -m "votre message de commit"
```

### Conventional Commits

À Epitech, on attend un **conventional commit** afin de donner un maximum d'informations rien qu'avec le commentaire. Il se divise en trois parties :

| Partie | Description | Exemples |
|--------|-------------|---------|
| **Type** | Nature du code pushé | `feat`, `fix`, `update`, `style`, `delete` |
| **Scope** | Fichier(s) ou dossier(s) concerné(s) | `auth`, `README`, `src/` |
| **Message** | Description détaillée de ce qui a été fait | ... |

**Format :**
```
type(scope): description du commit
```

> Le but du commit est de donner le maximum d'informations sur chaque push. Dans le cadre d'une entreprise, votre responsable ne devrait pas avoir besoin d'aller voir le code pour comprendre ce que vous avez pushé.

### Le flag `-a`

Le flag `-a` permet d'ajouter et de committer en une seule commande les fichiers **déjà suivis** (modifiés). Il **ne fonctionne pas** pour les nouveaux fichiers.

```bash
git commit -ma "type(scope): description"
```

> Créez un nouveau fichier `githubCommit.txt`, ajoutez une ligne dans `workshopGithub.txt`, puis utilisez `git commit -ma` et enfin `git status`. Que peut-on observer ?

### `git diff`

La commande `git diff` permet de comparer deux sources de code :

```bash
git diff                        # Compare le code local avec le repo actuel
git diff <commit>               # Compare le code local avec un commit précis
git diff <commit1> <commit2>    # Compare deux commits entre eux
```

---

## Push

`git push` permet, après avoir commité son code, de l'envoyer sur le repo avec la description du commit.

Pour pousser sur une nouvelle branche pour la première fois :

```bash
git push --set-upstream origin nom-de-la-branche
```

---

## Les branches

Les branches permettent de bien séparer le code et de travailler dans un environnement sans conflits.

### Créer une branche

```bash
git checkout -b nom-de-la-branche
```

### Mettre à jour une branche

Si votre branche n'est pas à jour avec le `main` ou le `dev` :

```bash
git pull origin main   # ou dev
```

### Supprimer une branche

Depuis la branche `main` :

```bash
git branch -rd origin/nom-de-la-branche
```

---

##  Stash

`git stash` permet de mettre de côté les modifications en cours (non commitées) pour pouvoir merge plus facilement.

```bash
git stash          # Stocke les modifications de côté
git stash pop      # Réapplique les modifications et les supprime du stash
git stash apply    # Réapplique les modifications en les conservant dans le stash
```

**Workflow typique :**
1. Vous avez des modifications en cours non commitées
2. Vous faites `git stash`
3. Vous pullez depuis la branche cible
4. Vous faites `git stash pop` pour réappliquer vos modifications

---

##  Les fonctionnalités de GitHub

### Pull Requests

Dans l'onglet **Pull Requests**, vous pouvez créer une pull request pour merger une branche sur une autre. Vous pouvez y ajouter :
- Une description
- Des commentaires
- Des reviewers

### Projects

L'onglet **Projects** permet de diviser et d'organiser les tâches d'un projet, seul ou en équipe. Vous pouvez y créer des tâches et leur associer :
- Des **milestones**
- Des **issues**
- Des **due dates**

> Pour aller plus loin, il existe un autre outil qui automatise beaucoup de choses : **[Linear](https://linear.app)**

---

## Documentation
