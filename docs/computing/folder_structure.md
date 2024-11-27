---
layout: default
title: Khanlab Folder Structure
parent: Computing
nav_order: 1
permalink: /computing/folder_structure
---


# **Khan Lab Folder Structure**

This document outlines the **proposed** organized folder structure for our neuroimaging lab under `/projects/<labnumber>/khanlab`. This structure is designed to centralize data, streamline collaboration, and ensure consistency across all projects.
This structure aims to improve collaboration, data accessibility, and lab productivity. For questions or feedback, contact the lab manager.

---

## **Root Directory**
All lab-related data and projects are organized under:
```
/projects/<labnumber>/khanlab
```

### **Top-Level Directories**
| Directory               | Purpose                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------|
| `/datasets`             | Raw and processed datasets, organized by source (internal, external, aggregated).        |
| `/trainees`             | Individual folders for lab members (current and past).                                   |
| `/code`                 | Central repository for lab-wide code, scripts, and pipelines.                            |
| `/docs`                 | Documentation files (e.g., dataset metadata, user guides, README files).                 |

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
            /logs              # Logs from processing or analysis steps
    /external        # External datasets (e.g., HCP, UK Biobank)
    /aggregated      # Combined datasets or multi-dataset studies
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

## **Docs Directory**
Documentation related to datasets, projects, or lab processes.

```
/docs
    dataset_guide.md
    pipeline_instructions.md
    lab_policies.md
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
   - Clone into relevant `code` subdirectories

---

## **Enforcing Structure**
1. Use automated scripts to ensure directory consistency.
2. Periodically audit the structure to maintain organization.
3. Follow permissions guidelines to prevent unauthorized access.

---



--- 
