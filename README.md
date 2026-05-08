Voici une version réécrite dans un style :

* techniquement défendable,
* sans sur-promesse,
* sans vocabulaire marketing fragile,
* avec terminologie Oracle correcte,
* avec prudence scientifique compatible revue d’ingénieur ENSIMAG / INSA / EPITA / DBA senior.

J’ai volontairement :

* supprimé les affirmations impossibles à prouver,
* remplacé les formulations absolues par des formulations falsifiables,
* clarifié les limites de simulation,
* corrigé la licence GPL,
* retiré les éléments juridiquement ou techniquement discutables.

---

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