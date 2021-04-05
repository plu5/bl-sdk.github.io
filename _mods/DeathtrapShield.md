---
layout: mod

authors: "Relentless" # Authors of the mod
title: Deathtrap Shield # Title of the mod
version: "1.1.0" # Version of the mod
supported: "BL2" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Gives Deathtrap its own configurable shield from the inventory of Gaige." # A short description of the mod itself.
description: "Gives Deathtrap its own configurable shield from the inventory of Gaige." # This is set in order to keep the SEO proper
longDescription: "Gives Deathtrap its own configurable shield from the inventory of Gaige.\n\nFeatures:\n- Deathtrap can use its own shield and no longer shares the shield with Gaige\n- you can define which shield to use in the inventory\n- configurable hotkey\n\nNotes:\n- since this is often not the case with SDK mods: yes, this has multiplayer support\n- the default behaviour of the skill applies and the shield of Gaige will be shared when:\n  - you don't set a Deathtrap shield\n  - you equip the Deathtrap shield to Gaige\n- the Deathtrap shield will lose its status when:\n  - you set a new Deathtrap shield while already having one\n  - you equip the Deathtrap shield to Gaige\n  - you throw the Deathtrap shield on the ground\n  - another character that is not a Mechromancer puts it in their inventory\n- other useful information:\n  - this only works if you unlocked the `Sharing is Caring` skill\n  - you can only set one Deathtrap shield at a time\n  - you can't set a Deathtrap shield as trash or favorite (unset it first)\n  - the Deathtrap shield will have another color\n- the hotkey to set the Deathtrap shield can be modified in the modded keybinds\n- if you have a Deathtrap shield set, you won't be able to edit your save game in the SaveGame Editor unless you rejoin the game and remove the shield status, this can't be fixed\n\nEverything related to versions and their release notes can be found in the [changelog](https://github.com/RLNT/bl2_deathtrapshield/blob/main/CHANGELOG.md).\nIf you found a bug or you have a feature request, please use our issue tracker linked below.\nIn case you need support, please join our [Discord](https://discordapp.com/invite/Q3qxws6)." # Description of what the mod can do
categories: ['Utility'] # Category of the type of mod

requirements: ['EridiumLib >= 0.4.1'] # Requirements for the given mod
requirementTitles: ['EridiumLib'] # The link-friendly name of the requirements

issues: "https://github.com/RLNT/bl2_deathtrapshield/issues"
download: "https://github.com/RLNT/bl2_deathtrapshield/releases/tag/v1.1.0"
source: "https://github.com/RLNT/bl2_deathtrapshield" # Link to source code
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