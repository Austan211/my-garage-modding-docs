<h1 class="white" >Weather</h1>

The game uses [Enviro](https://assetstore.unity.com/packages/tools/particles-effects/enviro-sky-and-weather-33963) for handling time and weather, this means that in order to interact with time or weather you just need to get the Enviro instance and do the changes that you need.

Since the instance is static you can just use EnviroSkyMgr.instance for getting it. Here some examples modifying the game a bit:

```cs
EnviroSkyMgr.instance.ChangeSeason(EnviroSeasons.Seasons.Autumn); // Sets the season to Autumn.
EnviroSkyMgr.instance.ChangeSeason(EnviroSeasons.Seasons.Winter); // Sets the season to Winter (it doesn't snow!)

EnviroSky.instance.ChangeWeather(1); // Changes the weather to sunny

EnviroSkyMgr.instance.ChangeWeather(8); // Sets the weather to snowy (but still doesn't snow - you may want to check "The tools class" section)
```

You can find more information in [Enviro docs](http://warlords-destiny.com/Enviro_Documentation.pdf);