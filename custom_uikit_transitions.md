#Custom UIKit Transitions

By using segues in Storyboards, it's possible to create various types of Segues. That's the easy stuff. When creating your own Segue , there's the option to create a custom segue. 

Of course, use ```prepareForSegue``` to prepare various data between viewControllers. 
Check which segue is triggered by checking the segue identifier. 

When creating immersive experiences , it's nice to hide that pesky navigation bar. However to implement back/forward behavior, keeping everything within a nav controller is reccomended. 

### UIStoryBoardSegue subclass

All the segues are simply subclasses of UIStoryBoardSegue. We can thus create our own subclasses to implement a custom transition. 

From the Apple Docs: 

For custom segues, the main method you need to override is the ```perform``` method. The storyboard runtime calls this method when it is time to perform the visual transition from the view controller in sourceViewController to the view controller in destinationViewController. If you need to initialize any variables in your custom segue subclass, you can also override the ```initWithIdentifier:source:destination:``` method and initialize them in your custom implementation.


###UInavigationControllerDelegate & UIViewControllerAnimatedTransitioning protocols

There's only so far various segues can take you. To really get crazy, there are two protocols that can controls transitions. ```transitionDuration``` and ```animateTransition``` are the workhorses of transitions. A 'transitions context' is passed in which we use to get the "to" and "from" view controllers. 

To support custom UITransitions within navigationControllers, use the UINavigationController delegate method : ```
navigationController:animationControllerForOperation:fromViewController:toViewController:
```
This gives you a chance to provide an animation controller for the transition.
#### NOTE
When using AutoLayout + Custom transitions , be sure to call ```[transitionContext containerView] layoutIfNeeded]``` to ensure layout and constraints are current before animating or doing any other layout operations which depend on the current layout!



