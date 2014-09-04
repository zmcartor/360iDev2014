#UIDynamics Talk

### Gravity 
Can control the direction of gravity with vectors. Magnitude and direction. 

In UIDynamics, the animator is an omni-present 'thing' you don't have to start/stop it. It's always there animating everything!

Can create multiple behaviors and add to just one animator! If there are competing behaviors, it will typically warn you :S 

### Dynamic Animator Delegate
There is a delegate callback on the Animator which will be fired when the dynamic animations are complete. Called ``` <UIDynamicAnimatorDelegate> ```

Only two delegate callbacks

``` 
- (void)dynamicAnimatorDidPause:(UIDynamicAnimator *)animator

- (void) dynamicAnimatorWillResume:(UIDynamicAnimator *)animator 

```
These can be used to remove an animation when it's finished; such as a gravity behavior or whichever.

Notice that the gravity behavior never pauses! It's always falling off the screen!

Another way to do things is add a secret floor off the screen and create a collision behavior. When the item collides with the secret wall, remove the behaviors. Remember things can be placed outside of the screen! :D 

Tracking the intersection of the frames also works by placing callback on the 'action' block of the UIDynamicBehavior :

```
 if (!CGRectIntersectsRect(self.authorView.frame, self.view.frame)){
            [self.animator removeBehavior:self.gravity];
            [self.authorView removeFromSuperview];
            NSLog(@"removed!");
        }

```

### Tweaking UIDynamic Behaviors
To tweak various parameters of the dynamic behaviors, we can add multiple generic UIDynamic behaviors that reference whatever we'd like to animate. Gravity + angular falling looks pretty cool. To do that, we add a UIDynamicBehavor, allow rotation and then add an angular momentum vector. Add this UIDynamic behavior to the animator and poof!


### Actions during animation
When animating views and things in/out , it's possible for user to touch the view and interact with things. This might not be what you want! Remember to allow/disallow user interaction while stuff is happening!

#### Within the Action block, place some UIAnimations!
This is a very powerful thing. Check out the project-menu-2 for an example of animating an alpha and removing the overlay view when buttons move off the screen.

### Custom ViewController transitions
UIDynamics can be added to custom viewcontroller transitions. 
Checkout CSIStoriesViewController. Adhere to the protocol 
``` <UIViewControllerTransitioningDelegate> ```

```
CSSettingsViewController *settingsVC = [[CSSettingsViewController alloc] init];
    settingsVC.delegate = self;
    settingsVC.modalPresentationStyle = UIModalPresentationCustom;
    settingsVC.transitioningDelegate = self
    
   ```
Various transition controllers are then provided to provide services for transition in and out of the view. 
Checkout : ```CSPresentSettingsAnimationController ```

Custom ViewControllerTransitions are pretty cool! Check them out, they aren't too hard to figure out.

### Debugging UIDynamics
use DynamicXray framework !
Anywhere you use an animator, add the Xray as a behavior to the animator. Super cool! 
