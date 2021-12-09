<h1 class="white" >Frequent errors you may find</h1>

### I cant use coroutines
This is because you are trying to use them in the Mod class (which is no possible). You have to create a MonoBehaviour class and use it there.

### My MonoBehaviour script is not running!
Remember that in order to use a MonoBehaviour script you have to add it to a GameObject. If you already did it and still doesn't work check when you are creating the GameObject, if you are doing it in the main menu but trying to execute it in-game it probably was destroyed due to the scene change, you can use DontDestroyOnLoad (if you need it in both main menu and the game) or load it later.

### My mod is not working
Right now the game will not warn you if the mod crashed, you will have to manually check the game's log if you suspect that your mod is crashing. The Player.log file is located in "%appdata%/../LocalLow/Viking/My Garage" (you can go with Windows + R).

### Visual Studio can't copy the .dll into the folder.
Close the game, you can't modify the mods (this includes compiling them and trying to overwrite the old version) while the game is running.