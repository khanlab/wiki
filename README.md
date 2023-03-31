# Khanlab Wiki

_Originally curated [here](https://github.com/myousif9/khanlab-osf)._

This wiki was built using Jekyll and Github pages using the JustTheDocs theme.

## Updating the Wiki
Each "page" of the wiki is found in its corresponding folder under `/docs`. The
front matter describes how the data should be ordered in the navigation, whether
a table of contents should be shown, whether it is a child or parent page, and
the subpath of the URL.

Example parent page
```
---
layout: default
title: Open Science
nav_order: 5
description: "Open-science practices of the Khan Lab"
has_children: false
permalink: /open-science
---
```

Example child page
```
---
layout: default
title: Website
parent: Onboarding
nav_order: 5
permalink: /onboarding/website
---
```

## Config
The config (`_config.yml`) has variables that set properties for the page. 
Importantly, the `callouts` should be kept be in mind as it sets the 
title and colour for each type of call out.

## Callouts
A callout can be set on the page using syntax that is similar to `{: .note}`. It
is important that the name of the callout, as well as the colour is set in the
config.


[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
