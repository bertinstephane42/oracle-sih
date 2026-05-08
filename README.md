# Oracle SIH (Système d'Information Hospitalier) — Démonstrations Techniques

> 5 applications HTML/CSS/JS autonomes, zero-dépendance, hors-ligne, à but pédagogique — simulant l'infrastructure, le développement, la connaissance lexicale, les cycles de décision et l'optimisation avancée Oracle dans un contexte de Système d'Information Hospitalier (SIH) avec conformité HDS/RGPD.

---

## Table des matières

1. [Fichier 1 : Architecture Infrastructure](#fichier-1--architecture-infrastructure)
2. [Fichier 2 : SQL Workbench PUI](#fichier-2--sql-workbench-pui)
3. [Fichier 3 : Lexique & Quiz Oracle](#fichier-3--lexique--quiz-oracle)
4. [Fichier 4 : Workflow de Décision](#fichier-4--workflow-de-décision)
5. [Fichier 5 : Advanced Performance Suite](#fichier-5--advanced-performance-suite)
6. [Thèmes Transversaux](#thèmes-transversaux)
7. [Prérequis](#prérequis)
8. [Licence](#licence)

---

## Fichier 1 : Architecture Infrastructure

**Fichier :** `1.oracle-infra-sih-demo.html`

4 modules couvrant les fondations Oracle dans un CHU :

| Module | Contenu |
|---|---|
| Multitenant CDB/PDB | Topologie `CDB$ROOT` + 4 PDBs, Resource Plan (shares CPU/IO), contention dictionnaire partagé (`row cache objects`, `shared pool`), Data Masking via `DBMS_DATA_MASKING` pour clonage RGPD |
| SGA / PGA Internals | Buffer Cache LRU + Touch Count (Midpoint Insertion), Latch `cache buffers chains` (contention quadratique O(N²)), PGA Temp Spill (bascule disque ×500-×10000) |
| I/O & Cohérence | Cycle Undo/Redo, SCN (System Change Number), Read Consistency, Instance Recovery (SMON : Redo Apply + Undo Apply), simulation ORA-01555 Snapshot Too Old |
| Cloud Souverain & IA | TDE AES-256 / BYOK, OCI France `eu-france-1` certifié HDS, Auto-Tuning (index auto, SPM, stats), IA embarquée vs générative |

---

## Fichier 2 : SQL Workbench PUI

**Fichier :** `2.oracle-workbench-sih-demo.html`

Environnement de développement Oracle simulé pour la gestion des stocks PUI (Pharmacie à Usage Intérieur) :

- **Éditeur SQL/PL/SQL** avec sélecteur de 3 snippets pré-définis :
  - `[SELECT]` Stocks critiques — jointures multi-tables avec sous-requête
  - `[PL/SQL]` BULK COLLECT + FORALL — batch nocturne de réapprovisionnement
  - `[TRIGGER]` `trg_check_peremption` — blocage de dispensation des médicaments expirés
- **Machine d'états** 5 phases (IDLE → PARSING → EXECUTING → FETCHING → COMPLETED) avec délais simulés
- **Explain Plan** simulé avec arbre CBO et alertes d'indexation
- **Data Grid** dynamique, métriques (temps, Logical Reads, Physical Writes, Coût CBO)
- **Maintenance :** tablespaces, gestion RBAC (Least Privilege), Audit HDS, purge anonymisée RGPD

---

## Fichier 3 : Lexique & Quiz Oracle

**Fichier :** `3.oracle-lexical-sih-demo.html`

Base de connaissances Oracle interactive :

- **50 termes** couvrant : index (B-tree, bitmap, fonctionnel), verrous, transactions, SGA/PGA, RMAN, Data Guard, partitionnement, SQL\*Loader, External Tables, V\$ views…
- **18 exemples de code** exécutables : DDL (CREATE TABLE, contraintes), DML, PL/SQL (triggers, packages), Explain Plan, hints, audit, RMAN, Data Pump
- **20 questions QCM** avec feedback immédiat
- **Navigation** par 5 catégories : SQL, PL/SQL, Performance, Sécurité, Sauvegarde
- **Mode Workflow** 6 étapes : revue lexicale progressive avec shuffle aléatoire

---

## Fichier 4 : Workflow de Décision

**Fichier :** `4.oracle-lifecycle-sih-demo.html`

Guide interactif couvrant le cycle de vie Oracle en contexte HDS :

- **6 étapes** : Chiffrement, Haute Disponibilité, Dimensionnement, Upgrade, Stratégie Cloud, Reprise d'Activité
- **4 choix par étape** (bonne pratique, risqué, risqué++, piège) — mélangés aléatoirement à chaque session
- **Modale de confirmation** style Oracle avant changement de choix
- **Feedback uniquement** dans la console `#sim-log` (neutre, sans couleur)
- **Tableau de bord** : indicateurs de risque, barres de progression, historique
- **Graphique** : barres colorées par qualité de décision
- **Écran de complétion** : score final et message de risque (vert/ambre/rouge)

---

## Fichier 5 : Advanced Performance Suite

**Fichier :** `5.oracle-advanced-sih-demo.html`

4 modules d'optimisation avancée sur 5×10⁹ lignes / 2,5 To avec moteur de calcul algorithmique :

| Module | Contenu |
|---|---|
| Partitionnement Avancé | Simulation Range mensuel (120 partitions / 10 ans), Partition Pruning via métadonnées HIGH_VALUE/LOW_VALUE, PEL, réduction I/O de 95 % |
| In-Memory Column Store | Transposition Row→Column, compression IMCU (6,7×), scan vectorisé SIMD AVX2, passage de 5243 s à 0,1 s |
| OCI Data Flow & Spark | Architecture distribuée serverless (1–32 nœuds), shuffle, predicate pushdown Oracle Big Data Connector, coût estimé |
| Dashboard Comparatif | Score global moyenné par technologie active uniquement, barres avant/après, conformité HDS / ISO 27001 / COFRAC |

- **Moteur de calcul :** classe `PerformanceEngine` avec formules réalistes (pruning factor, compression IMCU, débit Spark 20 Go/s par nœud)
- **Animation interactive :** job Spark simulé en 20 étapes (Map → Shuffle → Reduce → Write) avec barres de progression par exécuteur
- **3 curseurs de paramétrage :** période d'analyse (1–120 mois), colonnes sélectionnées (2–200), nœuds de calcul (1–32)
- **Données :** PATIENT_SIMU_XXXX / PRESCRIPTION_HISTORY — NIR fictifs — volumétrie 5×10⁹ lignes

---

## Thèmes Transversaux

- **Données 100 % fictives** (NIR_FICTIF, MED_TEST_XXX, LOT_SIMU_XXX, PATIENT_FICTIF, Dr_DUMMY) — aucune donnée de santé réelle
- **Conforme RGPD Art. 25** (Privacy by Design) et **HDS** (Hébergement de Données de Santé)
- **Architecture :** ES6 Classes · Vanilla JS · Zero Dependency · Offline
- **Design :** Dark theme · grille responsive · police monospace · modales d'aide contextuelle avec focus trap
- **Cohérence visuelle** : palette CSS variables partagée, composants réutilisables entre les 5 fichiers

---

## Prérequis

Aucun. Ouvrir chaque fichier `.html` dans un navigateur récent (Chrome/Firefox/Edge).

---

## Licence

Copyright (C) 2025 Stéphane Bertin

Ce programme est un logiciel libre ; vous pouvez le redistribuer et/ou le modifier selon les termes de la GNU General Public License telle que publiée par la Free Software Foundation ; version 4 de la Licence, ou (à votre discrétion) toute version ultérieure.

Ce programme est distribué dans l'espoir qu'il sera utile, mais SANS AUCUNE GARANTIE ; sans même la garantie implicite de COMMERCIALISATION ou D'ADAPTATION À UN USAGE PARTICULIER. Voir la GNU General Public License pour plus de détails.

Vous devriez avoir reçu une copie de la GNU General Public License avec ce programme ; si ce n'est pas le cas, consultez <https://www.gnu.org/licenses/>.
