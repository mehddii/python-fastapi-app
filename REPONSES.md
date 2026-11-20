# Réponses — TP 7

## Q1

`actions/checkout` peut fonctionner sans `with` car ses valeurs par défaut utilisent le dépôt et la référence associés à l'exécution courante. `actions/setup-node` doit connaître la version de Node.js à installer ; le paramètre `node-version: 20` lui fournit cette configuration.

## Q2

Chaque job GitHub Actions s'exécute sur un runner et dans un système de fichiers isolés. Le dépôt désigne les sources versionnées, mais `report.txt` est généré pendant le job `build` et n'est pas enregistré dans Git. Le job `verify` ne peut donc le récupérer qu'en le transférant explicitement, ici avec un artefact.

## Q6

Une action locale référencée avec `./.github/actions/build-info` est un fichier du dépôt. Au début du job, le runner ne possède pas encore ces fichiers. `actions/checkout` doit donc télécharger le dépôt dans l'espace de travail avant que le runner puisse trouver et exécuter l'action locale.

## Q7

Dans une action composite, GitHub Actions exige que chaque step utilisant `run` déclare explicitement son interpréteur. Contrairement à une step définie directement dans un job, aucune valeur de shell implicite n'est appliquée dans les métadonnées de l'action composite. `shell: bash` rend donc l'exécution explicite et prévisible.
