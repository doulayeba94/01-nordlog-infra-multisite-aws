# Étape 4 — Plan de Reprise/Continuité d'Activité (PRA/PCA)

## Contexte
Formaliser un PRA/PCA pour répondre à la contrainte RTO < 4h / RPO < 1h sur le WMS, système le plus critique identifié.

## À produire

### 4.1 Classification des systèmes
Tableau des systèmes (WMS, ERP, messagerie, fichiers partagés...) avec RTO et RPO cible pour chacun, justifiés par leur criticité métier.

### 4.2 Stratégie de reprise
Pour le WMS notamment : réplication (synchrone/asynchrone), site de secours ou bascule cloud (lien avec l'étape 5), fréquence de sauvegarde.

### 4.3 Procédure de test du PRA
Modalités et fréquence de test du plan (ex : test annuel en environnement isolé), et indicateurs de succès.

## Livrables
- [ ] Tableau RTO/RPO par système
- [ ] Stratégie de reprise détaillée (WMS en priorité)
- [ ] Procédure de test du PRA/PCA
