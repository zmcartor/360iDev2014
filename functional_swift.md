#Functional Swift


## Quick Currying with CImage Filters
With Core Image, you can create a filter, and then apply that to a pic.

imagine there is a Filter which takes in CImage and produces a CImage

``` typealias Filter CIImage -> CImage ```

Function could be created which takes in a radius, and constructs a Filter which is curried with our radius param. Function returns a function!

A color generator could be created which takes a color, and returns a Filter which applies that color to an image. Function returns a curried function!

Funcs that return funcs can be called like functionThatReturnsFunc(input)(to_func)

Nesting a bunch of params almost makes things look like Lisp haha.

## Create a custom operator!

Custom operator called '|>' which combines various filters into one. This is called a 'function composition operator' 

``` let myFilter = blur(image) |> applyColor(red)```

myFilter() now will apply both a blur and color it red when called. neato!

## 

OOP is all about telling computer howto do. Functional is about describing what you want. Is that almost declarative ?

slides at: http://speakerdeck.com/chriseidhof


