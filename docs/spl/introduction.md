# What is SimplePartLoader?

This small mod is a way to allow developers to easily add their own custom car parts into the game. It will automatically handle localization, adding most of the components and also saving and loading of the part.

SimplePartLoader is capable of:
- Loading and saving (uses the same loading system as the game)
- Creating transparents in an easy way (for attaching the objects into cars)
- Making a part paintable
- Attachments with nuts, bolts and pry-tool
- Automatically add your part into game's catalog

SimplePartLoader is **not** capable of:
- Complex structures with BoltNut (untested - probably will not work due to missing components)
- Complex transparents structures (using attachables or dependants objects will result in unexpected behaviour)
- Adding new cars into the game
- Saving custom data of parts (Planned feature!)

The mod was developed by Federico Arredondo. Special thanks to BrennFuchS for the caching resources feature and mbdriver for letting me add custom car part support into game's saves loader!

If you have any kind of issue with the loader or want to do any suggestion please use the [issues section in Github](https://github.com/FedeArre/SimplePartLoader/issues)