# Réponses — TP 7

## Q1

`actions/checkout` peut fonctionner sans `with` car ses valeurs par défaut utilisent le dépôt et la référence associés à l'exécution courante. `actions/setup-node` doit connaître la version de Node.js à installer ; le paramètre `node-version: 20` lui fournit cette configuration.

## Q2

Chaque job GitHub Actions s'exécute sur un runner et dans un système de fichiers isolés. Le dépôt désigne les sources versionnées, mais `report.txt` est généré pendant le job `build` et n'est pas enregistré dans Git. Le job `verify` ne peut donc le récupérer qu'en le transférant explicitement, ici avec un artefact.

## Q6

Une action locale référencée avec `./.github/actions/build-info` est un fichier du dépôt. Au début du job, le runner ne possède pas encore ces fichiers. `actions/checkout` doit donc télécharger le dépôt dans l'espace de travail avant que le runner puisse trouver et exécuter l'action locale.

## Q7

Dans une action composite, GitHub Actions exige que chaque step utilisant `run` déclare explicitement son interpréteur. Contrairement à une step définie directement dans un job, aucune valeur de shell implicite n'est appliquée dans les métadonnées de l'action composite. `shell: bash` rend donc l'exécution explicite et prévisible.

## Observation — Partie 4

Lors de l'exécution réussie du commit `b543cd6`, GitHub Actions a affiché 0 s pour la step de l'action composite `build-info`, contre 5 s pour la step de l'action Docker `docker-hello`. L'action Docker est plus lente au démarrage, car le runner doit préparer et lancer son conteneur, tandis que l'action composite exécute directement ses commandes dans l'environnement du runner. Les jobs complets `build` et `docker-hello` ont chacun duré 11 s, mais le job `build` contenait aussi l'installation de Node.js, la génération du rapport et son téléversement.
