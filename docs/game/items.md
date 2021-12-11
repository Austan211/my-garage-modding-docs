<h1 class="white" >Pickable items</h1>

Making an item Pickable is very easy, just adding the MooveItem component to it (and making sure it has no parent by default and a rigidbody) should work!
Small example:

```cs
    // We create our own item but is not pickable yet
    GameObject newTable = GameObject.Instantiate(bundle.LoadAsset<GameObject>("Table"));
    // We make it pickable now!
    newTable.AddComponent<MooveItem>();
```

Easy as that! Now we can just go in-game and pick it with the hand, also you may want to check the properties of the MooveItem class:

```cs
    MooveItem moveItem = newTable.AddComponet<MooveItem>(); // We save the MooveItem instance
    moveItem.price = 1234; // The item price when selling it in the pawn shop.
    moveItem.CanPutInBox = false; // It can't be stored in a box
    moveItem.Collectible = false; // Is only saved if is in the garage. 
```

Also, the last one is an interesting property: IsFurniture - It makes the item use the furniture system of the game (removes the rigidbody after is in place) and also makes it only movable with the move tool.

```cs
    moveItem.IsFurniture = true;
```

Note that this is only for items - Car parts use the Pickup class!