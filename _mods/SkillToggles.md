---
layout: mod

authors: "Relentless, Chronophylos" # Authors of the mod
title: Skill Toggles # Title of the mod
version: "1.3.1" # Version of the mod
supported: "BL2 + TPS" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Lets you deactivate Action Skills by holding a configurable hotkey." # A short description of the mod itself.
description: "Lets you deactivate Action Skills by holding a configurable hotkey." # This is set in order to keep the SEO proper
longDescription: "Lets you deactivate Action Skills by holding a configurable hotkey.\n\nFeatures:\n- deactivate the Action Skills for each character\n- configurable hotkey\n- options to enable deactivation for class individually\n\nNotes:\n- since this is often not the case with SDK mods: yes, this has multiplayer support if all players have it installed\n- deactivating Action Skills won't give you a cooldown bonus\n  - there are some exceptions in Borderlands TPS where it works\n- in a multiplayer environment, only the host settings of the mod are taken into account\n  - that means only the host can define which Action Skills are deactivatable\n  - you can still use your own hotkey\n- the default toggle key is `F` which also is the default Action Skill hotkey\n  - you need to *hold* they key, not just press it to avoid accidental deactivation\n  - you can change it to anything in the modded keybinds but you can't change it back to `F` because it's already taken by the Action Skill\n  - if you want to use the `F` key again, you need to delete the settings.json file in the mod directory, restart the game and reenable the mod\n  - if you are using another hotkey for the Action Skill, you can also directly edit the modded hotkey in the `settings.json` file while the game is closed\n\nEverything related to versions and their release notes can be found in the [changelog](https://github.com/RLNT/bl2_skilltoggles/blob/main/CHANGELOG.md).\nIf you found a bug or you have a feature request, please use our issue tracker linked below.\nIn case you need support, please join our [Discord](https://discordapp.com/invite/Q3qxws6)." # Description of what the mod can do
categories: ['Utility'] # Category of the type of mod

requirements: ['EridiumLib >= 0.4.1'] # Requirements for the given mod
requirementTitles: ['EridiumLib'] # The link-friendly name of the requirements

issues: "https://github.com/RLNT/bl2_skilltoggles/issues"
download: "https://github.com/RLNT/bl2_skilltoggles/releases/tag/v1.3.1"
source: "https://github.com/RLNT/bl2_skilltoggles" # Link to source code
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