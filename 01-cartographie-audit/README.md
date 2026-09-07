# Étape 1 — Cartographie et audit technique

## Contexte
Avant toute recommandation, il faut établir un état des lieux exhaustif : réseau, serveurs, flux applicatifs (WMS, ERP, terminaux mobiles).

## Données fournies (à utiliser pour l'analyse)

| Site | Lien WAN actuel | Latence moyenne | Incidents notables |
|---|---|---|---|
| Siège Lille | Fibre 50 Mbps, non redondée | 15 ms (local) | RAS |
| Entrepôt Lyon | VPN IPSec sur ADSL 20 Mbps | 45 ms vers siège | Panne WMS 8h (rupture lien) |
| Entrepôt Marseille | VPN IPSec sur ADSL 20 Mbps | 50 ms vers siège | Coupures fréquentes < 5 min |
| Entrepôt Rennes | VPN IPSec sur ADSL 10 Mbps | 60 ms vers siège | Lenteurs signalées en fin de journée |
| Entrepôt Strasbourg | VPN IPSec sur ADSL 10 Mbps | 55 ms vers siège | RAS |

Le WMS est hébergé sur un serveur physique unique au siège (pas de réplication). L'ERP est hébergé chez un prestataire externe (SaaS), accédé via Internet depuis chaque site.

## À produire

### 1.1 Cartographie applicative et réseau
- Schéma de l'architecture existante (sites, liens, serveurs, flux principaux)
- Tableau des flux applicatifs critiques (source, destination, protocole, criticité)

### 1.2 Analyse des liens WAN
- À partir du tableau ci-dessus, identifier les sites les plus à risque et pourquoi

### 1.3 Constats d'audit
- Synthèse des constats (documentaire, technique)
- Premier niveau de recommandations (avant l'analyse de risques formelle de l'étape 2)

## Livrables
- [ ] Schéma d'architecture existante
- [ ] Cartographie des flux applicatifs
- [ ] Synthèse des constats d'audit
