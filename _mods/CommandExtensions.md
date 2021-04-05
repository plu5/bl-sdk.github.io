---
layout: mod

authors: "apple1417" # Authors of the mod
title: Command Extensions # Title of the mod
version: "1.5" # Version of the mod
supported: "BL2 + TPS" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Adds a few new console commands, which are fully compatible with blcmm files." # A short description of the mod itself.
description: "Adds a few new console commands, which are fully compatible with blcmm files." # This is set in order to keep the SEO proper
longDescription: "Adds a few new console commands, and provides functionality for other mods to do the\nsame. All these commands are fully compatible with blcmm files, you can just put them\nin your mod and have users merge it with other files and enable/disable various\ncategories and it all just keeps working fine.\n\n[See here for info on the builtin commands and how to write mods using them.](https://github.com/apple1417/bl-sdk-mods/blob/master/CommandExtensions/Writing-Mods.md)" # Description of what the mod can do
categories: ['Library'] # Category of the type of mod

requirements: [] # Requirements for the given mod
requirementTitles: [] # The link-friendly name of the requirements

issues: ""
download: "https://github.com/apple1417/bl-sdk-mods/raw/master/CommandExtensions/CommandExtensions.zip"
source: "https://github.com/apple1417/bl-sdk-mods/" # Link to source code
license: ['GNU GPLv3', 'https://choosealicense.com/licenses/gpl-3.0'] # License name, link about the license from https://choosealicense.com/

---
**Contents**
* TOC
{:toc}

## {{page.title}}

Mod by: {{page.authors}}
Current Version: {{page.version}}

<p></p>
### Description

{{page.longDescription | markdownify }}

Currently Supports: `{{page.supported}}`

{% if page.categories.size > 0 %}
Categories:
{% for category in page.categories %}
  * [{{category}}](/types/{{category}})
{% endfor %}
<p></p>
{% endif %}

{% if page.requirements.size > 0 %}
### Requirements

{% for requirement in page.requirements %}

{% assign reqName = page.requirementTitles[forloop.index0] %}

{% for mod in site.mods %}

{% assign modName = mod.path | remove_first: '_mods/' %}
{% assign xz = reqName | append: '.md' %}

{% if modName == xz %}
* [{{ requirement }}]( {{ reqName | relative_url | prepend: '/mods'}} ) <sup>[(Direct Download)]({{mod.download}})</sup>
{% endif %}
{% endfor %}

{% endfor %}
<p></p>
{% endif %}

### Links

{% if page.download != "" %}
You can download {{page.title}} here: [Download Link]({{page.download}})
{% endif %}

{% if page.issues != "" %}
Report issues here: [Issue Tracker]({{page.issues}})
{% endif %}

{% if page.source != "" %}
View the source code here: [Source Code]({{page.source}})
{% endif %}

{% if page.license.size > 0 %}
This mod is licensed using {{page.license[0]}} <sup>[?]({{page.license[1]}})</sup>
{% endif %}