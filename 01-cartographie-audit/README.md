# Étape 1 — Cartographie et audit technique

## Contexte

Avant toute recommandation, il faut établir un état des lieux exhaustif : réseau, serveurs, flux applicatifs (WMS, ERP, terminaux mobiles).

## Données de trafic et incidents (fournies)

| Site | Lien WAN actuel | Latence moyenne | Incidents notables |
|---|---|---|---|
| Siège Lille | Fibre 50 Mbps, non redondée | 15 ms (local) | RAS |
| Entrepôt Lyon | VPN IPSec sur ADSL 20 Mbps | 45 ms vers siège | Panne WMS 8h (rupture lien) |
| Entrepôt Marseille | VPN IPSec sur ADSL 20 Mbps | 50 ms vers siège | Coupures fréquentes < 5 min |
| Entrepôt Rennes | VPN IPSec sur ADSL 10 Mbps | 60 ms vers siège | Lenteurs signalées en fin de journée |
| Entrepôt Strasbourg | VPN IPSec sur ADSL 10 Mbps | 55 ms vers siège | RAS |

---

## 1.1 Cartographie applicative et réseau

### Schéma de l'architecture existante

![Architecture existante NORDLOG](../docs/schemas/architecture-existante.svg)

### Tableau des flux applicatifs critiques

| Source | Destination | Protocole/Port | Criticité |
|---|---|---|---|
| Terminaux WMS mobiles (par entrepôt) | Serveur WMS (Siège) | TCP/443 (API applicative) | Critique |
| Serveur WMS | Base de données WMS (interne, Siège) | TCP/1433 | Critique |
| Postes utilisateurs (tous sites) | ERP SaaS (Internet, prestataire externe) | TCP/443 | Critique |
| Postes Siège | Active Directory / serveur fichiers | TCP/445, 389 | Moyenne |
| Tous sites | Messagerie (SaaS) | TCP/443 | Moyenne |
| Serveur WMS | NAS de sauvegarde (interne, nocturne) | TCP/445 | Basse |

---

## 1.2 Analyse des liens WAN

| Site | Niveau de risque | Analyse |
|---|---|---|
| **Siège Lille** | **Critique** (risque transverse) | Le lien fibre du siège n'est pas redondé, et tous les entrepôts en dépendent pour accéder au WMS (hébergé uniquement au siège). Une panne de ce lien ou du serveur WMS immobilise l'ensemble des 4 entrepôts simultanément. C'est le point de défaillance le plus structurant de toute l'infrastructure. |
| **Entrepôt Lyon** | Élevé (déjà matérialisé) | A déjà subi la panne de 8h à l'origine de la mission — confirme que l'absence de redondance ADSL sur ce site n'est pas un risque théorique mais un incident réel. Priorité de remédiation immédiate. |
| **Entrepôt Marseille** | Élevé | Les coupures fréquentes (<5 min) suggèrent un problème de couche physique ou de stabilité de la ligne ADSL plutôt qu'un simple manque de bande passante — chaque coupure interrompt les sessions applicatives WMS des terminaux mobiles, avec un impact cumulatif sur la productivité même sans panne totale. |
| **Entrepôt Rennes** | Moyen | Les lenteurs en fin de journée, combinées à la plus faible bande passante (10 Mbps), évoquent une saturation du lien aux heures de forte activité logistique (fin de journée = préparation des expéditions du lendemain). |
| **Entrepôt Strasbourg** | Latent (sous-estimé) | Aucun incident signalé à ce jour, mais la même faiblesse structurelle (ADSL 10 Mbps non redondé) que les autres sites est présente — l'absence d'incident ne signifie pas absence de risque, seulement qu'il ne s'est pas encore matérialisé. |

**Conclusion :** le risque n'est pas propre à un seul entrepôt mais **structurel** : aucun site n'a de lien redondé, et le siège constitue un SPOF critique dont dépendent tous les autres. Lyon et Marseille doivent être traités en priorité (incidents déjà avérés), mais une solution structurelle (redondance généralisée + réduction de la dépendance à un WMS mono-site) est nécessaire — c'est l'objet des étapes suivantes (analyse de risques, architecture cible, migration AWS).

---

## 1.3 Constats d'audit

### Synthèse des constats

```
L'audit de l'infrastructure réseau NORDLOG révèle une architecture
structurellement fragile : le Siège de Lille héberge l'unique instance
du serveur WMS sans réplication, sur un lien fibre lui-même non redondé,
constituant un point de défaillance unique dont dépendent les 4 entrepôts
pour l'ensemble de leur activité logistique. Cette fragilité s'est déjà
matérialisée sur le site de Lyon (panne de 8h ayant immobilisé les
expéditions). Les liaisons WAN des entrepôts, toutes basées sur de
l'ADSL en VPN IPSec sans secours, présentent des symptômes distincts
mais révélateurs d'un même défaut structurel : coupures fréquentes à
Marseille, saturation aux heures de pointe à Rennes, absence d'incident
signalé à ce jour à Strasbourg mais sans garantie de continuité.
Aucune segmentation réseau formelle (VLAN, DMZ) n'a été constatée à ce
stade, et l'architecture ne dispose d'aucun plan de reprise d'activité
documenté.
```

### Premiers éléments de recommandation (avant l'analyse de risques formelle de l'étape 2)

| Recommandation | Urgence |
|---|---|
| Mettre en place un lien de secours (4G/5G ou second opérateur) sur le site de Lyon | Immédiate — incident déjà survenu |
| Investiguer la cause physique des coupures récurrentes à Marseille (test de ligne, remplacement de modem/routeur) | Immédiate |
| Étudier une hausse de bande passante ou un lissage de charge en fin de journée à Rennes | Court terme |
| Redonder le lien fibre du siège (deuxième opérateur ou lien satellite/4G de secours) | Court terme — SPOF critique |
| Engager une réflexion sur la réplication ou l'externalisation du WMS (au-delà d'un simple lien réseau redondé) | Moyen terme — sera traité aux étapes 3 à 5 |

---

## Livrables

- [x] Schéma d'architecture existante
- [x] Cartographie des flux applicatifs
- [x] Synthèse des constats d'audit
