# UIKit Recipes
github.com/twenty3/Fling-Demo


Dynamic item - doesn't have to be an UIView, or even on screen. Anything that implements this protocol (or can you make it) can be used within dynamics.

Within UIDynamics, the bounding boxes are the things that collide. Not the actual shapes. Howto overcome this ?


Checkout DynamicItem properties. Really tweaking these fields can exert much better fine control over rotation, and others.

Once a DynamicItem has been given to the Animator, messing with the bounds/frame will throw errors.


## PanGesture + AttachmentBehavior

Within the pan gesture recognizer, we keep moving the point on the attachmentBehavior, and update this point.

Put the attachmentPoint wherever the touch actually happened. This prevents 'jumping' under your finger. (or maybe you want that)

Another trick is to attachBehavior at the center of the view, and don't worry about the exact point of touch. Play around with a couple schemes to get the correct feel.


Turning off gravity - when dragging tokens around from the bottom of the screen, we want them to stay put when we let go. 'Transient behaviors' are behaviors we remove whenever the animator pauses. 

#### Flinging things around
Pan gesture velocity should influence behaviors. Luckily, UIPanGesture tracks velocity. ``UIDynamicItem addLinearVelocity``` allows adding velocity behavior to a UIDynamicItem.

Interesting method on animator : ```
updateItemUsingCurrentState:``` allows us to change things after they have been added to the animator.

At each tick of the animator, we can check if the velocity is less than a certain value. If it's super small, that behavior can be removed. Then, we can add a snap behavior to snap it to final place.

## Custom Behaviors

 UIDynamic behaviors are simply 'forces' applied against properties. (bounds, frame, whatever) we can hook this 'forces' upto other properties like size, alpha, or anything! Neat!

Create a fade-in efect
- Class with implements UIDynamicItemProtocol 
- Methods ```bounds``` , ```size``` , ```transform``` are wired into alpha.

Use UIpushBehavior to exert force on the item. This causes force to be exerted on the alpha value. Cool!

