---
layout: default
title: Khanlab Folder Structure
parent: Computing
nav_order: 1
permalink: /computing/folder_structure
---

# **NEW** Khan Lab storage migration 

Our digital alliance storage allocation on graham/nibi is migrating from ctb-akhanf to rrg-akhanf, to be completed by the end of August. 

With this change, we need to also enforce a major policy changes in how `project` space is used, so we can more easily comply with stricter storage and number of file quotas:

1. Project space must only be used for archived files related to curated datasets, completed analyses/processing, and archived checkpoints of in-progres analyses/processing. 

2. For any work in progress you must make use of your scratch folder. 

3. All data on the project drive must be kept in the centralized `khanlab` folder (see below), which will have subfolders for datasets and trainees. These must all be group-readable so we can monitor storage usage. 

4. Your personal project folder (e.g. in `~/projects/rrg-akhanf/$USER`) **must not** be used to store data, and should also be group-readable so we can monitor storage usage. 





# **Khan Lab Folder Structure**

This document outlines the **proposed** organized folder structure for our neuroimaging lab under `/projects/rrg-akhanf/khanlab`. This structure is designed to centralize data, streamline collaboration, and ensure consistency across all projects.
This structure aims to improve collaboration, data accessibility, and lab productivity.

---

## **Root Directory**
All lab-related data and projects are organized under:
```
/projects/rrg-akhanf/khanlab
```

### **Top-Level Directories**
```
| Directory               | Purpose                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------|
| `/datasets`             | Raw and derived datasets, organized by source (internal, external).        |
| `/trainees`             | Individual folders for archived data from lab members (current and past).                                   |
| `/code`                 | Central repository for lab-wide code, scripts, containers, and pipelines.                            |
```
---

## **Datasets Directory**
All datasets are stored in the `/datasets` directory, with raw and processed data grouped by dataset.

```
/datasets
    /internal        # Datasets generated within the lab
        /<dataset_name>
            /sourcedata        # Raw source
            /tabular           # Tabular data
            /bids              # BIDS (raw or minimally-preproc)
            /derivatives       # Processed data from pipelines (e.g., fMRIPrep, QSIprep)
            /code              # Dataset-specific code
    /external        # External datasets (e.g., HCP, UK Biobank)
```

---

## **Trainees Directory**
Individual folders for lab members, divided into **current** and **past** trainees. These folders should store the data 
that you wish to retain (e.g. analyses related to papers published or in-progress). These folders will inherit group-writable 
permission so that lab managers can move/archive the data at a later date.

### What about my folders in /project/<allocation>/<username>? 
These folders (one for each allocation, including default allocation and project allocations, should not be used for any
persistent data, since the lab managers do not have access to them for archiving, nor do your fellow lab members (for collaboration).
These folders will be wiped after you leave the lab.

```
/trainees
    /current
        /<username>
            /<project_name>
    /past
        /<username>
            /<archived_project_name>
```

---

## **Code Directory**
Centralized location for shared scripts, code, containers required by the group. This folder should be group-writable by default.

```
/code
  /containers
```



---

## **Folder Creation Guide**
When adding new data or projects:
1. **For Datasets**:
   - Create a folder under `/datasets/internal` or `/datasets/external`.
   - Use subfolders for `sourcedata`, `bids`, `tabular`, `derivatives`, `code`.
   - Ideally, raw data should be placed in `sourcedata`, and the code to generate the other folders
    should be in a github repository and cloned in `code`.

2. **For Trainees**:
   - Create a folder under `/trainees/current/<username>`.
   - Archive past members under `/trainees/past`.

3. **For Code**:  
   - Use github repositories under the khanlab org

---

## **Enforcing Structure**

**This section is under construction** 
1. Use automated scripts to ensure directory consistency.
2. Periodically audit the structure to maintain organization.
3. Follow permissions guidelines to prevent unauthorized access.

---



--- 
