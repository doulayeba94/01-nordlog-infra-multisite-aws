# Analyse et modernisation d'une infrastructure multi-sites — Cas NORDLOG

> Mission fictive d'audit et de modernisation d'infrastructure, avec migration hybride vers AWS. Étude de cas pédagogique construite pour refléter une mission de conseil réelle.

## Contexte

**NORDLOG** est un groupe de logistique (5 sites : 1 siège + 4 entrepôts) dont le système d'information (WMS de gestion d'entrepôt, ERP) repose sur une infrastructure vieillissante et non redondante. Une panne du WMS de 8 heures a immobilisé les expéditions d'un entrepôt entier. La direction commande un audit complet suivi d'une modernisation, avec une migration partielle vers le cloud AWS pour réduire la dépendance aux datacenters physiques.

**Sites :**

| Site | Rôle | Effectifs |
|---|---|---|
| Siège (Lille) | Direction, IT, finance | 50 postes, 5 serveurs |
| Entrepôt Lyon | Logistique | 30 postes + 20 terminaux WMS mobiles, 3 serveurs locaux |
| Entrepôt Marseille | Logistique | 25 postes + 15 terminaux WMS |
| Entrepôt Rennes | Logistique | 20 postes + 12 terminaux WMS |
| Entrepôt Strasbourg | Logistique | 15 postes + 10 terminaux WMS |

**Contraintes :**
- Budget CAPEX max 300 000 €
- RTO WMS < 4h, RPO < 1h
- Délai global : 9 mois
- Aucune contrainte réglementaire sectorielle stricte (bonnes pratiques ANSSI comme référence)

## Sommaire de la mission

| Étape | Dossier | Objectif |
|---|---|---|
| 0 | [`00-cadrage-mission`](./00-cadrage-mission) | Périmètre, objectifs, référentiel, parties prenantes |
| 1 | [`01-cartographie-audit`](./01-cartographie-audit) | Cartographie et audit technique (réseau, serveurs, flux applicatifs WMS/ERP) |
| 2 | [`02-analyse-risques`](./02-analyse-risques) | Identification des points de défaillance (SPOF) et analyse des risques IT |
| 3 | [`03-architecture-cible-ha`](./03-architecture-cible-ha) | Architecture cible segmentée (VLAN, DMZ, zone de confiance) + haute disponibilité (cluster firewall, redondance) |
| 4 | [`04-pra-pca`](./04-pra-pca) | Élaboration d'un PRA/PCA (RTO/RPO par système) |
| 5 | [`05-migration-aws`](./05-migration-aws) | Migration partielle vers AWS (VPC, VPN site-to-site, sauvegarde externalisée) |
| 6 | [`06-budget-roadmap`](./06-budget-roadmap) | Proposition budgétaire et roadmap de migration |

## Compétences démontrées

Audit d'infrastructure multi-sites · Analyse de risques et identification de SPOF · Architecture réseau segmentée et haute disponibilité · Plan de continuité/reprise d'activité (PRA/PCA) · Cloud hybride AWS (VPC, VPN site-to-site) · Chiffrage et roadmap de migration
