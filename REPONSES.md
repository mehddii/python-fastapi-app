# Réponses — TP 7

## Q1

`actions/checkout` peut fonctionner sans `with` car ses valeurs par défaut utilisent le dépôt et la référence associés à l'exécution courante. `actions/setup-node` doit connaître la version de Node.js à installer ; le paramètre `node-version: 20` lui fournit cette configuration.

## Q2

Chaque job GitHub Actions s'exécute sur un runner et dans un système de fichiers isolés. Le dépôt désigne les sources versionnées, mais `report.txt` est généré pendant le job `build` et n'est pas enregistré dans Git. Le job `verify` ne peut donc le récupérer qu'en le transférant explicitement, ici avec un artefact.
