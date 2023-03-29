---
layout: default
title: Data
parent: Computing
nav_order: 4
permalink: /computing/data
---

## Data Practices

The majority of our data is kept on the network file system on Graham, as this 
is regularly backed up. Simlarly, our code and manuscripts are 
version-controlled in appropriate locations (see below for options).

{: .note}
Store your work somewhere where it is backed up and if possible, 
version controlled

## Data Storage
The Digital Alliance of Canada has different tiers of storage: `/home`, 
`/project`, and `/scratch`

* `/home` - store copies of your code and other small files
* `/project` - where project data will be coming from; use this folder for 
**finalized** data

{: .important}
The `/project` filesystem has a **STRICT** limit on the total number of files 
storage size, so you should zip/tar your files that reside there to ensure the 
average file size is at least 1GB

* `/scratch` - where active work should be done

{: .important}
Files on the `/scratch` filesystem expire after 60 days if they have not been
modified. You will be sent 2 e-mails prior to the deletion of these fies. Move
your data to `/project` once it has been finalized!

## Code
Code should be stored in a git repository (preferably on GitHub, using either a
public or private repository). Clone repositories can then be in your home 
directory, local machine, or scratch space. If you make a mistake, you can 
revert to a previous commit (e.g. saved version).

{: .note}
Store code, scripts, and markup documents here. Changes made should be 
committed and pushed to GitHub (e.g. time-stamped and associated with user).

## Manuscripts
Western provides a OneDrive account that can be used to store papers you are
reading or writing, as well as any other reference material. Alternatively, you
can store these on Google Drive. These tools make it easy to share and 
collaborate on documents.