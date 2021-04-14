---
layout: main
title: FAQ
permalink: /faq/
---

If you have a question that is not answered here, you can search on [Discord](https://discord.gg/VJXtHvh), and if you do not find it, ask there.

**Page Contents**
* TOC
{:toc}

<hr/>

# User FAQ
## How to start using PythonSDK mods?
Follow the steps described on [the main page]({{ site.baseurl }}{% link index.md %}).

## Can I use PythonSDK mods with text mods?
Yes. Usual compatibility concerns still apply, like if several mods change the same variables they will interfere with each other. This is the case regardless of whether the mods are PythonSDK mods or text mods.

## What is the difference between PythonSDK mods and text mods?
Text mods can only modify objects once; when run. PythonSDK mods can modify dynamically generated objects and run arbitrary game functions whenever they please.

## Why do I not see Mods menu after installation?
- Ensure you have all the required files; your `Binaries/Win32` folder should have `ddraw.dll`, `pythonXX.dll`, `pythonXX.zip`, and the `Mods` subfolder. The `Mods` subfolder should contain an `__init__.py` and the various mods folders (most importantly `ModMenu`) which should each also have an `__init__.py`.
- To be certain, download [latest](https://github.com/bl-sdk/PythonSDK/releases) again and extract and overwrite the files. [Video demonstration](https://www.youtube.com/watch?v=nvTYjFjQ-HI).
- Ensure you have [Microsoft Visual C++ Redistributable](https://aka.ms/vs/16/release/vc_redist.x86.exe) installed.
- Console output or the contents of `python-sdk.log` in your `Binaries/Win32` folder may contain clues as to what went wrong.

If you are on Linux: PythonSDK does not yet work natively on Linux, but it seems to work well under SteamPlay/Proton and Wine. See [The README section on Linux](https://github.com/bl-sdk/PythonSDK#linux-steamplayproton-and-wine).

## Why does my game crash/freeze?
If you are running a mod or modpack that modifies skills (such as Skill Randomizer, Exodus), it will crash if you try to make a new character with those mods enabled. First make the new character, then enable those mods.

If that is not your situation, try to narrow down the mod that causes the issue by disabling all other mods and restarting to see if it still happens, and when you find the culprit: contact the mod author, if it’s a large modpack they may have a discord server you can ask on, or create an issue on their mod’s repository if there is one.

<hr/>

# Developer FAQ
## How do I create a new mod?
1. Create a new folder in the Mods folder
2. Create an `__init__.py` within it with the following basic template:
   ```python
   import unrealsdk
   from Mods import ModMenu
   
   class MyMod(ModMenu.SDKMod):
       Name: str = "My Mod Name"
       Author: str = "My Name"
       Description: str = "My Mod Description"
       Version: str = "1.0.0"
       SupportedGames: ModMenu.Game = ModMenu.Game.BL2 | ModMenu.Game.TPS  # Either BL2 or TPS, or both with | in between
       Types: ModMenu.ModTypes = ModMenu.ModTypes.Utility  # One of Utility, Content, Gameplay, Library, or several with | in between
       
   instance = MyMod()
   
   ModMenu.RegisterMod(instance)
   ```
3. Launch the game. Your mod should now appear in the mod manager. If it doesn’t, console output / contents of `python-sdk.log` (which can be found in your `Win32` folder, one folder up from the Mods folder) should give a clue as to why.

## How to reload my mod without having to restart the game?
Add the following to your `__init__.py` **before** RegisterMod is called:
```python
if __name__ == "__main__":
    unrealsdk.Log(f"[{instance.Name}] Manually loaded")
    for mod in ModMenu.Mods:
        if mod.Name == instance.Name:
            if mod.IsEnabled:
                mod.Disable()
            ModMenu.Mods.remove(mod)
            unrealsdk.Log(f"[{instance.Name}] Removed last instance")

            # Fixes inspect.getfile()
            instance.__class__.__module__ = mod.__class__.__module__
            break
```
Now you should be able to reload your mod by running `pyexec ModFolderName/__init__.py` (change ModFolderName to the name of the folder your mod is in).

Note that this code snippet is a workaround more than anything, and could break in certain situations. Restarting your mod like this is not the same as restarting the game, as it does not restart game state, so it will not be a clean slate and your mod could potentially behave differently than if you were to restart.

## How to make my mod do things when it’s enabled?
Override the `Enable` instance method, e.g.:

```python
class MyMod(ModMenu.SDKMod):
    ...
    def Enable(self) -> None:
        super.Enable()
        unrealsdk.Log("I ARISE!")
```
`super.Enable()` calls the base class `Enable` method, which registers any hooks or network methods, so you should call that first.

`Log` will log a message to the console. Now when you launch the game and enable your mod you should see "I ARISE!" in the console output. Replace that with whatever you want to do upon enable.

Cleanup functionality can go in the `Disable` instance method:

```python
    ...
    def Disable(self) -> None:
        unrealsdk.Log("I sleep.")
        super.Disable()
```
`super.Disable()` calls the base class `Disable` method, which removes any hooks or network methods.

Now when you disable your mod you should see "I sleep." in the console output. Replace that with whatever you want to do upon disable.

A good practice is to restore anything you’ve changed back to what it was in the `Disable` method.

For other functions you can override, check the `SDKMod` base class, defined in `ModMenu/ModObjects.py` in the Mods folder.

## How to save enabled state?
`SaveEnabledState` allows you to indicate whether your mod should be automatically enabled on subsequent runs if the user enabled it.

Values it can be set to:
* `NotSaved`: The enabled state is not saved.
* `LoadWithSettings`: The enabled state is saved, and the mod is enabled when the mod settings are loaded.
* `LoadOnMainMenu`: The enabled state is saved, and the mod is enabled upon reaching the main menu - after hotfixes are all setup and all the normal packages are loaded.

For example, to set it to `LoadWithSettings` add the following class variable to your mod class:
```python
SaveEnabledState: ModMenu.EnabledSaveType = ModMenu.EnabledSaveType.LoadWithSettings
```
This will save your mod’s enabled state in settings.json, and the mod will be enabled when the mod settings are loaded.

## How to add options to the options menu?
Instantiate your options and add them to the `Options` instance variable of your mod class.

See `ModMenu/Options.py` for available option classes you can use.

Here is an example for adding a `Boolean` option:
```python
class MyMod(ModMenu.SDKMod):
    ...
    def __init__(self) -> None:
        super().__init__()

        self.MyBoolean = ModMenu.Options.Boolean(
            Caption="Set My Boolean",
            Description="Whether My Boolean should be on.",
            StartingValue=True,
            Choices=["No", "Yes"]  # False, True
        )

        self.Options = [
            self.MyBoolean,
        ]
```

This `Boolean` should now appear in the options menu, under the name of your mod (provided the mod is enabled). You can get the value from it by accessing `self.MyBoolean.CurrentValue`, which, since it’s a boolean, will be True or False.

To handle changes to this value in real time, you can override the method `ModOptionChanged`. For example:

```python
    ...
    def ModOptionChanged(self, option: ModMenu.Options.Base, new_value) -> None:
        if option == self.MyBoolean:
            if new_value:
                unrealsdk.Log("You turned on My Boolean")
            else:
                unrealsdk.Log("You turned off My Boolean")
```

Note that this function is called before the change to CurrentValue occurred, so we check `new_value` and not `self.MyBoolean.CurrentValue`.

Also note that for backwards-compatibility reasons, upon enable of your mod this function will be called for every option that is not in a `Nested`. Do not rely on this functionality, as it may be removed in future. Logic addressing settings values on startup should be placed in the `Enable` method instead.

You can change the values of options programmatically, but make sure to call `ModMenu.SaveModSettings(mod: ModObjects.SDKMod)` afterwards (passing an instance of your mod, or `self` if called from within your mod class) or the new values will not be updated in the mod’s `settings.json`.

## How to add game keybinds?
See `ModMenu/KeybindManager.py`.

Instantiate your keybinds and add them to the `Keybinds` instance variable of your mod class.

Here is an example:

```python
...
def sayHi() -> None:
    unrealsdk.Log("hi")

class MyMod(ModMenu.SDKMod):
    ...
    Keybinds = [
        ModMenu.Keybind("Say hi", "F3", OnPress=sayHi),
    ]
```

Now "hi" will be outputted to the console whenever F3 is pressed while ingame.

Any bindings can be customised by the user in Options > Keyboard / Mouse > Modded Key Bindings.

If the function you give `OnPress` takes an argument, it will be passed a `ModMenu.InputEvent` enum with the input event type, which can be `Pressed` (0), `Released` (1), `Repeat` (2), `DoubleClick` (3), or `Axis` (4). This allows you to perform different actions depending on the input type, which you can use, for instance, to do something while a button is held by watching for `Pressed` and `Released`.

Alternatively, there is also the `ModMenu.SDKMod` method `GameInputPressed(self, bind: ModMenu.Keybind, event: ModMenu.InputEvent)` which you can override. It will be called when any key event is performed on one of the mod’s `Keybinds`. Instead of passing an `OnPress` method when you define the `Keybind`, you can perform the associated action in this method instead.

```python
...
class MyMod(ModMenu.SDKMod):
    ...

    HiBind = ModMenu.Keybind("Say hi", "F3")

    Keybinds = [
        HiBind,
    ]

    def GameInputPressed(self, bind: ModMenu.Keybind, event: ModMenu.InputEvent) -> None:
        if bind == self.HiBind and event == ModMenu.InputEvent.Pressed:
            unrealsdk.Log("hi")
```

## How to add mod manager keybinds?
You can have bindings the mod performs when a key is pressed in the mods menu, just like the default `Enable` by pressing `Enter`, by modifying `SettingsInput` instance variable of your mod class. This is a dictionary mapping `key`: `action`, where both are `str`. Handle the different actions by overriding `SettingsInputPressed`. See the `SDKMod` base class in `ModMenu/ModObjects.py`.

Here is an example:

```python
def sayHi() -> None:
    unrealsdk.Log("hi")

class MyMod(ModMenu.SDKMod):
    ...
    SettingsInputs = ModMenu.SDKMod.SettingsInputs
    SettingsInputs["H"] = "Say hi"
    
    def SettingsInputPressed(self, action: str) -> None:
        if action == "Say hi":
            sayHi()
        else:
            super().SettingsInputPressed(action)
```

Now "hi" will be outputted to the console whenever H is pressed while the mod is selected in the mod manager.

## How to hook into game functions?
You can use the `@Hook` decorator. PythonSDK will handle the registering and removing of hooks itself, so long as you remember to call the base class Enable/Disable if you override those methods.

The function you hook must have the signature:
`([self,] caller: unrealsdk.UObject, function: unrealsdk.UFunction, params: unrealsdk.FStruct)`

Example:

```python
class MyMod(ModMenu.SDKMod):
    ...
    @ModMenu.Hook("WillowGame.WillowPlayerController.SpawningProcessComplete")
    def onSpawn(self, caller: unrealsdk.UObject, function: unrealsdk.UFunction, params: unrealsdk.FStruct) -> bool:
        unrealsdk.Log("onSpawn called")
        return True
```

If you do not return True the function you hooked into will not continue executing as normal, which is sometimes desired, but if you do not want that remember to return True. If I forget return True in this case, I spawn in a weird place, don’t have any money, eridium, or anything in my inventory, among other things, because we diverted the logic ordinarily handling all that.

Alternatively, it is also possible to register hooks manually with `unrealsdk.RunHook(funcName: str, hookName: str, funcHook: object)`, where
* `funcName`: a string of the game function to hook, 
* `hookName`: a name it can be referenced by when you remove it, 
* `funcHook`: the function you want to have called,

*or* `unrealsdk.RegisterHook(..)` (same arguments), 

and remove them with `unrealsdk.RemoveHook(funcName: str, hookName: str)`.

It is preferrable to use `RunHook` over `RegisterHook`, since the former ensures the hook is not registered twice.

## How to know what game objects to modify?
* Look through decompiled UPKs, as explained in [the Writing SDK Mods section on the main page]({{ site.baseurl }}{% link index.md %}#writing-sdk-mods)
* Look through objects in BLCM Object Explorer, and other tools described in [BLCM wiki](https://github.com/BLCM/BLCMods/wiki)
* Look at the source of [existing PythonSDK mods]({{ site.baseurl }}{% link mods.md %})
* Even source of text mods can help, as they can tell you what objects you can modify.

You can discuss what you’re trying to do on the [Discord](https://discord.gg/VJXtHvh), and maybe people will chime in to help.

## How to access the objects I want to modify?
The following unrealsdk functions may be of use:
* <b>`unrealsdk.FindAll(ClassName: str)`:</b> Returns a list of `unrealsdk.UObject`s found, or raises RuntimeError if none found.
* <b>`unrealsdk.FindClass(ClassName: str[, Lookup: bool = false])`:</b> Returns a `unrealsdk.UClass`, or `None` if not found.
* <b>`unrealsdk.FindObject(ClassName: str, ObjectFullName: str)`:</b> Returns a `unrealsdk.UObject`, or `None` if not found.
* <b>`unrealsdk.FindObject(Class: unrealsdk.UClass, ObjectFullName: str)`:</b> Returns a `unrealsdk.UObject`, or `None` if not found.
* <b>`unrealsdk.GetEngine()`:</b> Returns a `unrealsdk.UObject` `WillowGameEngine`. This is often used to get our player’s `PlayerController`, which can be done like this: `unrealsdk.GetEngine().GamePlayers[0].Actor`. In UE Explorer, see both `WillowGameEngine` from `WillowGame.upk` and `Engine` from `Engine.upk` for other things you can do with it.

To explore these functions you can run them in the console like `py unrealsdk.Log(unrealsdk.FindAll("WillowPlayerPawn"))` and see what you get.

You will notice what you get can depend on the context, like the function above will have a different `WillowPlayerPawn` instance in the second position in the list depending on the character class you have selected. Also, while on the menu on your own, you just see the two instances (the default instance and your pawn), whereas while ingame with other players, you will also see other instances on that list.

**On `ClassName` and `ObjectFullName`:**
* In BLCM Object Explorer, objects are presented like `GlobalsDefinition'GD_Globals.General.Globals'`. The part outside of the quote marks (`GlobalsDefinition`) is the `ClassName`, and the part inside of the quote marks (`GD_Globals.General.Globals`) is the `ObjectFullName`.
* In UE Explorer you cannot see instances, just classes, but it allows you to see class definitions which can let you see how the game gets the instance you are interested in rather than getting it by name. More on that later.
* In the `FindAll` Log output, for each item on the list the part before the space is the `ClassName`, and the part after the space is the `ObjectFullName`.

**On `FindAll`:**

`FindAll` is useful for exploring, but generally should only be used in code when you have to, as if you are only after a specific object there are better, and less costly performance-wise, ways to get it. Cases where you may want to use it are, for instance, iterating over all objects of a certain class, like changing a property or calling a function on all `WillowPlayerController`s. In that case you may want to note that the first result of `FindAll` is usually the default instance, in this case `WillowGame.Default__WillowPlayerController`, and skip that one.

Example snippet from apple’s [Crowd Control](https://bl-sdk.github.io/mods/BorderlandsCrowdControl/) Kill Players effect:

```python
    for controller in unrealsdk.FindAll("WillowPlayerController"):
        if controller.Name.startswith("Default__"):
            continue
        controller.CausePlayerDeath(True)
```

**For getting a specific object, if you know its class and full name,** you can get it like this: `unrealsdk.FindObject("GlobalsDefinition", "GD_Globals.General.Globals")`.

**Getting a specific object by looking at the way the game gets it:**

For example, let’s say you are interested in `MissionTracker`, which you found while exploring `WillowGame.upk` in UE Explorer.
1. Press Ctrl+Shift+F to search in all classes for references to this object. In many places we see it being accessed with the following: `WillowGameReplicationInfo(WorldInfo.GRI).MissionTracker`.
2. In `Engine.upk`, you can see the `Engine` class has a function `GetCurrentWorldInfo()`.
3. So, let’s try to do `unrealsdk.GetEngine().GetCurrentWorldInfo().GRI.MissionTracker`. You can try `py unrealsdk.Log(unrealsdk.GetEngine().GetCurrentWorldInfo().GRI.MissionTracker)` in the console and see what you get.

This is the way by which the mod [Mission Selector](https://bl-sdk.github.io/mods/MissionSelector/) gets the `MissionTracker`, which it uses to get and set active missions.

## How to publish my mod?
Upload your mod(s) to a public repository, then to add it to this site follow the steps on [the Adding to the Database section on the main page]({{ site.baseurl }}{% link index.md %}#adding-to-the-database).

Note that you should not commit `settings.json` file nor `__pycache__`, as they are automatically generated.
