<h1 class="white" >ModLoader</h1>

The game includes its own ModLoader so players don't have to go through the process of setting it up. Also the modloader does not add any UI by itself and only adds the logic part for the developers to be able to interact with most of the game.

The ModLoader has two classes, ModLoader and Mod.

Now a detailed list about these two classes (written by Horsey4).
```cs
The ModLoader class
  Fields:
    static List<Mod> mods (List of all mods that are currently loaded, not recommended to touch)
  Methods:
    Mod GetModInstance(string id) (Returns the instance of the mod under the specified id, null if not found or not enabled)
    bool IsModInstalled(string id) (Returns true if the mod under the specified id is installed, otherwise false)
- DO NOT INSTANTIATE
```

```cs
The Mod class
  Properties:
    string Name (Name of the mod, required)
    string ID (ID of the mod, must be unique, required)
    string Author (Author of the mod, required)
    string Version (Version of the mod, required)
    byte[] Icon (Image icon data for the mod, optional)

  Fields:
    bool enabled (If the mod should be executed or not, not recommended to use)

  Methods (all are optional):
    Constructor (Only called once per game session, called before OnMenuLoad, useful to load assets)
    void OnMenuLoad() (Called when the main menu is loaded)
    void SecondPassOnMenuLoad() (Called after OnMenuLoad)
    void MenuUpdate() (Same functionality as unity, only called while in main menu)
    void MenuLateUpdate() (Same functionality as unity, only called while in main menu)
    void MenuFixedUpdate() (Same functionality as unity, only called while in main menu)
    void MenuOnGUI() (Same functionality as unity, only called while in main menu)
    void OnLoad() (Called when the game is loaded using new save or continue)
    void SecondPassOnLoad() (Called after OnLoad)
    void Update() (Same functionality as unity, only called while ingame)
    void LateUpdate() (Same functionality as unity, only called while ingame)
    void FixedUpdate() (Same functionality as unity, only called while ingame)
    void OnGUI() (Same functionality as unity, only called while ingame)
    void Continue() (Called when the game is continued)
    void SecondPassContinue() (Called after Continue)
    void OnSave() (Called when the game is saved)
    void OnBarnSave() (Called when the barn is closed or the game is saving with the barn open. Note that game saves the barn first and then the rest)
    void OnBarnLoad() (Called when the barn is loaded)
```

Some things to remember:
- OnLoad is called before the saving system starts loading the game. For example if you manipulate the player money here it will be overwritten by the saving system.
- Continue is called after the saving system loaded the game but in the same frame, this means that in order to interact with the loaded things you have to wait until the end of the frame ([Unity docs](https://docs.unity3d.com/ScriptReference/WaitForEndOfFrame.html))