# Réponses — TP 6

## Q1

Une écriture dans `GITHUB_ENV` est traitée par le runner GitHub Actions à la fin de la step. Le processus shell de la step en cours n'est donc pas modifié. La variable devient disponible uniquement pour les steps suivantes du même job.

## Q2

Le job `verify-env` n'affiche pas la valeur `my-app` : `APP_NAME` n'y est pas définie. Les variables écrites dans `GITHUB_ENV` sont limitées aux steps suivantes du job qui les a créées et ne sont pas transmises à un autre job.

## Q3

L'opérateur `>` remplace le contenu de `GITHUB_OUTPUT`. S'il est utilisé pour chaque écriture de deux outputs dans la même step, la seconde écriture efface la première et seul le dernier output reste disponible. L'opérateur `>>` ajoute chaque output au fichier sans supprimer les précédents.

## Q4

`GITHUB_ENV` ne transmet une variable qu'aux steps suivantes du même job. Les jobs s'exécutent dans des environnements séparés. `GITHUB_OUTPUT` permet à une step de produire une valeur, que le job expose ensuite explicitement comme output et qu'un job dépendant récupère via le contexte `needs`.

## Q5

Sans `needs: build`, le job `deploy` ne dépend plus de `build` et peut démarrer en parallèle. Le résultat de `build` n'est pas présent dans son contexte `needs`, donc `needs.build.outputs.full_version` n'est pas disponible et la version complète ne peut pas être transmise à `deploy`.
