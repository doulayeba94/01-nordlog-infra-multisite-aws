# Étape 3 — Architecture cible segmentée et haute disponibilité

## Contexte
Répondre aux SPOF et risques identifiés à l'étape 2 par une architecture cible segmentée et redondante, respectant le budget CAPEX (300 000 € max, à réconcilier avec l'étape 6).

## À produire

### 3.1 Segmentation réseau
- Plan de segmentation par site : VLAN (utilisateurs, WMS/serveurs, DMZ, management)
- Définition de la/les zone(s) de confiance (trusted zone) et de la DMZ (pour les flux ERP SaaS et futurs flux AWS)

### 3.2 Haute disponibilité
- Design d'un cluster firewall (actif/passif ou actif/actif) au siège
- Proposition de redondance des liens WAN pour les entrepôts les plus critiques (identifiés à l'étape 2)

### 3.3 Schéma d'architecture cible
Schéma complet intégrant segmentation + HA (à déposer dans `../docs/schemas/`)

## Livrables
- [ ] Plan de segmentation VLAN/DMZ par site
- [ ] Design du cluster firewall et de la redondance WAN
- [ ] Schéma d'architecture cible
