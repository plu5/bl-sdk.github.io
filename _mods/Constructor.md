---
layout: mod

authors: "juso" # Authors of the mod
title: Constructor # Title of the mod
version: "1.0.2" # Version of the mod
supported: "BL2 + TPS" # Supported games; currently can only display as "BL2", "BL2 + TPS", or "TPS"

tagline: "Mod/Ressource that allows the easy creation and use of new non replacing Objects." # A short description of the mod itself.
description: "Mod/Ressource that allows the easy creation and use of new non replacing Objects." # This is set in order to keep the SEO proper
longDescription: "# Constructor V.1.0.2\n[PythonSDK](https://github.com/bl-sdk/PythonSDK) Mod/Ressource that allows the easy creation and use of new non replacing Objects.\n\n## Installation\n1. Download and install [PythonSDK](https://github.com/bl-sdk/PythonSDK)  \n2. Download this mod by downloading the provided `.zip`  \n3. Extract the `.zip` archive into the `/Binaries/Win32/Mods` directory of your game.\n4. To enable the mod go start the game, go to `Mods` menu and press `Enter` on the `Constructor`  \n\n## Installing constructor addons/Non replacing mods\nSimply place the provided files/folders anywhere inside `/Binaries/Win32/Mods/Constructor`.  \nThe names of the files do not really matter, as most mods will add new objects, so they won't overwrite each other and\nshouldn't cause any compatibility issues.  \nIf you do care about load order, the files will be loaded in alphabetical order of their respective directory.\n\n## Using normal text mods alongside of the Constructor\nAs always, use BLCMM to configure your mods and decrease compatibility issues. \nAfter you are done in BLCMM make sure the files extension is `.blcm` and then place the file inside of the `Constructor` directory.  \nIt's basically the same as with constructor addons/Non replacing mods. Load order of the `.blcm` files is again, alphabetically.\nThe `.blcm` mods will then automatically be merged and enabled. \n\n## FAQ\n- Can I use gibbeds Save editor to acquire new objects? \n  - No, all your items will be stored in a `.json` file instead of the `.sav` file the game uses. You can open this `.json` with any text editor and simply give yourself any item you want, but you will need to know the parts object name.\n- Do I need all DLCs to use this mod?\n  - No, you only need the base game. But if you plan on using an addon that uses an DLC item as its base, then you will ofc need the DLC to use this new item.\n- Why does my game crash when I throw a grenade?\n  - This is related to multiple objects having the same name. So you either have a duplicate copy of an addon inside the Constructor directory or one of the addons you use has a bug/duplicate entry.\n- Does this work in coop?\n  - No.\n\n## Getting Addons\n- [Borderlands 2 Reloaded](https://www.nexusmods.com/borderlands2/mods/272) \n adds 20+ new items to the base game, all of which can be farmed from specific sources. Planning on overhauling parts of the vanilla game later on, just wanting to get a beta out. -Created By: SteveKiller568  \n - [TPS Lasers in BL2](https://www.nexusmods.com/borderlands2/mods/281)\n attempts to recreate the Laser weapon category from The Pre-Sequel in BL2.   \n - [MoxxiCard](https://github.com/zondaken/bl2-mods/tree/main/sdk-mods/MoxxiCard)\n   is a simple QoL mod which adds card information to the card about the life steal amount.  \n--------------------------------\n*If you've created a Repo or mod page with your creations message me, and I'll happily add it to this list :)*\n\n### Contact me\n- Discord `juso#6352`\n- Discord servers that can help you:\n  - [Borderlands 2 Modding](https://discord.gg/DK74kjy)\n  - [BL: Exodus](https://discord.gg/tdK5MGK)\n  " # Description of what the mod can do
categories: ['Content', 'Library'] # Category of the type of mod

requirements: [] # Requirements for the given mod
requirementTitles: [] # The link-friendly name of the requirements

issues: "https://github.com/juso40/bl2sdk_Mods/issues"
download: "https://github.com/juso40/bl2sdk_Mods/raw/master/Constructor/Constructor.zip"
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