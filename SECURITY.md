# Politique de sécurité

## Signaler une vulnérabilité

Ne créez **pas** d'issue publique ni de ticket ordinaire pour une faille de
sécurité. Utilisez le signalement privé de GitHub (onglet *Security* →
*Report a vulnerability*) du dépôt concerné, ou contactez le responsable
technique du projet.

Indiquez : le composant touché, la version, les étapes de reproduction et
l'impact estimé. N'incluez aucune donnée personnelle réelle.

## Traitement

| Gravité | Prise en charge | Résolution visée |
|---|---|---|
| P1 — critique (fuite de données, contournement d'authentification) | < 4 h ouvrées | < 1 jour ouvré |
| P2 — majeure | < 1 jour ouvré | < 2 jours ouvrés |
| P3 — mineure | < 2 jours ouvrés | sprint suivant |

Chaque faille est consignée dans le registre des incidents (dépôt
NovaPulse-docs), rattachée au risque R1 ou R6 du référentiel, et corrigée par
le circuit normal d'intégration et de déploiement continus.

## Versions maintenues

Seule la dernière version déployée en production reçoit des correctifs.
