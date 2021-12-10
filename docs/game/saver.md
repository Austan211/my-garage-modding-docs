<h1 class="white" >The saving system</h1>

IMPORTANT! This section only explains the issue with the save system and modding - It does not explain how it works internally (Altough is very easy).

The save system in the game works very well, is capable of saving all the game parts and also rust, dirt and paint. Also there is the barn save which is basically a copy and paste of the same system but adapted for the barn. Let's dig a bit into the code.

```cs
    // Saver class - Save function
    foreach (Transform transform in UnityEngine.Object.FindObjectsOfType<Transform>())
	{
		if (transform.name == "Player")
		{
			saveSystem.add("PlayerPosition", transform.position);
			saveSystem.add("PlayerRotation", transform.rotation);
			saveSystem.add("PlayerStarted", transform.GetComponent<tools>().Started);
			saveSystem.add("snowAmount", transform.GetComponent<tools>().snowAmount);
			saveSystem.add("day", EnviroSkyMgr.instance.Time.Days);
		}
		saveSystem.add("Money", tools.money);
		saveSystem.add("SavedVersion", Application.version.ToString());
		if (transform.gameObject.GetComponent<SavePosition>() && transform.position.y > 10f)
		{
			saveSystem.add("PropPosition" + transform.gameObject.GetComponent<SavePosition>().SceneNumber.ToString(), transform.localPosition);
			if (!transform.gameObject.GetComponent<SavePosition>().DontSaveRotation)
			{
				saveSystem.add("PropRotation" + transform.gameObject.GetComponent<SavePosition>().SceneNumber.ToString(), transform.localRotation);
			}
		}
    // And continues...
```

As this snippet shows the save system loops through all the GameObjects in the game, this means everything is getting saved, so far so good. Also we can see the SavePosition component which basically tells the game to save the position of that (This component is only used in some specific objects like tools in the game, the car parts are different). So apparently the game can load our modded things without an issue? Sadly is not the case and this is why.

```cs
    // Saver class - Load function
    if ((int)this.save.get("Objects", 0) > 0)
	{
		this.ObjectNumber = (int)this.save.get("Objects", 0);
		for (int j = 0; j < (int)this.save.get("Objects", 0); j++)
		{
			if ((string)this.save.get("ObjectNr" + this.ObjectNumber.ToString(), "") != "" && Resources.Load((string)this.save.get("ObjectNr" + this.ObjectNumber.ToString(), "")) != null)
			{
				GameObject gameObject = UnityEngine.Object.Instantiate<GameObject>(Resources.Load((string)this.save.get("ObjectNr" + this.ObjectNumber.ToString(), "")) as GameObject);
    // And continues...
```
You might already see the issue, but i will explain this in detail. The game has every object that uses as a prefab and the loader is just there to instantiate them, this has the advantage of being efficent since it reduces the amount of information that the save system has to save and load but also adds two problems for the modders:
- We cannot use this system since the loading of the prefabs is done through Resources.Load (and is not possible to add assets there in runtime).
- Even if we get a way to add our own assets into the game Resources we cannot add the game's components into our own injected prefab.

That's why doing any mods that require some complex saving (like a car part) is very hard to achieve, but is not impossible at least!