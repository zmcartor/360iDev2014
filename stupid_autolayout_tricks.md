# Stupid AutoLayout Tricks

checkout http://autolayoutzen.com

### Paint by memory addresses

When printing out constraints, various view will simply be represented like <UIButton 0x23456ae> 

- get memory address, 0x1234aef
- expr (UIView *)0x12345aef backgroundColor = [UIColor redColor];
- continue !

Greatly helps when figuring out which view is causing layout to be ambiguous or unsatisfyable. 

### Name your constraints

Name your constraints! Set an Xcode label on various constraints to disambiguate them. protip! This also works for Xibs and controls. Comment everything to make it much easier to grok.

### _autolayoutTrace

Debugger command. Useful in figuring out it a layout is ambiguous or if something is causing problems.

``` [self.view _autolayoutTrace] ```
This will print out an entire trace. Useful to also use the 'paint by numbers' trick. 

### Restoration Identifiers
 ??? 
 

### _layoutDebuggingIdentifier
Available on iOS8 , this is a private method so no shippy!
To get into private methods, use the selector trick.

``` 
SEL name = NSSelectorFromString(@"_layoutDebuggingIdentifier");
performSelector:name etc ...

```

### QuickLook
Viewing constraints via quicklook. Hitting spacebar will show infoz about it. Possible by overriding the method 

``` - (id)debugQuickLookObject ```

Speaker provides nice little override for this to print out human reps of the constraint.

### Profiling Template
There is a template within instruments for profiling Cocoa Layout stuff.
Displays various constraints and when they are added /removed etc.



