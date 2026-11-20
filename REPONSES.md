# Réponses — TP 6

## Q1

Une écriture dans `GITHUB_ENV` est traitée par le runner GitHub Actions à la fin de la step. Le processus shell de la step en cours n'est donc pas modifié. La variable devient disponible uniquement pour les steps suivantes du même job.

## Q2

Le job `verify-env` n'affiche pas la valeur `my-app` : `APP_NAME` n'y est pas définie. Les variables écrites dans `GITHUB_ENV` sont limitées aux steps suivantes du job qui les a créées et ne sont pas transmises à un autre job.
