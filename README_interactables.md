# VRTK Examples - Interactables

[Home](README.md)

## Prerequisites

* You have a basic environment setup. See the scene "Base Scene" for an example.

## Overview: What are interactables, and interactors?

In VRTK 4.0, we have the concept of interactables, and interactors. You would configure an interactor, which would interact with multiple objects (interactables) in the scene. For example, you might have a player's hand, which could pickup a gun, or a pencil.

Currently, this document serves as an overview of what interactables/interactors are. You can see some examples of interactables in this repo, under the `Interactables` scene.

### Interactors

The interactor is typically a child of a tracked alias (eg: TrackedAlias-\>Alias-\>LeftControllerAlias). As the name implies, here we define how the player interacts with the world, and what happens when certain events are triggered. We can define, at a global level, what happens when we...

- Touch an interactable (eg: we touch a button)
- Untouch an interactable (eg: we stop touching a button)
- Grab an interactable (eg: we grab a gun)
- Ungrab an interactable (eg: we let go of a gun)

### Interactables

The interactable is a gameobject that the player can, as you would guess, interact with. In the interactable, we can define...

- What happens when the player grabs the object with both hands? Should the second hand...
	- control the direction of the gameobject? (eg: Moving your non-dominant hand while holding a rifle would change the rifle's direction)
	- control the scale of the gameobject? (eg: Pinching both ends of a cube, and having it expand as you move your hands apart)
	- become the primary hand instead? (eg: Hold an apple in your right hand. Now, grab it with your left. In this case, your right hand would let go, and the left hand would become the primary grabber)
	- do nothing!


We can also configure how the grab action should operate for this object. For example...

- Should the interactor let go of the object on a toggle, or should the interactor let go of the object when the player releases the button? 
- If I were to grab a gun, I would like to hold it by the handle, not by the object's origin. Likewise, if I'm grabbing a box, I might want to pick it up by the point of where I grabbed it.

Note: See the FAQ section on this page to see how to configure these two settings.


## FAQs / Tips and Tricks

### How can I configure the interactor to let go on a toggle, instead of letting go when the player releases the grab button?

This is configured under your interactable. 

Go to `[your interactable]->InteractionLogic->Interactable.GrabLogic->Interactable.GrabReceiver`. You can set the Grab Type field to either "Hold Till Release", or "Toggle".


### How can I configure where the object snaps to when it's grabbed?

This is configured under your interactable. The gameobject names will vary depending on what action type your interactable is using (eg: follow, control direction, swap, etc). 

Go to `[your interactable]->InteractionLogic->Interactable.GrabLogic->Actions->[Primary|Secondary]Action->Interactable.GrabAction.[ActionType]`. Here, you can set the "Grab Offset" field":

- None: Default. Snaps to the origin of the interactable.
- Precision Point: The interactable will follow the point where the player grabs.
- Orientation Handle: Snaps to the transform of the orientation handle, which is a child of this gameobject (`Dependencies->OrientationHandles`). 
	- So, you could have any gameobject as a child of the `OrientationHandles` gameobject, and the interactable will follow that transform.

## See also

[VRTK 4.0 Documentation: Interactions](https://academy.vrtk.io/Documentation/HowToGuides/Interactions)
