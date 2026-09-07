# Étape 5 — Migration partielle vers AWS

## Contexte
Réduire la dépendance au datacenter physique du siège en migrant une partie de l'infrastructure vers AWS, en particulier pour répondre aux exigences de continuité (PRA) définies à l'étape 4.

## À produire

### 5.1 Design VPC
- Schéma du VPC cible (subnets publics/privés, zones de disponibilité)
- Ce qui migre vers AWS (ex : réplica WMS, sauvegardes) vs ce qui reste on-premise

### 5.2 Connectivité site-à-site
- Design du VPN site-to-site entre le siège et le VPC AWS
- Impact sur le plan d'adressage existant (chevauchements à éviter)

### 5.3 Sauvegarde externalisée
- Stratégie de sauvegarde vers AWS (ex : S3 + cycle de vie vers Glacier), fréquence, rétention

## Livrables
- [ ] Schéma du VPC cible
- [ ] Design de la connectivité VPN site-to-site
- [ ] Stratégie de sauvegarde externalisée
