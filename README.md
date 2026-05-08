# Oracle SIH (Système d'Information Hospitalier) — Démonstrations Techniques

> Ensemble de 5 applications HTML/CSS/JavaScript autonomes, sans dépendance externe et exécutables hors-ligne, destinées à la démonstration pédagogique de mécanismes Oracle Database et d’architectures SIH (Système d’Information Hospitalier) dans un contexte de conformité HDS/RGPD.

---

# Table des matières

1. [Objectifs et périmètre](#objectifs-et-périmètre)
2. [Méthodologie et limites](#méthodologie-et-limites)
3. [Fichier 1 : Architecture Infrastructure](#fichier-1--architecture-infrastructure)
4. [Fichier 2 : SQL Workbench PUI](#fichier-2--sql-workbench-pui)
5. [Fichier 3 : Lexique & Quiz Oracle](#fichier-3--lexique--quiz-oracle)
6. [Fichier 4 : Workflow de Décision](#fichier-4--workflow-de-décision)
7. [Fichier 5 : Advanced Performance Suite](#fichier-5--advanced-performance-suite)
8. [Thèmes transversaux](#thèmes-transversaux)
9. [Prérequis](#prérequis)
10. [Licence](#licence)

---

# Objectifs et périmètre

Ce projet a pour objectif de fournir des démonstrateurs pédagogiques interactifs permettant d’illustrer :

* certains mécanismes internes d’Oracle Database ;
* des problématiques de performance et de cohérence transactionnelle ;
* des stratégies d’architecture SIH ;
* des notions de sécurité et de conformité réglementaire ;
* des workflows de décision liés à l’exploitation d’infrastructures critiques.

Les applications ne constituent pas :

* un moteur Oracle réel ;
* un environnement de benchmark ;
* un outil de validation de capacité de production ;
* une simulation exhaustive du comportement du Cost Based Optimizer (CBO).

Les démonstrations privilégient la compréhension des mécanismes conceptuels et des ordres de grandeur observés dans des architectures Oracle modernes.

---

# Méthodologie et limites

## Conception

L’architecture fonctionnelle, les scénarios SIH et la sélection des concepts techniques ont été définis par Stéphane Bertin dans un objectif de vulgarisation avancée des mécanismes Oracle.

Le développement HTML/CSS/JavaScript a été réalisé avec assistance IA, puis relu, corrigé et validé manuellement.

---

## Sources techniques

Les mécanismes représentés reposent principalement sur :

* la documentation officielle Oracle ;
* les guides Oracle Database Concepts ;
* les guides Oracle Performance Tuning ;
* les bonnes pratiques Oracle Cloud Infrastructure ;
* des comportements couramment observés en exploitation Oracle.

---

## Nature des simulations

Les applications implémentent des modèles pédagogiques simplifiés permettant de représenter :

* des phénomènes de contention ;
* des mécanismes de cache ;
* des stratégies de partitionnement ;
* des cycles de cohérence transactionnelle ;
* des workflows analytiques distribués.

Les métriques affichées (temps, gains de performance, volumes I/O, ratios de compression, débits Spark) constituent des estimations pédagogiques et non des mesures contractuelles.

Certains phénomènes réels ne peuvent être reproduits fidèlement dans un environnement navigateur hors-ligne, notamment :

* la variabilité réseau ;
* les effets NUMA ;
* les comportements exacts du scheduler Oracle ;
* les mécanismes internes du CBO ;
* la gestion mémoire JVM ;
* les contentions concurrentes à forte charge ;
* les coûts réels de shuffle Spark.

---

# Fichier 1 : Architecture Infrastructure

**Fichier :** `1.oracle-infra-sih-demo.html`

Démonstrateur des mécanismes fondamentaux d’infrastructure Oracle dans un contexte hospitalier.

| Module              | Contenu                                                                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Multitenant CDB/PDB | Topologie `CDB$ROOT` + PDBs, isolation logique, Resource Manager, contention dictionnaire partagé, démonstration de masquage de données pour environnements de test |
| SGA / PGA Internals | Buffer Cache, politique LRU approximative, Touch Count, contention `cache buffers chains`, spill TEMP lors de saturation PGA                                        |
| I/O & Cohérence     | Undo/Redo, SCN, Read Consistency, recovery simplifié, illustration pédagogique d’ORA-01555                                                                          |
| Cloud & Sécurité    | TDE AES-256, BYOK, OCI France (`eu-france-1`), principes d’auto-tuning Oracle, distinction IA embarquée / IA générative                                             |

---

# Fichier 2 : SQL Workbench PUI

**Fichier :** `2.oracle-workbench-sih-demo.html`

Simulation d’un environnement de développement Oracle appliqué à une PUI (Pharmacie à Usage Intérieur).

Fonctionnalités principales :

* éditeur SQL/PLSQL ;
* snippets pédagogiques préconfigurés ;
* simulation d’états d’exécution SQL ;
* Explain Plan simplifié ;
* grille de résultats dynamique ;
* indicateurs de coût et d’activité logique ;
* démonstration RBAC et audit.

Exemples fournis :

* requêtes SQL multi-tables ;
* traitements batch PL/SQL (`BULK COLLECT`, `FORALL`) ;
* triggers de contrôle métier ;
* maintenance logique et audit.

Les plans d’exécution affichés sont illustratifs et ne reflètent pas un CBO Oracle réel.

---

# Fichier 3 : Lexique & Quiz Oracle

**Fichier :** `3.oracle-lexical-sih-demo.html`

Base de connaissances interactive couvrant des notions Oracle courantes :

* index B-tree et bitmap ;
* transactions et verrous ;
* SGA/PGA ;
* RMAN ;
* Data Guard ;
* partitionnement ;
* SQL*Loader ;
* vues dynamiques `V$`.

Le module comprend :

* un lexique technique ;
* des exemples SQL/PLSQL ;
* des QCM interactifs ;
* un mode de révision progressive.

Les extraits de code sont fournis à des fins pédagogiques et peuvent nécessiter adaptation pour une utilisation réelle.

---

# Fichier 4 : Workflow de Décision

**Fichier :** `4.oracle-lifecycle-sih-demo.html`

Simulation de workflows décisionnels liés à l’exploitation d’un SIH Oracle.

Thématiques couvertes :

* chiffrement ;
* haute disponibilité ;
* PRA/PCA ;
* upgrade ;
* stratégie cloud ;
* dimensionnement.

Le système attribue des scores relatifs de risque selon des heuristiques simplifiées représentant des bonnes pratiques généralement admises.

Il ne constitue pas :

* un outil d’audit ;
* une certification HDS ;
* une méthode formelle d’analyse de risque.

---

# Fichier 5 : Advanced Performance Suite

**Fichier :** `5.oracle-advanced-sih-demo.html`

Démonstrateur pédagogique de techniques d’optimisation avancées appliquées à des volumétries importantes.

| Module                | Contenu                                                                              |
| --------------------- | ------------------------------------------------------------------------------------ |
| Partitionnement       | Range partitioning, pruning logique, réduction d’I/O estimée, illustration PEL       |
| In-Memory             | Représentation simplifiée d’un stockage colonne, compression logique, scan vectorisé |
| OCI Data Flow & Spark | Workflow distribué simplifié : map, shuffle, reduce, write                           |
| Dashboard             | Comparaison relative des optimisations activées                                      |

Fonctionnalités :

* moteur de calcul simplifié ;
* paramètres interactifs ;
* visualisation de jobs distribués ;
* simulation de gains analytiques.

Les accélérations présentées correspondent à des scénarios favorables et ne doivent pas être interprétées comme des garanties de performance réelles.

---

# Thèmes transversaux

* données entièrement fictives ;
* aucune donnée médicale réelle ;
* architecture Vanilla JS / ES6 ;
* fonctionnement hors-ligne ;
* absence de dépendances externes ;
* design responsive ;
* composants mutualisés entre les modules.

---

# Conformité et sécurité

Les démonstrateurs s’inspirent :

* des principes RGPD (« Privacy by Design ») ;
* des exigences généralement associées aux environnements HDS ;
* des pratiques de cloisonnement et de chiffrement courantes dans les SIH.

Le projet ne constitue toutefois ni :

* une certification HDS ;
* une homologation de sécurité ;
* une validation réglementaire officielle.

---

# Lexique Technique (SIH & Oracle)

Ce glossaire détaille le jargon technique utilisé dans les démonstrateurs, couvrant l’architecture Oracle, les concepts avancés de base de données et le contexte hospitalier (SIH).

---

# Architecture Oracle & Instance

| Terme                                  | Définition                                                                                                                                                                 |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CDB (Container Database)**           | Base de données conteneur dans l’architecture Oracle Multitenant, hébergeant le dictionnaire de données partagé ainsi que les PDB.                                         |
| **PDB (Pluggable Database)**           | Base de données « branchable » au sein d’un CDB, contenant les données applicatives et fonctionnant comme une base quasi indépendante.                                     |
| **CDB$ROOT**                           | Conteneur racine du CDB stockant les métadonnées système communes à toutes les PDB.                                                                                        |
| **Multitenant**                        | Architecture Oracle permettant de consolider plusieurs bases pluggables (PDB) au sein d’une même base conteneur (CDB), généralement pilotée par une seule instance Oracle. |
| **Instance Oracle**                    | Ensemble constitué de la mémoire partagée (SGA) et des processus d’arrière-plan assurant l’accès et la gestion des fichiers de la base.                                    |
| **SGA (System Global Area)**           | Zone mémoire partagée par tous les processus Oracle d’une instance, contenant les caches et structures de contrôle internes.                                               |
| **PGA (Program Global Area)**          | Zone mémoire privée associée à un processus ou thread serveur, utilisée notamment pour les tris, opérations de hachage et variables de session.                            |
| **Buffer Cache**                       | Composant de la SGA stockant en mémoire les blocs lus depuis le disque afin de réduire les accès physiques.                                                                |
| **LRU (Least Recently Used)**          | Principe historique inspirant la gestion du Buffer Cache, basé sur la récence d’utilisation des blocs.                                                                     |
| **Touch Count**                        | Mécanisme moderne de gestion du cache privilégiant les blocs fréquemment accédés plutôt qu’une simple politique LRU stricte.                                               |
| **Redo Log Buffer**                    | Zone mémoire de la SGA stockant temporairement les entrées redo avant écriture sur disque.                                                                                 |
| **Resource Manager**                   | Fonctionnalité Oracle contrôlant l’allocation CPU, I/O et parallélisme entre sessions, groupes de consommateurs ou PDB.                                                    |
| **Dictionnaire de données**            | Ensemble de tables et vues internes stockant les métadonnées de la base (objets, utilisateurs, privilèges, structures).                                                    |
| **ASM (Automatic Storage Management)** | Gestionnaire de stockage Oracle optimisant la répartition, la redondance et les performances des fichiers de base.                                                         |
| **RAC (Real Application Clusters)**    | Architecture permettant à plusieurs instances Oracle de partager une même base physique pour assurer haute disponibilité et scalabilité.                                   |

---

# Mécanismes Internes & Performance

| Terme                                   | Définition                                                                                                                                |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **CBO (Cost-Based Optimizer)**          | Optimiseur Oracle utilisant les statistiques objets pour choisir le plan d’exécution estimé le moins coûteux.                             |
| **Explain Plan**                        | Représentation hiérarchique des opérations choisies par l’optimiseur pour exécuter une requête SQL.                                       |
| **Execution Plan Hash Value**           | Identifiant numérique unique représentant la structure logique d’un plan d’exécution.                                                     |
| **Read Consistency**                    | Mécanisme garantissant qu’une requête voit les données telles qu’elles existaient au début de son exécution.                              |
| **SCN (System Change Number)**          | Horloge logique interne synchronisant la cohérence transactionnelle et la récupération.                                                   |
| **Undo**                                | Données stockées dans les segments Undo permettant l’annulation des transactions et la cohérence en lecture.                              |
| **Redo**                                | Journal des modifications assurant la durabilité transactionnelle et la récupération après incident.                                      |
| **ORA-01555 (« Snapshot Too Old »)**    | Erreur indiquant qu’une requête longue ne trouve plus les informations Undo nécessaires à sa cohérence.                                   |
| **AWR (Automatic Workload Repository)** | Référentiel interne stockant l’historique des métriques de performance Oracle.                                                            |
| **ASH (Active Session History)**        | Historique échantillonné de l’activité des sessions Oracle utilisé pour l’analyse de performance.                                         |
| **Wait Events**                         | Événements indiquant pourquoi une session Oracle attend (I/O, verrous, CPU, contention).                                                  |
| **Cache Buffers Chains**                | Structures internes de synchronisation (latches/mutexes) protégeant les chaînes de blocs mémoire.                                         |
| **Latch / Mutex**                       | Mécanismes légers de synchronisation protégeant l’accès concurrent aux structures internes Oracle.                                        |
| **Spill TEMP**                          | Débordement d’opérations mémoire (tris, hash joins, agrégations) vers le tablespace TEMP lorsque la mémoire PGA allouée est insuffisante. |
| **TEMP Tablespace**                     | Tablespace temporaire utilisé pour les opérations SQL intermédiaires nécessitant du stockage transitoire.                                 |
| **Partition Pruning**                   | Technique où l’optimiseur élimine les partitions non pertinentes afin de réduire drastiquement les I/O.                                   |
| **Range Partitioning**                  | Découpage logique d’une table selon des intervalles de valeurs (dates, identifiants, seuils).                                             |
| **Adaptive Query Optimization**         | Mécanismes Oracle adaptant dynamiquement certaines décisions d’optimisation à l’exécution.                                                |
| **In-Memory Column Store (IMCS)**       | Structure mémoire stockant les données en format colonne pour accélérer l’analytique.                                                     |
| **In-Memory Option**                    | Option Oracle activant l’IMCS et l’optimisation analytique mémoire.                                                                       |
| **Scan Vectorisé**                      | Exécution exploitant le traitement SIMD CPU pour analyser plusieurs valeurs simultanément.                                                |
| **NUMA (Non-Uniform Memory Access)**    | Architecture matérielle où la latence mémoire dépend de la proximité physique entre processeur et mémoire.                                |

---

# Développement SQL & PL/SQL

| Terme                                | Définition                                                                                                         |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| **PL/SQL**                           | Langage procédural Oracle étendant SQL avec variables, boucles, exceptions et logique conditionnelle.              |
| **BULK COLLECT**                     | Instruction récupérant plusieurs lignes en mémoire afin de réduire les context switches SQL/PLSQL.                 |
| **FORALL**                           | Instruction exécutant des opérations DML en mode bulk pour limiter les allers-retours entre moteurs SQL et PL/SQL. |
| **Trigger**                          | Procédure stockée exécutée automatiquement en réponse à un événement DML ou système.                               |
| **RBAC (Role-Based Access Control)** | Modèle de sécurité attribuant les privilèges via des rôles plutôt que directement aux utilisateurs.                |
| **V$ Views**                         | Vues dynamiques exposant l’état courant de l’instance Oracle (sessions, mémoire, SQL, I/O, verrous).               |
| **Index B-Tree**                     | Structure d’index équilibrée optimisée pour les recherches exactes et par intervalle.                              |
| **Index Bitmap**                     | Index compressé adapté aux colonnes à faible cardinalité dans les charges analytiques.                             |
| **SQL*Loader**                       | Utilitaire Oracle de chargement massif de données depuis des fichiers externes.                                    |

---

# Infrastructure, Cloud & Sécurité

| Terme                                     | Définition                                                                                                      |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **HDS (Hébergement de Données de Santé)** | Certification réglementaire française obligatoire pour l’hébergement de données de santé à caractère personnel. |
| **RGPD**                                  | Règlement européen encadrant le traitement et la protection des données personnelles.                           |
| **TDE (Transparent Data Encryption)**     | Chiffrement natif Oracle protégeant les données au repos de manière transparente pour les applications.         |
| **AES-256**                               | Algorithme de chiffrement symétrique couramment utilisé par Oracle TDE.                                         |
| **BYOK (Bring Your Own Key)**             | Modèle cloud permettant au client de conserver la maîtrise de ses clés cryptographiques.                        |
| **OCI (Oracle Cloud Infrastructure)**     | Plateforme cloud publique d’Oracle.                                                                             |
| **eu-france-1**                           | Région OCI située à Marseille, utilisée pour les exigences de souveraineté et conformité françaises.            |
| **Data Guard**                            | Solution Oracle de réplication physique ou logique assurant haute disponibilité et reprise d’activité.          |
| **GoldenGate**                            | Solution Oracle de réplication logique temps réel et migration sans interruption.                               |
| **RMAN (Recovery Manager)**               | Outil Oracle de sauvegarde, restauration et récupération.                                                       |
| **PRA (Plan de Reprise d’Activité)**      | Dispositif technique permettant le redémarrage après sinistre.                                                  |
| **PCA (Plan de Continuité d’Activité)**   | Organisation garantissant le maintien des services critiques pendant un incident.                               |
| **Audit Oracle**                          | Mécanisme enregistrant les accès et actions effectuées sur les données sensibles à des fins de traçabilité.     |

---

# Contexte SIH (Système d’Information Hospitalier)

| Terme                                 | Définition                                                                                                     |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **SIH**                               | Ensemble des ressources logicielles, matérielles et humaines gérant l’information de santé d’un établissement. |
| **PUI (Pharmacie à Usage Intérieur)** | Service hospitalier assurant l’achat, le stockage et la dispensation des médicaments.                          |
| **Données de santé**                  | Informations relatives à l’état de santé physique ou mental, passé, présent ou futur d’une personne.           |
| **Cloisonnement**                     | Isolation logique ou physique des flux sensibles afin de limiter les risques d’accès non autorisé.             |
| **Auditabilité**                      | Capacité d’un système à fournir une traçabilité vérifiable des actions réalisées.                              |
| **Traçabilité**                       | Historisation des opérations critiques (qui, quoi, quand, comment).                                            |

---

# Big Data & Analytique

| Terme                                    | Définition                                                                                                 |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Apache Spark**                         | Moteur distribué open source de traitement massif de données en mémoire.                                   |
| **OCI Data Flow**                        | Service managé Oracle exécutant des traitements Apache Spark sans gestion d’infrastructure.                |
| **Map / Reduce**                         | Paradigme distribué où « Map » transforme/répartit les données et « Reduce » agrège les résultats par clé. |
| **Shuffle**                              | Redistribution réseau intermédiaire des données entre nœuds lors d’un traitement distribué.                |
| **Entrepôt de données (Data Warehouse)** | Base optimisée pour l’analyse et la lecture massive (OLAP).                                                |
| **OLTP (Online Transaction Processing)** | Traitement transactionnel optimisé pour écritures fréquentes et faible latence.                            |
| **OLAP (Online Analytical Processing)**  | Traitement analytique orienté agrégations complexes et lectures volumineuses.                              |

---

# Aide intégrée et Lexiques contextuels

Chaque application HTML incluse dans ce projet dispose de sa propre documentation interne, accessible directement depuis l'interface utilisateur. Aucune documentation externe n'est nécessaire pour comprendre les démonstrations.

## Fonctionnalités d'aide par onglet

Chaque onglet ou module au sein des 5 applications contient une section d'aide dédiée, généralement accessible via un bouton « ? » ou un panneau « Aide » en haut de l'interface. Ces sections fournissent :

*   **Le contexte fonctionnel** : Explication du scénario hospitalier (SIH) simulé.
*   **Les objectifs pédagogiques** : Ce que la démo vise à illustrer (ex: contention, plan d'exécution, workflow).
*   **Le mode d'emploi** : Instructions pas à pas pour interagir avec les simulateurs.
*   **Les limites de la simulation** : Rappel des différences entre le modèle pédagogique et le comportement réel d'une base de production.

## Lexiques techniques spécifiques

En plus du glossaire général présent dans ce fichier `README.md`, chaque fichier HTML intègre un **lexique technique contextuel** exhaustif.

Contrairement à un glossaire statique, ces lexiques internes :

1.  **Sont filtrés par pertinence** : Ils ne listent que les termes techniques effectivement utilisés dans l'onglet ou la démo en cours.
2.  **Sont interactifs** : Les définitions sont souvent accessibles au survol ou au clic sur les termes techniques dans l'interface.
3.  **Couvrent le spectre complet** : De l'architecture infrastructure (CDB/PDB, SGA) aux concepts Big Data (Spark, Shuffle), en passant par la sécurité (TDE, RBAC) et le développement (PL/SQL, Explain Plan).

Cette approche « *just-in-time*» permet à l'utilisateur de comprendre le jargon technique exactement au moment où il est confronté au concept, sans avoir à quitter l'application pour chercher une définition.

---

# Prérequis

Aucun prérequis logiciel spécifique.

Exécution :

* Chrome ;
* Firefox ;
* Edge ;
* tout navigateur moderne compatible ES6.

---

# Licence

Copyright (C) 2025 Stéphane Bertin

Ce programme est un logiciel libre ; vous pouvez le redistribuer et/ou le modifier selon les termes de la GNU General Public License telle que publiée par la Free Software Foundation ; version 3 de la licence, ou (à votre discrétion) toute version ultérieure.

Ce programme est distribué SANS AUCUNE GARANTIE, sans même la garantie implicite de qualité marchande ou d’adéquation à un usage particulier.

Pour plus d’informations :
[GNU General Public License](https://www.gnu.org/licenses/?utm_source=chatgpt.com)