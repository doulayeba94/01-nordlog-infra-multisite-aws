# Étape 2 — Analyse des risques et points de défaillance

## Contexte
Sur la base de la cartographie établie à l'étape 1, il s'agit d'identifier formellement les points de défaillance uniques (SPOF) et d'évaluer les risques associés.

## À produire

### 2.1 Identification des SPOF
Tableau des points de défaillance uniques identifiés (ex : serveur WMS unique, lien ADSL non redondé par site, absence de bascule automatique) avec le système/service impacté par chacun.

### 2.2 Analyse de risques simplifiée
Pour chaque scénario de risque (au moins 5, incluant a minima : panne serveur WMS, coupure lien WAN entrepôt, panne datacenter siège, cyberattaque ransomware, erreur humaine de configuration) :
- Probabilité (1-4)
- Gravité (1-4)
- Niveau de risque (probabilité × gravité)
- Mesures de réduction proposées

### 2.3 Priorisation
Classement des risques par criticité décroissante, avec justification du traitement retenu (réduire/éviter/transférer/accepter) pour chacun.

## Livrables
- [ ] Tableau des SPOF
- [ ] Tableau d'analyse de risques (5 scénarios minimum)
- [ ] Classement et stratégie de traitement
