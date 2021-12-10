Some Unity functions (mostly any Find operation) is expensive and slow to do, you should really try to evade using these when possible.
Let's take for example this code:

```cs
    void Update() // Update function - called once per frame
    {
        GameObject.Find("Player").GetComponent<tools>.GoGarage();
        if(GameObject.Find("Player").GetComponent<tools>.LOG)
        {
            GameObject.Find("Player").GetComponent<tools>.LOG = false;
        }
    }
```

This code compiles without any issue and even works in-game, but is not efficent! We are getting the same GameObject and the same components three times per frame. Now just imagine this:

- The game runs at 60FPS
- We have 3 find operations and 3 GetComponent operation
- This means that per second we have 180 finds and 180 GetComponent
- In one minute you did 10800 finds and 10800 Getcomponent

Now let's see the following code which does exactly the same!

```cs
    tools toolsInstance;

    void Start() // Start function - called one frame before Update
    {
        toolsInstance = GameObject.Find("Player").GetComponent<tools>();
    }

    void Update() // Update function - called once per frame
    {
        toolsInstance..GoGarage();
        if(toolsInstance.LOG)
        {
            toolsInstance.LOG = false;
        }
    }
```

This code does the same but it only does 1 find and 1 GetComponent, more efficent than the previous one!
Since we know that the Player object does not change in the playthrough (also the tools instance doesn't change) this is the best way for doing this.