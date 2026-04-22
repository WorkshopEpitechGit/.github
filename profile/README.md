# 🧪 Workshop GitHub — Branches, Pull Requests & Collaboration

> Atelier pratique pour découvrir le workflow Git/GitHub en équipe.  
> Chaque module contient un contexte réaliste, des commandes à exécuter et des questions de validation.

---

## Sommaire

1. [Mise en place](#1-mise-en-place)
2. [Branches](#2-branches)
3. [Push & Remote](#3-push--remote)
4. [Pull Request](#4-pull-request)
5. [Conflits](#5-conflits)
6. [Bonus & Challenge final](#6-bonus--challenge-final)

---

## 1. Mise en place

> **Contexte :** Tu rejoins une équipe qui développe un site web. Tout le monde travaille sur le même dépôt GitHub. Avant de coder, il faut configurer ton environnement.

### Exercice 1 — Cloner le dépôt partagé `[pratique]`

L'équipe a déjà un dépôt sur GitHub. Tu dois en faire une copie locale sur ta machine.

```bash
git clone https://github.com/equipe/projet-web.git
cd projet-web
ls -la   # Observer les fichiers, dont le dossier .git
```

**Question :** Que signifie `origin/main` dans `git branch -a` ?

- A. La branche principale sur ton PC
- B. La branche `main` du dépôt distant (GitHub) 
- C. Une branche supprimée

---

## 2. Branches

> **Contexte :** Le chef de projet demande d'ajouter une page "À propos". Tu ne dois **pas** modifier directement `main` — toujours travailler dans une branche dédiée.

> A quoi ca sert les branches ? => Eh bah Jami ca sert à organiser dans un premier temps ton code, tu te retrouves plus facilement dans un endroit dédiée a une feature. Ca permet aussi a tes coéquippiers de suivre ton avancé avec les notions d'après, à travers une pull request on force nos équipiers a lire notre code afin qu'ils puissent dire si oui ou non il semble correcte

> Dans quel contexte on met en place des branches ? => C'est pas compliqué, si tu as une nouvelles features qu'elle soit grande ou non tu **DOIS** faire une branche, que ce soit une gestion de map ou la création d'un bouton tu dois toujours faire des pull request

### Exercice 2.1 — Créer et basculer sur une branche `[pratique]`

Une branche est une copie parallèle du code. Les modifications n'affectent pas `main` tant que tu n'as pas mergé.

```bash
git checkout -b [nom-du-chef-de-groupe]/titre   # Créer ET basculer d'un coup
git branch                           # L'étoile indique la branche courante
```

> 🟡 Convention de nommage courante : `feature/xxx` pour les nouvelles fonctionnalités, `fix/xxx` pour les corrections de bugs. C'est très important que vos branches est un nom complet, on est censé savoir de quoi est consitué votre branch ! Pour aller plus loin sur la convention et "automatiser" les noms des branches linear permet de faire une gestion des branches avec la mise en place de nom adapté ainsi que des tickets lié a ceci.

---

### Exercice 2.2 — Faire des modifications et committer `[pratique]`

Crée la page `about.html`, puis enregistre tes changements dans un commit.

```bash
echo about.html => '<h1>À propos</h1>' > about.html
git status                           # about.html apparaît en rouge (untracked)
git add about.html                   # Ajouter au staging area
git status                           # about.html en vert (staged)
git commit -m "feat: ajouter la page about"
```

> 🟡 `git add .` ajoute **tous** les fichiers modifiés. Sois précis pour éviter de committer des fichiers non désirés. Pour plus d'information demandé la cheat-sheet de github

---

### Exercice 2.3 — Naviguer entre branches `[concept]`

Tu peux basculer entre branches à tout moment. Observe que les fichiers changent réellement sur ton disque !
Demander a un deuxième membre de créer une autre branch et refaite les étapes 2.1 et 2.2 afin de créer une nouvelle branche et essayer ces étapes suivantes

```bash
git checkout main                    # Retour sur main (about.html disparaît)
ls                                   # about.html n'est plus là !
git checkout [nom-de-votre-deuxième-coéquippier]/titre      # Retour sur ta branche
ls                                   # about.html est de retour
```

**Question :** Que se passe-t-il si tu as des modifications non commitées et que tu tentes de changer de branche ?

- A. Git les supprime automatiquement
- B. Git refuse ou te demande de stash/commit d'abord 
- C. Git les transfère sur l'autre branche

---

## 3. Push & Remote

> **Contexte :** Ta branche existe localement, mais tes collègues ne la voient pas encore. Il faut pousser ton travail sur GitHub pour pouvoir collaborer.

### Exercice 3.1 — Push ta branche sur GitHub `[pratique]`

La première fois, tu dois dire à Git où push cette branche.

```bash
git push --set-upstream origin [nom-du-chef-de-groupe]/titre   # -u = définir l'upstream (une seule fois)
git push                                 # Les fois suivantes, git push suffit
```

> 🟡 `origin` est l'alias du dépôt distant (GitHub). Tu peux le voir avec `git remote -v`.

---

### Exercice 3.2 — Récupérer le travail des autres `[pratique]`

Pendant que tu travaillais, une collègue a pushé des changements sur `main`. Tu dois les récupérer.

```bash
git fetch origin          # Télécharger sans modifier tes fichiers
git checkout main
git pull                  # = git fetch + git merge
git log --oneline --graph # Voir les nouveaux commits
```

> 🟡 `git pull` met directement à jour ta branche locale. `git fetch` est plus prudent — il télécharge sans fusionner.

---

### Exercice 3.3 — Comprendre fetch vs pull `[concept]`

La différence entre `fetch` et `pull` est subtile mais importante en équipe.

```bash
git fetch origin                # Récupère, n'applique PAS
git diff main origin/main       # Voir ce qui a changé avant d'appliquer
git merge origin/main           # Appliquer manuellement
```

**Question :** Quelle commande télécharge les changements distants **sans** modifier ta branche locale ?

- A. `git pull`
- B. `git fetch`
- C. `git clone`

---

## 4. Pull Request

> **Contexte :** Ta page "titre" est prête. Avant de l'intégrer à `main`, l'équipe doit relire ton code. C'est à ça que sert la Pull Request.

### Exercice 4.1 — Créer une Pull Request sur GitHub `[pratique]`

Une PR est une demande de fusion. Elle permet la revue de code, les discussions, et les tests automatiques.

```bash
git push origin feature/page-about   # S'assurer que tout est pushé
```
Après avoir push sur ta branch, tu auras directement la capacité de pouvoir fusionné ta branch avec la branch que tu souhaites 

Ensuite, sur GitHub :
1. Clique sur l'onglet **Pull Requests** → **New pull request**
Ou alors :
1. Clique sur compare and pull request dans l'affichage principal du repo
2. Choisis `base: main ← compare: feature/page-about`
3. Donne un titre clair et une description de tes changements
4. Clique sur **Create pull request**


> ⚠️⚠️⚠️ Une bonne description de PR explique **quoi** et **pourquoi**, pas seulement comment.

---

### Exercice 4.2 — Faire une revue de code `[concept]`

En binôme : l'un crée la PR, l'autre la relit. Utilisez les commentaires GitHub pour les retours.

| Rôle | Action |
|------|--------|
| **Auteur de la PR** | Décrit clairement ce que tu as fait et pourquoi dans la description |
| **Reviewer** | Clique sur "Files changed", commente les lignes, approuve ou demande des changements |
| **Auteur (suite)** | Répond aux commentaires, fait les corrections demandées, puis re-push |
| **Reviewer (suite)** | Vérifie les corrections et approuve quand tout est bon |

> 🟡 Sur GitHub, tu peux suggérer directement une modification de code dans un commentaire avec le bouton `+/-`.

---

### Exercice 4.3 — Merger la Pull Request `[pratique]`

Une fois approuvée, la PR peut être fusionnée dans `main`.

```bash
git checkout main
git pull                                       # Récupérer le merge fait sur GitHub
git branch -d feature/page-about              # Supprimer la branche locale
git push origin --delete feature/page-about   # Supprimer la branche distante
```

**Question :** Pourquoi supprimer la branche après le merge ?

- A. Pour garder le dépôt propre — la branche a rempli son rôle 
- B. C'est obligatoire, sinon Git crashe
- C. Pour libérer de l'espace disque (les commits sont perdus)

---

## 5. Conflits

> **Contexte :** Deux personnes ont modifié le même fichier en même temps. Git ne sait pas quelle version garder — il faut résoudre le conflit manuellement.

### Exercice 5.1 — Provoquer un conflit (intentionnellement) `[pratique]`

Pour comprendre les conflits, il faut en créer un. Travaillez à deux : modifiez la même ligne du même fichier dans deux branches différentes.

```bash
git checkout main && git pull
git checkout -b fix/titre
echo '<h1>Mon super site</h1>' > index.html
git add . && git commit -m "fix: changer le titre"

git checkout main
echo '<h1>Notre super projet</h1>' > index.html   # Un collègue a changé la même ligne
git add . && git commit -m "fix: autre titre"
```

---

### Exercice 5.2 — Identifier et lire un conflit `[concept]`

Lors du merge, Git insère des marqueurs dans le fichier pour montrer les deux versions.

```bash
git merge fix/titre   # Git signale un conflit !
cat index.html        # Observer les marqueurs de conflit
```

Le fichier contiendra quelque chose comme :

```
<<<<<<< HEAD
<h1>Notre super projet</h1>
=======
<h1>Mon super site</h1>
>>>>>>> fix/titre
```

> 🟡 `<<<<<<< HEAD` = ta version actuelle. `>>>>>>> fix/titre` = la version à merger. Le séparateur `=======` divise les deux.

---

### Exercice 5.3 — Résoudre le conflit `[pratique]`

Ouvre le fichier dans un éditeur, choisis quelle version garder (ou combine les deux), puis supprime les marqueurs.

```bash
code index.html        # Éditer manuellement, supprimer les marqueurs
git add index.html     # Marquer le conflit comme résolu
git commit -m "merge: résoudre conflit sur le titre"
git log --oneline --graph   # Voir le commit de merge
```

> ⚠️ Si tu te trompes, `git merge --abort` annule tout et te ramène à l'état avant le merge.

**Question :** Après avoir édité le fichier pour résoudre un conflit, quelle est la prochaine étape ?

- A. `git merge --continue`
- B. `git push` directement
- C. `git add <fichier>` puis `git commit` 

---

## 6. Bonus & Challenge final

> **Contexte :** Votre équipe maîtrise les bases ! Voici des commandes avancées très utiles au quotidien, suivies d'un challenge en équipe.

### Exercice 6.1 — git stash : mettre de côté `[concept]`

Tu dois changer de branche mais tu as des modifications en cours non prêtes à committer ? `git stash` les met temporairement de côté.

```bash
git stash             # Sauvegarder les modifs en cours
git checkout autre-branche   # Changer de branche sans conflit
git stash pop         # Récupérer ses modifs plus tard
git stash list        # Voir tous les stashs
```

> `git stash pop` réapplique **et** supprime le stash. `git stash apply` le garde pour réutilisation.

---

### Exercice 6.2 — git rebase : rejouer l'histoire `[concept]`

Au lieu de merger (qui crée un commit de merge), `rebase` rejoue tes commits par-dessus `main`. L'historique reste linéaire.

```bash
git checkout feature/ma-feature
git rebase main               # Rejouer mes commits sur main à jour
git log --oneline --graph     # Historique propre et linéaire
```

> ⚠️ Ne jamais rebase une branche déjà partagée avec d'autres (`origin/...`). Rebase réécrit l'historique !

---

### 🏆 Challenge final — Workflow complet `[challenge]`

En équipe de 3, réalisez le workflow complet **sans aide** :

1. **Personne A** crée une branche `feature/footer` et ajoute un pied de page
2. **Personne B** crée une branche `feature/navbar` et ajoute une navigation
3. **Personne C** modifie aussi `index.html` (pour provoquer un conflit)
4. A et B ouvrent chacun une **PR sur GitHub**
5. Faites la **revue croisée** et mergez dans l'ordre
6. **Résolvez les conflits** si nécessaire

> Objectif : tout le monde doit avoir une PR approuvée et mergée dans `main` d'ici la fin du workshop !

---

## 📚 Récapitulatif des commandes essentielles

| Commande | Description |
|----------|-------------|
| `git clone <url>` | Copier un dépôt distant en local |
| `git status` | Voir l'état des fichiers |
| `git add <fichier>` | Ajouter au staging area |
| `git commit -m "message"` | Enregistrer un snapshot |
| `git checkout -b <branche>` | Créer et basculer sur une branche |
| `git push -u origin <branche>` | Pousser une branche sur GitHub |
| `git fetch` | Télécharger sans appliquer |
| `git pull` | Télécharger et appliquer |
| `git merge <branche>` | Fusionner une branche |
| `git stash` | Mettre les modifs de côté |
| `git rebase <branche>` | Rejouer les commits |
| `git log --oneline --graph` | Visualiser l'historique |

---