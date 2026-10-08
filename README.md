# .github — socle commun de l'organisation NovaPulse-lab

Ce dépôt est **public** : GitHub n'applique les fichiers par défaut d'une
organisation que depuis un dépôt `.github` public. Il ne contient aucun code
métier ni secret.

| Fichier | Effet |
|---|---|
| `.github/ISSUE_TEMPLATE/` | Formulaires d'issue (anomalie, tâche) proposés dans tous les dépôts qui n'ont pas les leurs |
| `.github/pull_request_template.md` | Modèle de PR par défaut |
| `.github/workflows/jira-sync.yml` | Workflow réutilisable : fait avancer le ticket Jira selon la branche et la PR |
| `.github/workflows/pr-lint.yml` | Workflow réutilisable : vérifie le titre de PR et le nom de branche |
| `CONTRIBUTING.md`, `SECURITY.md` | Règles de contribution et de signalement, affichées dans chaque dépôt |
| `profile/README.md` | Page de présentation de l'organisation |

## Utiliser les workflows réutilisables

Dans chaque dépôt de code, `.github/workflows/governance.yml` appelle :

```yaml
uses: NovaPulse-lab/.github/.github/workflows/jira-sync.yml@main
secrets: inherit
```

Secrets attendus **dans chaque dépôt** (les secrets d'organisation ne sont pas
accessibles aux dépôts privés en offre Free) :

- `JIRA_USER_EMAIL` : adresse du compte Atlassian ;
- `JIRA_API_TOKEN` : jeton d'API Atlassian.

## Historique

Voir [CHANGELOG.md](CHANGELOG.md).
