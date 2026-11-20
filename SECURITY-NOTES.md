# Notes de sécurité — TP 7

## Vérification de `actions/setup-node`

Consultation effectuée le 20 novembre 2026 :

- le créateur `Actions` possède le badge **Verified** sur [GitHub Marketplace](https://github.com/marketplace/actions/setup-node-js-environment) ;
- le [dépôt `actions/setup-node`](https://github.com/actions/setup-node) affiche environ **5,0 k étoiles** ;
- le code source se trouve dans le dossier **`src/`**.

## Q3

La référence `@main` est mobile : son contenu peut changer à chaque nouveau commit sans modification du workflow. Une mise à jour compromise ou incompatible serait donc exécutée automatiquement. Une version majeure comme `@v4` suit une ligne de version contrôlée et limite les changements inattendus. Pour une production exigeant une reproductibilité maximale, l'épinglage sur le SHA complet d'un commit vérifié est encore plus sûr.

## Q4

Non. Le badge **Verified** confirme que GitHub a vérifié l'identité du créateur comme partenaire officiel ; il ne prouve pas que chaque version du code est exempte de vulnérabilité, de compromission ou d'erreur. Il faut toujours examiner l'action, sa version et les permissions qu'elle demande.

## Q5

Avant d'utiliser en production une action d'un fournisseur inconnu, il faut notamment :

1. examiner son dépôt et le code de la version visée, ses dépendances, son historique de maintenance et ses alertes de sécurité ;
2. vérifier qu'elle demande uniquement les permissions et secrets indispensables, puis l'épingler sur un SHA de commit audité et immuable.
