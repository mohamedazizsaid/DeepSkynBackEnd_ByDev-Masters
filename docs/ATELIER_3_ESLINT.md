# Atelier 3 — Exploration d'un outil de test statique

## 1. Outil choisi : ESLint

ESLint est un outil d'analyse statique pour JavaScript et TypeScript. Il inspecte le code sans lancer l'application et signale les problèmes correspondant aux règles configurées : erreurs probables, variables inutilisées, incohérences de code et certaines mauvaises pratiques.

## 2. Pourquoi ESLint pour DeepSkyn ?

Le backend DeepSkyn utilise NestJS et TypeScript. Le dépôt possède déjà :
- une configuration `.eslintrc.js` ;
- les dépendances `eslint`, `@typescript-eslint/parser`, `@typescript-eslint/eslint-plugin`, `eslint-config-prettier` et `eslint-plugin-prettier` ;
- un script `lint` dans `package.json`.

L'outil peut donc être intégré sans abonnement à un service externe. Il est adapté à une première démarche de qualité logicielle sur le module backend.

## 3. Application au projet

- Dépôt : https://github.com/mohamedazizsaid/DeepSkynBackEnd_ByDev-Masters
- Branche d'intégration proposée : `salim`
- Fichier de configuration : `.eslintrc.js`
- Workflow CI ajouté : `.github/workflows/eslint.yml`

### Exécution locale

Après installation des dépendances :

```bash
npm ci
npx eslint "{src,apps,libs,test}/**/*.ts"
```

Le script existant `npm run lint` utilise `--fix`, qui peut modifier automatiquement des fichiers. Pour une première inspection et pour la CI, la commande directe ci-dessus est préférable car elle ne demande pas de correction automatique.

## 4. Intégration continue

Le workflow GitHub Actions exécute ESLint lors d'un push sur `salim` ou la branche de travail de l'atelier, et lors d'une pull request vers `salim`. Le job installe Node.js 20, installe les dépendances avec `npm ci`, puis lance ESLint. Une erreur ESLint fait échouer le job et rend le résultat visible dans l'onglet Actions.

## 5. Comment lire le résultat

- **0 / succès** : ESLint n'a signalé aucune erreur bloquante selon la configuration actuelle.
- **Échec** : ouvrir les logs du job, relever le fichier, la ligne et la règle, puis corriger ou justifier l'exception.
- **Avertissements** : les examiner et les traiter selon la sévérité configurée.

Le statut du workflow doit être consulté après son exécution ; ce rapport ne prétend pas que le code passe l'analyse avant le lancement du job.

## 6. Résultats de l'inspection statique préliminaire

La configuration et les dépendances ESLint existantes ont été vérifiées dans le dépôt. La commande ESLint n'a pas été exécutée localement pendant la préparation de cet atelier : aucun résultat PASS/FAIL ni nombre d'anomalies n'est donc annoncé ici. Le workflow créé fournit l'exécution reproductible sur GitHub Actions.

## 7. Limites

ESLint ne prouve pas que les fonctionnalités métier sont correctes et ne remplace pas les tests unitaires, les tests d'intégration/E2E, les tests de sécurité ou la revue de code. Il ne détecte que les problèmes couverts par les règles et les fichiers analysés. La qualité des résultats dépend de la configuration.

## 8. Conclusion

ESLint est un choix pertinent pour le backend TypeScript de DeepSkyn car il est déjà installé et configuré. L'ajout d'un workflow CI permet d'automatiser l'analyse à chaque changement. La prochaine étape est de consulter le premier run, corriger les anomalies signalées et conserver son lien comme preuve d'exécution dans le compte rendu de l'atelier.

## Références

- Dépôt backend : https://github.com/mohamedazizsaid/DeepSkynBackEnd_ByDev-Masters
- Documentation officielle ESLint : https://eslint.org/docs/latest/
- GitHub Actions : https://docs.github.com/actions
