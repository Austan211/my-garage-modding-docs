# The transparents class

Every car part in the game can be attached for something, you just have to pick it up and go to the place where it belongs and a checkmark appears! How the game does know that the item you have belongs there? With an invisible GameObject that has a "transparents" component attached to it (and they share the name GameObject name).

Then the idea is simple for custom car parts, we just need to make our own object that has this component and attach it, easy as that? Well, actually yes and no. If we are just looking for doing something simple like our example spoiler then yes, is easy as that, we just need to add our transparent into the correct place (in this case, the trunk door of LAD) but in some cases like building a car from scratch (Thing that is not supported by SimplePartLoader!) then you will find some hard structures like the Tunnel. We will not get deep in these structures since is not part of the loader.

So how i can add my own transparent using SimplePartLoader? Easy as this:

```cs
Part spoiler = SPL.LoadPart(bundle, "example_spoiler");
spoiler.SetupTransparent("TrunkDoor06", Vector3.zero, Quaternion.identity, Vector3.one);
```

The SetupTransparent function allows us to register internally all the transparents that the SimplePartLoader has to load into the game, the parameters are the following:

1 - (*string*) attachesTo - Name of the part that the will add the transparent to.<br>
2 - (*Vector3*) transparentLocalPos - The local position of the transparent. (Remember that it will be a child of the object that attaches to). This is used for moving the attached part.<br>
3 - (*Quaternion*) transparentLocalRot - The local rotation of the transparent.<br>
4 - (*Vector3*) scale - Optional one, the local scale of the transparent. The default value is Vector3.one<br>
5 - (*bool*) testingModeEnable - Optional one, enables the transparent editor (explained below)<br>

# The transparent editor

SimplePartLoader provides an in-game transparent editor for making things easier to setup for the developers. Note that this is a developer tool and is not intended for final releases (So disable it before releasing your mod!)

To use it just enable the testingModeEnable in the SetupTransparent function of the transparent that you want to modify, go to a new game (using continue may cause issues and FPS drops if it has too many objects with your new transparent) and buy the part that your transparent attaches to or spawn a job car that has it, you will see a white cube appear where your transparent is, this is the transparent preview and you can disable/enable it with **Z**.

The editor works in the following way: It allows you to modify both position and rotation of the object with the numpad. You need first to select the mode (rotation or position, shown at the top-left) with **Numpad 0** and then start moving:

X axis: Press **Numpad 1** for decrease and **Numpad 3** for increase. <br>
Y axis: Press **Numpad 4** for decrease and **Numpad 6** for increase. <br>
Z axis: Press **Numpad 7** for decrease and **Numpad 9** for increase. <br>

There is also a multiplier key which is **Keypad Enter** that will do a bigger increase/decrease while pressed.
You can also do a 90° degrees turn (-90° if the multipier is being pressed) using **Numpad 2** (in X axis), **Numpad 5** (in Y axis) and **Numpad 8** (in Z axis).

You can have your custom car part attached in the transparent while doing the modification but be sure of only attaching it. Bolting it may cause issues.

After you finished you only need to copy the values that are shown in the top-left and set them up in the SetupTransparent function and that's it!