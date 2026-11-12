# Contribuer à NovaPulse

Ce guide s'applique à tous les dépôts de l'organisation NovaPulse-lab. Chaque
dépôt complète ce socle commun avec son propre `guidelines.md` (conventions de
code de la stack concernée).

## 1. Du ticket au déploiement

```
Jira (NOVA-123)
  └─ issue GitHub créée automatiquement : [NOVA-123] …
       └─ branche  feat/NOVA-123-totp-enrollment (depuis dev) → Jira passe « En cours »
            └─ PR vers dev  feat(auth): add TOTP enrollment (NOVA-123)
                 ├─ ouverte (non brouillon)        → Jira passe « Revue en cours »
                 └─ fusionnée (squash) dans dev    → Jira passe « En recette »
                                                     puis « Terminé(e) » après recette
dev ──── PR de version  chore(release): v0.2.0 ────► main
```

- **Jira est la source de vérité.** On ne crée pas d'issue GitHub sans ticket
  NOVA ; l'issue est un miroir pour le développement.
- Les transitions automatiques sont **à sens unique** (jamais de retour
  arrière). Le passage en « Terminé(e) » se fait à la main dans Jira après
  validation de la ligne correspondante du cahier de recettes.

## 2. Branches

| Branche | Rôle | Reçoit | Environnement |
|---|---|---|---|
| `dev` | Intégration, **branche par défaut** | Les PR de travail, fusionnées en squash | Préproduction |
| `main` | Versions validées, toujours déployable | Uniquement les PR de version depuis `dev` | Production |
| `<type>/NOVA-<n>-<slug>` | Travail sur un ticket | — | Développement local |

| Élément | Format | Exemple |
|---|---|---|
| Branche de travail | `<type>/NOVA-<n>-<slug>`, créée depuis `dev` | `fix/NOVA-42-rounding-dividends` |
| Titre de PR de travail (vers `dev`) | `<type>(<scope>): <résumé> (NOVA-<n>)` | `fix(transactions): round dividends with bcmath (NOVA-42)` |
| Titre de PR de version (`dev` → `main`) | `chore(release): vX.Y.Z` | `chore(release): v0.2.0` |

Types autorisés : `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`,
`build`, `ci`, `chore`, `revert`, `security`.

**PR de version.** Fusionnée en *merge commit* (pas en squash) pour conserver
sur `main` l'historique des commits de `dev`. Avant de l'ouvrir : section
`[Unreleased]` du CHANGELOG renommée en `[X.Y.Z] - AAAA-MM-JJ`. Après la
fusion : étiquette `vX.Y.Z` sur `main`.

> Les dépôts sont privés en offre GitHub Free : la protection de branche n'est
> pas disponible. L'interdiction de pousser directement sur `dev` et `main`
> est donc une **règle d'équipe**, contrôlée par le workflow `PR lint` (qui
> refuse toute PR vers `main` ne venant pas de `dev`) et par la revue.

## 3. Commits

[Conventional Commits](https://www.conventionalcommits.org/fr/) dans les
branches, en anglais. Les PR de travail sont fusionnées en **squash** : le
titre de la PR devient le commit sur `dev`, d'où le format strict du titre (il
alimente le CHANGELOG et le lien avec Jira).

```
feat(portfolio): add asset allocation chart

Uses ECharts with a textual table alternative (RGAA 1.1).

Refs: NOVA-57
```

`!` après le type (`feat!:`) ou un pied `BREAKING CHANGE:` signale une rupture
de compatibilité.

## 4. Définition de « terminé »

Une tâche est terminée quand sa preuve existe :

- [ ] tests unitaires ajoutés ou mis à jour, CI au vert ;
- [ ] entrée dans le `CHANGELOG.md` du dépôt ;
- [ ] documentation mise à jour si impact (`architecture.md`, manuels) ;
- [ ] ligne du cahier de recettes ajoutée ou exécutée si fonctionnalité ;
- [ ] contrôle d'accessibilité si un écran est concerné ;
- [ ] aucune régression sur les règles métier non négociables (voir §5).

## 5. Règles non négociables

- Jamais de `float` pour l'argent : `bigint` en centimes, `decimal` pour les
  quantités, Value Object `Money`, calculs avec bcmath.
- Registre de transactions immuable : pas de suppression, correction par
  transaction d'annulation.
- Journal d'audit en ajout seul sur les accès et opérations financières.
- Aucun appel réseau externe pendant une requête utilisateur : passer par
  Messenger (retries + failed transport).
- Aucun secret dans le code ni dans les issues : variables d'environnement et
  secrets GitHub uniquement.
- Aucune donnée personnelle ou patrimoniale réelle dans les tickets, issues,
  journaux de CI ou captures.

## 6. Signaler une anomalie

Créer un ticket **Bug** dans Jira (projet NOVA) en remplissant la fiche :
gravité P1 à P3, environnement, version, étapes de reproduction, résultats
attendu et obtenu, lien Sentry. L'issue GitHub correspondante est générée
automatiquement. Les failles de sécurité suivent [SECURITY.md](SECURITY.md).
