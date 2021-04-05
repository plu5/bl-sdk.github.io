---
layout: mod

authors: "juso" # Authors of the mod
title: Pokelands # Title of the mod
version: "1.0" # Version of the mod
supported: "BL2" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Pokemon, but in Borderlands 2. Kinda." # A short description of the mod itself.
description: "Pokemon, but in Borderlands 2. Kinda." # This is set in order to keep the SEO proper
longDescription: "# Setup\n\n1. Download: [Pawn Grenade](https://www.nexusmods.com/borderlands2/mods/234)  \n2. Add the ``Pokelands.blcm`` to the ``PawnGrenade.blcm`` using BLCMM and let it overwrite anything it wants.  \n2b. Tick the ``Offline`` box in BLCMM to change the Hotfix method. For me the normal online one didn't work when tested.  \n2c. Save the changes, you may now close BLCMM.\n3. Add the ``Nasty Suprise`` to your characters inventory, preferably with a low fuse.\n4. In Game, first ``exec PawnGrenade.blcm``, then enable the Pokelands SDK mod.\n5. Thats it.\n![yt](https://www.youtube.com/watch?v=r1H_Z9LRDUU&amp;t)" # Description of what the mod can do
categories: ['Content', 'Gameplay'] # Category of the type of mod

requirements: [] # Requirements for the given mod
requirementTitles: [] # The link-friendly name of the requirements

issues: "https://github.com/juso40/bl2sdk_Mods/issues"
download: "https://github.com/juso40/bl2sdk_Mods/raw/master/Pokelands/Pokelands.zip"
source: "https://github.com/juso40/bl2sdk_Mods/" # Link to source code
license: ['MIT', 'https://choosealicense.com/licenses/mit'] # License name, link about the license from https://choosealicense.com/

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