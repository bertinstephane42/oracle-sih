# Oracle SIH (Système d'Information Hospitalier) — Démonstrations Techniques

> Ensemble de 8 applications HTML/CSS/JavaScript autonomes, sans dépendance externe et exécutables hors-ligne, destinées à la démonstration pédagogique de mécanismes Oracle Database et d’architectures SIH (Système d’Information Hospitalier) dans un contexte de conformité HDS/RGPD.

---

# Table des matières

1. [Objectifs et périmètre](#objectifs-et-périmètre)
2. [Méthodologie et limites](#méthodologie-et-limites)
3. [Fichier 0 : Architecture des Tablespaces et Fichiers de Données](#fichier-0--architecture-des-tablespaces-et-fichiers-de-données)
4. [Fichier 1 : Architecture Infrastructure](#fichier-1--architecture-infrastructure)
5. [Fichier 2 : Atelier SQL PUI](#fichier-2--atelier-sql-pui)
6. [Fichier 3 : Lexique Oracle PUI](#fichier-3--lexique-oracle-pui)
7. [Fichier 4 : Cycle de vie projet Oracle PUI](#fichier-4--cycle-de-vie-projet-oracle-pui)
8. [Fichier 5 : Suite Performance Avancée](#fichier-5--suite-performance-avancee)
9. [Fichier 6 : Assistant SQL PUI](#fichier-6--assistant-sql-pui)
10. [Fichier 7 : Bonnes Pratiques DBA SIH](#fichier-7--bonnes-pratiques-dba-sih)
11. [Thèmes transversaux](#thèmes-transversaux)
12. [Conformité et sécurité](#conformité-et-sécurité)
13. [Aide intégrée et lexiques contextuels](#aide-intégrée-et-lexiques-contextuels)
14. [Prérequis](#prérequis)
15. [Licence](#licence)

---

# Objectifs et périmètre

Ce projet a pour objectif de fournir des démonstrateurs pédagogiques interactifs permettant d’illustrer :

* certains mécanismes internes d’Oracle Database ;
* des problématiques de performance et de cohérence transactionnelle ;
* des stratégies d’architecture SIH ;
* des notions de sécurité et de conformité réglementaire ;
* des flux de décision liés à l’exploitation d’infrastructures critiques.

Les applications ne constituent pas :

* un moteur Oracle réel ;
* un environnement de test de performance (benchmark) ;
* un outil de validation de capacité de production ;
* une simulation exhaustive du comportement de l'Optimiseur Coût-Based (CBO).

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
* les guides *Oracle Database Concepts* ;
* les guides *Oracle Performance Tuning* ;
* les bonnes pratiques Oracle Cloud Infrastructure ;
* des comportements couramment observés en exploitation Oracle.

---

## Nature des simulations

Les applications implémentent des modèles pédagogiques simplifiés permettant de représenter :

* des phénomènes de contention ;
* des mécanismes de mise en cache ;
* des stratégies de partitionnement ;
* des cycles de cohérence transactionnelle ;
* des flux analytiques distribués.

Les métriques affichées (temps, gains en performance, volumes d'E/S, ratios de compression, débits Spark) constituent des estimations pédagogiques et non des mesures contractuelles.

Certains phénomènes réels ne peuvent être reproduits fidèlement dans un environnement navigateur hors-ligne, notamment :

* la variabilité réseau ;
* les effets NUMA ;
* les comportements exacts de l'ordonnanceur (scheduler) Oracle ;
* les mécanismes internes du CBO ;
* la gestion mémoire de la JVM ;
* les contentions concurrentes à forte charge ;
* les coûts réels de brassage de données (shuffle) dans Spark.

---

# Fichier 0 : Architecture des Tablespaces et Fichiers de Données

**Fichier :** `0.oracle-database-structure.html`

Application pédagogique présentant l'architecture de stockage hiérarchique d'Oracle Database, des tablespaces logiques aux fichiers de données physiques.

| Module | Contenu |
|--------|---------|
| Vue d'ensemble | Architecture visuelle (cylindres de données), composants principaux (tablespace, data file, segment), types de tablespaces (SYSTEM, SYSAUX, UNDO, TEMP, USERS) |
| Hiérarchie | Diagramme complet Database → Tablespace → Data File → Segment → Extent → Data Block, détail de chaque niveau, guide de bonnes pratiques avec commandes SQL |
| Visualisation Interactive | Simulation d'allocation d'extents dans un fichier de données (grille 8×8), segmentation tables/index, fragmentation |
| Comparaison | Tableau comparatif des 6 composants (nature, taille, relations), règles d'appartenance, commandes SQL de diagnostic (`dba_tablespaces`, `dba_data_files`, `dba_segments`) |
| Administration | Gestion des utilisateurs (CREATE USER, QUOTA), rôles et profils de sécurité (CREATE ROLE, CREATE PROFILE), maintenance courante (DBMS_STATS, shrink, controlfile) |
| Quiz | 20 questions avec correction immédiate couvrant l'intégralité des concepts de la page |
| Glossaire | 9 termes détaillés : Tablespace, Data File, Segment, Extent, Data Block, ASM, ASSM, UNDO, TEMP |

Fonctionnalités :

* navigation par onglets avec sidebar ;
* aide contextuelle par module (bouton « ? ») ;
* lexique technique intégré (bouton « L ») ;
* grille interactive d'allocation d'espace ;
* quiz auto-correctif avec score ;
* glossaire dépliable par clic.

---

# Fichier 1 : Architecture Infrastructure

**Fichier :** `1.oracle-infra-sih-demo.html`

Démonstrateur des mécanismes fondamentaux d’infrastructure Oracle dans un contexte hospitalier.

| Module              | Contenu                                                                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Multitenant CDB/PDB | Topologie `CDB$ROOT` + PDBs, isolation logique, Gestionnaire de Ressources (Resource Manager), contention du dictionnaire partagé, démonstration de masquage de données pour environnements de test |
| Internes SGA / PGA  | Cache de tampons (Buffer Cache), politique LRU approximative, comptage d'accès (Touch Count), contention des chaînes de tampons en cache (`cache buffers chains`), débordement TEMP (spill) lors de saturation PGA                                        |
| E/S et Cohérence    | Undo/Redo, SCN, Cohérence en lecture (Read Consistency), récupération (recovery) simplifié, illustration pédagogique d’ORA-01555                                                                          |
| Cloud et Sécurité    | TDE AES-256, BYOK, OCI France (`eu-france-1`), principes d’auto-ajustement (auto-tuning) Oracle, distinction IA embarquée / IA générative                                             |

---

# Fichier 2 : Atelier SQL PUI

**Fichier :** `2.oracle-workbench-sih-demo.html`

Simulation d’un environnement de développement Oracle appliqué à une PUI (Pharmacie à Usage Intérieur).

Fonctionnalités principales :

* éditeur SQL/PLSQL ;
* extraits de code (snippets) pédagogiques préconfigurés ;
* simulation d’états d’exécution SQL ;
* Plan d'exécution (Explain Plan) simplifié ;
* grille de résultats dynamique ;
* indicateurs de coût et d’activité logique ;
* démonstration RBAC et audit.

Exemples fournis :

* requêtes SQL multi-tables ;
* traitements par lots (batch) en PL/SQL (`BULK COLLECT`, `FORALL`) ;
* déclencheurs (triggers) de contrôle métier ;
* maintenance logique et audit.

Les plans d’exécution affichés sont illustratifs et ne reflètent pas un CBO Oracle réel.

---

# Fichier 3 : Lexique Oracle PUI

**Fichier :** `3.oracle-lexical-sih-demo.html`

Lexique interactif couvrant les concepts Oracle dans un contexte PUI (Pharmacie à Usage Intérieur), organisé en trois onglets :

| Onglet | Contenu |
|--------|---------|
| Dictionnaire Interactif | 50 termes Oracle filtrables par domaine (Structure, Objets, PL/SQL, Triggers, Performance, Sécurité) avec cartes détaillées |
| Laboratoire d'exemples | Exemples pédagogiques SQL/PLSQL avec exécution simulée et messages d'erreur ORA |
| Quiz & Validation | QCM interactifs avec score et progression |

Le dictionnaire couvre des notions telles que :

* index B-tree et bitmap ;
* transactions et verrous ;
* SGA/PGA ;
* RMAN ;
* Data Guard ;
* partitionnement ;
* SQL*Loader ;
* vues dynamiques `V$`.

---

# Fichier 4 : Cycle de vie projet Oracle PUI

**Fichier :** `4.oracle-lifecycle-sih-demo.html`

Guide interactif de déploiement d'une application PUI, simulant les conséquences des choix techniques à chaque étape du cycle de vie d'un projet Oracle.

Le serious game se déroule en 6 étapes séquentielles :

| Étape | Thématique |
|-------|-----------|
| 1 | Installation & architecture (jeu de caractères, CDB/PDB) |
| 2 | Sécurité (TDE, RBAC, audit) |
| 3 | Développement (schéma, index, PL/SQL) |
| 4 | Tuning (performance, SQL, indexation) |
| 5 | Recette (validation, test, mise en production) |
| 6 | Production (exploitation, surveillance, sauvegardes) |

Le système attribue des scores de risque relatifs selon des heuristiques simplifiées représentant des bonnes pratiques généralement admises.

Il ne constitue pas :

* un outil d’audit ;
* une certification HDS ;
* une méthode formelle d’analyse de risque.

---

# Fichier 5 : Suite Performance Avancée

**Fichier :** `5.oracle-advanced-sih-demo.html`

Démonstrateur pédagogique de techniques d’optimisation avancées appliquées à des volumétries importantes.

| Module                | Contenu                                                                              |
| --------------------- | ------------------------------------------------------------------------------------ |
| Partitionnement       | Partitionnement par intervalle (Range), élagage logique (pruning), réduction des E/S estimée, illustration PEL       |
| En mémoire (In-Memory)             | Représentation simplifiée d’un stockage colonnaire, compression logique, balayage vectorisé (vector scan) |
| OCI Data Flow et Spark | Flux distribué simplifié : mappage (map), brassage (shuffle), réduction (reduce), écriture                           |
| Tableau de bord             | Comparaison relative des optimisations activées                                      |

Fonctionnalités :

* moteur de calcul simplifié ;
* paramètres interactifs ;
* visualisation de tâches (jobs) distribuées ;
* simulation de gains analytiques.

Les accélérations présentées correspondent à des scénarios favorables et ne doivent pas être interprétées comme des garanties de performance réelles.

---

# Fichier 6 : Assistant SQL PUI

**Fichier :** `6.oracle-sql-helper-sih-demo.html`

Atelier pédagogique interactif de 18 scénarios SQL/PLSQL couvrant les mécanismes fondamentaux d'Oracle Database dans le contexte d'une Pharmacie à Usage Intérieur (PUI).

| Scénarios | Concepts abordés |
|-----------|-----------------|
| 1 – 2 | Jointure interne (INNER JOIN) et externe (LEFT/RIGHT OUTER JOIN) |
| 3 – 4 | Agrégation (GROUP BY) et sous-requête corrélée |
| 5 – 6 | BULK COLLECT / FORALL et Trigger AFTER DELETE |
| 7 – 8 | Vue simple (CREATE VIEW) et vue matérialisée (MATERIALIZED VIEW) |
| 9 – 10 | Index unique (UNIQUE INDEX) et partitionnement (PARTITION BY RANGE) |
| 11 – 12 | Séquence (SEQUENCE / NEXTVAL) et exception ZERO_DIVIDE |
| 13 – 14 | Curseur explicite et MERGE (upsert) |
| 15 – 16 | Fonction analytique (RANK) et CTE récursive (WITH) |
| 17 – 18 | FOR UPDATE NOWAIT et EXECUTE IMMEDIATE |

Fonctionnalités :

* éditeur SQL avec validation contextuelle ;
* détection des erreurs syntaxiques (`;` manquant, parenthèses déséquilibrées) ;
* vérification des mots-clés par concept avec suggestion par distance de Levenshtein ;
* validation des identifiants (tables/colonnes) par analyse du schéma DDL ;
* exécution simulée avec affichage de résultats et grille dynamique ;
* indices de débogage progressifs (hints) par scénario ;
* solution experte accessible après confirmation (pédagogie active) ;
* console de sortie et tableau de bord de progression.

Données 100 % fictives, contexte PUI, conformes à la charte graphique des modules 1 à 5.

---

# Fichier 7 : Bonnes Pratiques DBA SIH

**Fichier :** `7-oracle-best-practices-sih-demo.html`

Simulateur interactif des 9 bonnes pratiques DBA Oracle appliquées à une Pharmacie à Usage Intérieur (PUI). Score de risque SIH agrégé sur 200 points.

| Pilier | Contenu |
|--------|---------|
| Espace (Tablespace) | Simulation de remplissage d'un tablespace PHARMA_DATA. Choix AUTOEXTEND UNLIMITED vs MAXSIZE + ALERTE 80%. Ajout de datafile. Alerte visuelle à saturation PUI. |
| Statistiques (CBO) | Comparaison statistiques obsolètes (30 jours) vs à jour. Lancement de requête critique avec temps d'exécution, coût optimiseur et lignes estimées. |
| Recycle Bin | Gestion des objets supprimés : DROP, FLASHBACK TABLE TO BEFORE DROP, PURGE RECYCLEBIN. Liste visuelle des objets BIN$. |
| Indexation | Compromis lecture/écriture avec slider 0-10 index. Courbes de performance recalibrées selon l'impact réel des index B-tree. |
| Deadlocks | Mini-jeu d'évitement d'interblocage (ORA-00060) entre deux transactions concurrentes sur stock_med et lot. Schéma visuel des verrous. |
| Volumétrie (ILM) | Gestion de la croissance des données HISTORIQUE_ACTES (20+ ans). Partitionnement RANGE, archivage à froid (ARCHIVE_TS), purge légale à 10 ans. Curseur année 2022-2035. |
| Haute Disponibilité (Data Guard) | Scénario PRA avec Switchover planifié et Failover d'urgence. Sélecteur de mode de protection (Max Protection / Availability / Performance) avec impact RPO et lag de redo. |
| Cluster RAC | Diagramme 3 nœuds avec Cache Fusion. Simulation de transfert de blocs entre instances et panne d'un nœud avec bascule automatique des services TNS. |
| Performance (AWR) | Génération de rapport AWR simulé (Avant / Pendant incident). Top 5 Wait Events cliquables avec diagnostic SQL associé et correction appliquée. |

Fonctionnalités :

* RiskEngine avec score pondéré (0-200) et niveau de risque (CRITIQUE <80 / ÉLEVÉ 80-139 / MAÎTRISÉ ≥140) ;
* dashboard agrégé avec jauge globale et détail par pilier (9 piliers) ;
* commandes DBA intégrées (ALTER TABLESPACE, DBMS_STATS, FLASHBACK, CREATE INDEX, ALTER TABLE MOVE PARTITION, ALTER DATABASE COMMIT TO SWITCHOVER, DBMS_WORKLOAD_REPOSITORY) ;
* requêtes de diagnostic enrichies (DBA_TABLESPACE_USAGE_METRICS, V$LOCKED_OBJECT, INDEX_STATS, V$DATAGUARD_STATS, GV$CACHE_TRANSFER, DBA_HIST_SQLSTAT) ;
* 9 modales d'aide contextuelle + lexique technique avec 24 termes classés en 9 sections ;
* réinitialisation complète des scores ;
* console de log avec horodatage.

Données 100 % fictives, contexte PUI, conforme RGPD Art. 25. Charte graphique identique aux modules 1 à 6.

---

# Thèmes transversaux

* données entièrement fictives ;
* aucune donnée médicale réelle ;
* architecture JavaScript natif (Vanilla JS) / ES6 ;
* fonctionnement hors-ligne ;
* absence de dépendances externes ;
* conception adaptative (responsive design) ;
* composants mutualisés entre les modules.

---

# Conformité et sécurité

Les démonstrateurs s’inspirent :

* des principes RGPD (« Confidentialité dès la conception » / *Privacy by Design*) ;
* des exigences généralement associées aux environnements HDS ;
* des pratiques de cloisonnement et de chiffrement courantes dans les SIH.

Le projet ne constitue toutefois ni :

* une certification HDS ;
* une homologation de sécurité ;
* une validation réglementaire officielle.

---

# Aide intégrée et lexiques contextuels

Chaque application HTML incluse dans ce projet dispose de sa propre documentation interne, accessible directement depuis l'interface utilisateur via deux boutons dédiés situés dans l'en-tête de page. Aucune documentation externe n'est nécessaire pour exploiter les démonstrateurs.

## 1. Aide contextuelle par onglet (Bouton « ? »)

Chaque onglet ou module dispose d'un bouton d'aide spécifique, identifié par un point d'interrogation (**?**) dans l'en-tête. En le cliquant, l'utilisateur accède à une rubrique détaillée couvrant exclusivement le module actif.

**Cette aide fournit :**
*   **Le contexte fonctionnel** : Explication du scénario hospitalier (SIH) simulé dans l'onglet.
*   **Les objectifs pédagogiques** : Ce que la démo vise à illustrer (ex: mécanisme de contention, lecture de plan d'exécution, flux de décision).
*   **Le mode d'emploi** : Instructions pas à pas pour interagir avec les simulateurs et interpréter les résultats.
*   **Les limites de la simulation** : Rappel précis des différences entre le modèle pédagogique et le comportement réel d'une base de production.

## 2. Lexique technique global (Bouton « L »)

Un bouton distinct, identifié par la lettre **« L »**, est présent en permanence dans l'en-tête de chaque page. Il ouvre un lexique technique exhaustif propre à l'application en cours d'exécution.

**Caractéristiques de ce lexique interne :**
*   **Exhaustivité ciblée** : Il recense l'intégralité des termes techniques, acronymes et concepts spécifiques utilisés dans le fichier HTML ouvert (de l'architecture CDB/PDB aux concepts Big Data comme le *brassage de données*).
*   **Accessibilité immédiate** : Consultable à tout moment sans quitter la démo, il permet une compréhension « à la demande » des concepts affichés à l'écran.
*   **Autonomie totale** : Chaque fichier contient son propre glossaire intégré, fonctionnant parfaitement hors-ligne, sans dépendre du présent fichier `README.md`.

Cette double approche (aide ciblée par onglet + lexique global) permet à l'utilisateur de maîtriser le jargon technique exactement au moment où il est confronté au concept, fluidifiant ainsi l'apprentissage des mécanismes Oracle et SIH.

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
[GNU General Public License](https://www.gnu.org/licenses/)