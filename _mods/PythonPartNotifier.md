---
layout: mod

authors: "apple1417" # Authors of the mod
title: Python Part Notifier # Title of the mod
version: "1.7" # Version of the mod
supported: "BL2 + TPS" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Shows the parts making up all of your items and weapons on their cards." # A short description of the mod itself.
description: "Shows the parts making up all of your items and weapons on their cards." # This is set in order to keep the SEO proper
longDescription: "Shows the parts making up all of your items and weapons on their cards. Yes this even includes Grenades, COMs, and Relics/Oz Kits. Has full mod support, so if a mod adds extra parts to a weapon or changes a part's mesh it will properly update. Unique part support is limited, they may just show the same as the base part with the same mesh.\n\n![Demo Image](https://cdn.discordapp.com/attachments/294502426302742529/614303846256082945/unknown.png)\n\nWhat exactly is shown on the card is very customizable through the options menu. Don't care about a part slot? You can turn it off. Running out of space with all the parts you want to show? You can remove the original description or turn the font size down. Or playing Randomizer and want to know what weapons each part comes from? Why not use detailed part names.\n\nNote that there are thousands of parts, so it's not impossible that the mod gets something wrong, don't be afraid to double check. If you do find an issue please report it alongside a gibbed code for the item." # Description of what the mod can do
categories: ['Utility'] # Category of the type of mod

requirements: [] # Requirements for the given mod
requirementTitles: [] # The link-friendly name of the requirements

issues: ""
download: "https://github.com/apple1417/bl-sdk-mods/raw/master/PythonPartNotifier/PythonPartNotifier.zip"
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