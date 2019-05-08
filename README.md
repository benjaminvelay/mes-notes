## Nouvelles

* **Voir les n derniers commits**:
  ```
  $ git log -n
  ```

* **Enregister les fichiers ajoutés sur le dernier commit**:
  ```
  $ git commit --amend
  ```
  Attention, en cas de branche déjà poussée sur github, la synchronisation doit être forcée :
  ```
  $ git push -f origin mabranche
  ```

* **Voir les branches actives**:

  ```
  $ git branch
  ```
  Pour voir toutes les branches avec leur dernier commit :
    ```
  $ git branch -v
  ```

* **Remettre à jour un repo par rapport à un autre**:

  ```
  git reset --soft origin/master
  ```
  Dans ce cas, a remis à jour le repos local (master), en prenant en référence le repo en ligne (origin)
  <br/>Existe aussi avec la versoin --hard

## Maîtrisées

## Heroku commandes

* **Avoir les logs d'une app**:

  ```
  $ heroku logs -a app
  ```
* **Accéder à la console d'une app**:

  ```
  $ heroku run rails c -a dividi-staging
  ```

  Ou en utilisant le remote :

  ```
  $ heroku run rails c -r staging
  ```

* **Problème de variable d'environnement HOST** *
  La nouvelle version de Puma utilise une variable d'environnement HOST, la définition dans Heroku de Host supprime celle de Puma

## Nouvelles

* **Envoyer une requête AJAX**:
  ```
  fetch("https://places-dsn.algolia.net/1/places/query", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ query: event.currentTarget.value })
  })
  ```


## Maîtrisées

## Nouvelles

* **Savoir quel shell est utilisé**:

  ```
  $ echo $SHELL
  ```

* **Liste des shells**:

  ```
  $ cat /etc/shells
  ```

* **Ajouter un alias**:

  Recupérer le lien du dossier racine
  ```
  $ pwd
  ```
  Se rendre dans ce dossier et ouvrir le fichier .zshrc (Ctrl +H pour afficher les fichiers cachés dans Linux)
  Repérer dans quel fichier sont chargés les alias
  Ouvrir le fichier correspondant (souvent .aliases)

* **Avoir la liste de tous les binaires dans un projet rails**:

  ```
  $ ll bin
  ```

  La liste se trouve dans le dossier /bin de l'app.

* **Ecoutez les paths**:

  ```
  $ echo $PATH
  ```

  ou pour que ce soit plus lisible :

  ```
  $ echo $PATH | tr : \\n
  ```

  Signifie l'ordre dans lequel le système cherche une variable dossier par dossier.

* **Liens symboliques**:

  Pour avoir les commandes possibles :
  ```
  $ man ln
  ```

  Paramétrer le lien avec la cible et le nom, par exemple :
  ```
  $ ln -s /home/thibault/code/thibault173/dividi dividi
  ```

  Accéder au dossier dividi local en tapant depuis n'importe ou :
  ```
  $ cd dividi
  ```

  Avoir la liste de tous les liens symboliques (donne en réalité tous les droits d'exécution des scripts)
  ```
  $ ls -l
  ```

* **Redirection des ports**:

  ```
  $ subl /etc/hosts
  ```

  La modification de ce fichier entraîne une redirection des adresses en local.

* **Wepback**:

  ```
  $ webpack-dev-server
  ```

  Permet de lancer webpack en local, pour éviter d'avoir à recharger la page web à chaque fois, cela ouvre un socket en local ?!?


## Maîtrisées

## Maintenance des gems

* **Règle primordiale**:

  Utiliser $ bundle update avec parcimonie !

* **Versionning des gems**:

  premier chiffre : version majeure = gros changements de structure
  deuxième chiffre : version mineure = changements mineurs, compatibles avec la version de base
  troisième chiffre : patchs, plutôt liés à la sécurité ou petits bugs

* **Indiquer pour chaque gem la version utilisée**:

  gem 'lambda', '~>2.2'
  signifie que lorsque la commande bundle update est exécutée, la gem lambda va aller chercher les patchs (versions 2.2.x)

* **Exécuter un bundle update**:

  Attention : si la version de la gem n'est pas indiquée, cela va aller chercher la dernière version à jour.

* **Exécuter un bundle outdated**:

  Voir à la main pour chaque gem et effectuer la mise à jour.

## Gem

* **Rubycritic**:

Permet d'auditer la complexité du code.

churn = taux de commits effectués sur un fichier.

* **erb**:

Permet de générer une base de données visuelle à partir du schéma.



## Autres infos rails

Attention sur ruby 3 : FrozenStringLiteralComment, un gros changement est prévu.

## Requêtes SQL avec Active Record

preload()

  @posts = Post.order(created_at: :desc).preload(:author)

  Effectue 2 requêtes en bdd.

eager_load()

  @posts = Post.order("authors.name").eager_load(:author)

  Effectue 1 seule requête en bdd, avec un LEFT INNER JOIN

includes()

  En fonction de la demande, choisit la meilleure solution entre preload() et eager_laod().

joins()

  Permet de sélectionner uniquement les données voulues en y associant un select(), la requete SQL est INNER JOIN et non LEFT OUTER JOIN.
  Aller sur joins() uniquement lorsque les données sont vraiment importantes et que le besoin de performance est nécessaire.

