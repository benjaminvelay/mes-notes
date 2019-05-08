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
