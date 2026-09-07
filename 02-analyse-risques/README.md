# Étape 2 — Analyse des risques et points de défaillance

## Contexte

Sur la base de la cartographie établie à l'étape 1, il s'agit d'identifier formellement les points de défaillance uniques (SPOF) et d'évaluer les risques associés.

---

## 2.1 Identification des SPOF

| SPOF identifié | Système/service impacté en cas de défaillance |
|---|---|
| Serveur WMS unique au Siège, sans réplication | Gestion d'entrepôt (WMS) — les 4 entrepôts simultanément |
| Lien fibre du Siège non redondé | Accès WMS + ERP pour l'ensemble des sites, connectivité Internet du siège |
| Liens ADSL des 4 entrepôts, non redondés | Accès local au WMS depuis les terminaux mobiles de chaque site |
| Base de données WMS colocalisée avec le serveur applicatif (pas de séparation) | Intégrité et disponibilité des données WMS en cas de panne matérielle |
| Absence de segmentation réseau (constatée à l'étape 1) | Propagation potentielle d'un incident de sécurité à l'ensemble du SI |

---

## 2.2 Analyse de risques simplifiée

| Scénario de risque | Probabilité | Gravité | Niveau de risque | Mesures de réduction |
|---|---|---|---|---|
| Panne du serveur WMS central (matériel ou logiciel) | 3 | 4 | **12** | Réplication ou clustering du WMS, sauvegardes régulières testées, plan de bascule (cf. étapes 3-5) |
| Coupure d'un lien WAN entrepôt (déjà réalisé à Lyon) | 4 | 3 | **12** | Lien de secours 4G/5G par entrepôt, supervision proactive des liens |
| Cyberattaque de type ransomware (aucune segmentation, pas de sauvegarde externalisée) | 3 | 4 | **12** | Segmentation VLAN (étape 3), sauvegarde externalisée immuable (étape 5), EDR, sensibilisation des utilisateurs |
| Erreur humaine de configuration (aucune procédure formalisée constatée) | 3 | 3 | **9** | Procédures documentées, tests en environnement isolé avant application en production, contrôle à double validation |
| Panne du lien fibre du Siège | 2 | 4 | **8** | Redondance du lien fibre (second opérateur), bascule partielle vers le cloud (cf. étape 5) |

---

## 2.3 Classement et stratégie de traitement

### Classement par criticité décroissante

Trois scénarios obtiennent le même score brut (12) : **ransomware**, **panne serveur WMS central** et **coupure d'un lien WAN entrepôt**. Le score seul ne suffit pas à les départager — on applique un critère secondaire : **l'étendue de l'impact et sa réversibilité**.

| Rang | Scénario | Score | Justification du rang |
|---|---|---|---|
| 1 | Ransomware | 12 | Impact potentiellement total (tous les sites) et **irréversible** en l'absence de sauvegarde externalisée saine — le risque le plus grave car il peut détruire la donnée elle-même, pas seulement l'accès |
| 2 | Panne serveur WMS central | 12 | Impact total (tous les sites simultanément) mais **récupérable** via redémarrage/restauration — grave mais moins définitif que le ransomware |
| 3 | Coupure lien WAN entrepôt | 12 | Impact **local** (un seul site à la fois) et déjà partiellement anticipé (lien de secours recommandé dès l'étape 1) — probabilité la plus élevée mais portée la plus limitée |
| 4 | Erreur humaine de configuration | 9 | Impact variable selon le composant touché, généralement limité et corrigible rapidement |
| 5 | Panne du lien fibre Siège | 8 | Grave par nature (impact total) mais probabilité plus faible qu'une coupure ADSL (infrastructure fibre plus fiable que l'ADSL) |

### Stratégie de traitement retenue

| Scénario | Stratégie | Justification |
|---|---|---|
| Ransomware | **Réduire** | Combinaison de mesures techniques (segmentation, EDR) et organisationnelles (sensibilisation) — traité en détail à l'étape 3 |
| Panne serveur WMS | **Réduire** | Nécessite une architecture cible à haute disponibilité — objet direct de l'étape 3 |
| Coupure lien WAN entrepôt | **Réduire** | Lien de secours par site, déjà recommandé en quick win à l'étape 1, à généraliser dans l'architecture cible |
| Erreur humaine | **Réduire** | Mesures organisationnelles à faible coût, à intégrer dans la gouvernance du projet |
| Panne lien Siège | **Réduire + Transférer** | Redondance locale (réduire) complétée par un report de charge vers AWS (transférer une partie du risque vers l'infrastructure cloud, cf. étape 5) |

---

## Livrables

- [x] Tableau des SPOF
- [x] Tableau d'analyse de risques (5 scénarios)
- [x] Classement et stratégie de traitement
