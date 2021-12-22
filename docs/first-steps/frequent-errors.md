<h1 class="white" >Frequent errors you may find</h1>

### I cant use coroutines
This is because you are trying to use them in the Mod class (which is no possible). You have to create a MonoBehaviour class and use it there.

### My MonoBehaviour script is not running!
Remember that in order to use a MonoBehaviour script you have to add it to a GameObject. If you already did it and still doesn't work check when you are creating the GameObject, if you are doing it in the main menu but trying to execute it in-game it probably was destroyed due to the scene change, you can use DontDestroyOnLoad (if you need it in both main menu and the game) or load it later.

### My mod is not working
Right now the game will not warn you if the mod crashed, you will have to manually check the game's log if you suspect that your mod is crashing. The Player.log file is located in "%appdata%/../LocalLow/Viking/My Garage" (you can go with Windows + R).

### Visual Studio can't copy the .dll into the folder.
Close the game, you can't modify the mods (this includes compiling them and trying to overwrite the old version) while the game is running.

### I'm not able to fix X issue, what can i do?
If using Google did not help you to fix your issue we don't have any issue to check on it on the coding channel in the official Discord server of My Garage.

# SimplePartLoader

### My car part falls through the ground
Add a Mesh Collider to it and make sure that "Convex" is ticked (and trigger is not ticked).

### My car part rotates weirdly after attaching it
The car part was not exported correctly into Unity. For a Blender guide on how to export properly [follow this guide](https://all3dp.com/2/blender-to-unity-how-to-import-blender-models-in-unity/).

### My car part is doing weird things after saving
Make sure the PrefabName is unique (don't use something simple, try to use something like the name of your mod + the name part for example). If you think this is a SimplePartLoader / game issue please contact me through Discord (Fede#0005).

### My paintable part does not work
Make sure the material that you are attaching is an Albedo, the rendering mode is Opaque and you selected the correct material index in code.

### I can't pick up my part
Make sure the part is only an object (is not composed by a group of objects), does not have parent and the collider is a Mesh collider (The only supported type is this one, others will not work)

### My part does not appear on the catalog!
Make sure that you didn't tick the "Dont show on catalog" option of the Partinfo, if is not ticked the mod may be crashing due to something so you may refer to the log to see what's happening. If you did anything wrong your mod will be disabled and SimplePartLoader will tell you what caused the error.