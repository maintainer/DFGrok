DFGrok
=========

Generates yUML ( http://yuml.me/ ) code from Objective-C++.  [Download latest build](https://github.com/darkFunction/DFGrok/releases) (OSX)

###Build

Before building project you need to download libclang with headers

`brew install --with-clang --all-targets --rtti --universal --jit llvm`

###Usage 
`dfgrok class1.m class2.m ...`

... or search for all classes in source tree
``dfgrok `find . -name "*.m"` ``

... or to see a visual representation of the changed files between master and dev:
``dfgrok `git diff --name-status dev..master | grep "\.m" | cut -c 3-` ``

... Then copy-paste output into http://yuml.me/diagram/plain/class/draw 


###What's it for?
It just helps you to quickly see class relationships by creating a 'back of napkin' style diagram.  It's useful as a starting point for looking at a bunch of unfamiliar classes or simply as a shared reference for discussion.  [Read more...](http://notes.darkfunction.com/DFGrok)

###Example output 

```
[DFDataModel{bg:orange}]^-[DFDemoDataModelOne{bg:orange}]
[DFDataModel],
[DFDataModel]delegate+->[id\n\<DFDataModelDelegate\>{bg:white}],
[DFDemoDataSource{bg:gray}],
[DFDemoDataSource]dataModelContainer++->[DFDataModelContainer{bg:gray}],
[DFDataModel]^-[DFDemoDataModelTwo{bg:orange}]
[DFDemoController{bg:green}],
[DFDemoController]demoDataSource++->[DFDemoDataSource],
[DFDataModelContainer],
[DFDataModelContainer]delegate+->[id\n\<DFDataModelContainerDelegate\>{bg:white}],
[DFDataModelContainer]dataModels++->*[id\n\<DFDataModelInterface\>{bg:white}],
[id\n\<DFDataModelDelegate\>]^-.-[DFDataModelContainer],
[id\n\<DFDataModelContainerDelegate\>]^-.-[DFDemoDataSource],
[id\n\<DFDataModelInterface\>]^-.-[DFDataModel],
```

![yUML](http://notes.darkfunction.com/images/yuml2.png)

####Key:
![yUML](http://notes.darkfunction.com/images/yumlkey.png)

###What's with the colours?
The idea is to reduce clutter by replacing some classes with colours.  In the example above, any class that inherits from `UIViewController` is green.  This means you can see at a glance what type of entity you are looking at without following the class heirarchy back, and there is no need to add the entity to the diagram.


####Notes for contributors
The code is pretty messy at the moment so I apologise for that- the project is tracer code really for playing with libclang and yUML.
