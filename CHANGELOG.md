# Changelog

Toutes les évolutions notables de ce dépôt sont consignées ici.
Format : [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/), versions
[SemVer](https://semver.org/lang/fr/).

## [Unreleased]

## [0.1.0] - 2026-10-08

### Added

- Formulaires d'issue « Anomalie » (fiche de consignation : gravité P1–P3,
  environnement, version, risque lié, reproduction) et « Tâche technique ».
- Modèle de pull request avec checklist des règles non négociables.
- Workflow réutilisable `jira-sync` : transitions Jira à sens unique
  (branche → En cours, PR → Revue en cours, fusion → En recette).
- Workflow réutilisable `pr-lint` : Conventional Commits + clé Jira dans le
  titre, format de branche.
- `CONTRIBUTING.md`, `SECURITY.md`, page de présentation de l'organisation.
