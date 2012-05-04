#Emacs-JAI

An elisp module for creating Java Advanced Imaging DAGs much more quickly

## History

If you've ever hacked on JAI you know that writing self-contained DAGs means
lots of scope and parameters and can be awful.  If you happen to be an Emacs
user this can make your life simpler. 

## Workflow

Load `jai.el` via `M-x load-file` into your emacs environment then call `M-x jai-buildop`.  It will then
enter interactive mode and you should provide the name of the JAI operator
variable you'd
like to create and insert at the current location.  You will then be asked for
the JAI operator which is to be inserted.  For example:

```text
M-x jai-buildop
RenderedOp name: example_adder
JAI Operation: add
```

produces

```java
RenderedOp example_adder; {
  ParameterBlockJAI pb = new ParameterBlockJAI("add");
    pb.addSource();
    pb.addSource();
    example_adder = JAI.create("add", pb);
}
```

Notice what is created:  a variable of type `RenderedOp` called `example_adder`
in the current scope.  In addition, an anonymous scope is created inside of
which a `ParameterBlockJAI` is created with the necessary bits to construct the
operator, and then `example_adder` is actually created with that
`ParameterBlockJAI` so that the current scope is not poluted with the blocks
taking up names, etc.

## Compatibility

I have no idea.  I have tested this under Emacs 21 where it was developed ages
during my awesome graduate years.  It also works under Aquamacs on OSX 10.7.
Since I am struggling to determine if JAI even exists anymore I won't
investigate much further unless there suddenly appears a meaningful user-base
(where meaningful is defined as more than 0, which is the current user-base).
