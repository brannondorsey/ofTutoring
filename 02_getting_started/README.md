#Week 2

##openFrameworks code structure

Each openFrameworks project comes with lots of files and folders:

- `openFrameworks-Info.plist`
- `src/` <---
- `openFrameworks/`
- `addons/`
- `frameworks/`
- `appDebug.app`

The actual coding takes place in the `src/` directory. Any new openFrameworks app consists of three files in this `src/` directory.

- `ofMain.cpp`
- `testApp.cpp`
- `testApp.h`

###ofMain.cpp

This is the main C++ file that is run when the app launches. Most programming languages use a `main()` function to execute code on launch. Most of the code in this file can be left alone. The main thing that it is used for is setting the __width and height of the app__ as well as setting the app to open in __fullscreen__.

```c++
#include "ofMain.h"
#include "testApp.h"

//========================================================================
int main( ){

	ofSetupOpenGL(1024,768, OF_WINDOW);			// <-------- setup the GL context

	// this kicks off the running of my app
	// can be OF_WINDOW or OF_FULLSCREEN
	// pass in width and height too:
	ofRunApp( new testApp());

}
```

### testApp.h

Contains the function and event prototypes for the app. More [below](#.h-and.cpp).

```c++
#pragma once

#include "ofMain.h"

class testApp : public ofBaseApp{
	public:
		void setup();
		void update();
		void draw();
		
		void keyPressed(int key);
		void keyReleased(int key);
		void mouseMoved(int x, int y);
		void mouseDragged(int x, int y, int button);
		void mousePressed(int x, int y, int button);
		void mouseReleased(int x, int y, int button);
		void windowResized(int w, int h);
		void dragEvent(ofDragInfo dragInfo);
		void gotMessage(ofMessage msg);
};
```

### testApp.cpp

The actual code writing occurs in this file. Here you define the logical procedures that actually take place when your app is running. 

```c++
#include "testApp.h"

//--------------------------------------------------------------
void testApp::setup(){
	//called when the app starts
}

//--------------------------------------------------------------
void testApp::update(){
	//called once per frame before draw
}

//--------------------------------------------------------------
void testApp::draw(){
	//called once per frame after update
}



//--------------------------------------------------------------
void testApp::keyPressed(int key){
	//called whenever a key is pressed
}

//--------------------------------------------------------------
void testApp::keyReleased(int key){
	//called whenever a key is released
}

etc...
```

##.h and .cpp

`.h` stands for __header__

`.cpp` stands for __C++__

In C++ every class must needs to have two files. The first is the __header__ file, which lists the class, property, and method prototypes. 
Think of it like an outline, or a list of ingredients for the class. 

- Any preprocessor statements there to prevent multiple header definitions
- Any include statements to other classes
- Any class extension statements
- Any variables local to the class
- Prototypes of any functions to be contained in the class
- And the security settings of these functions and variables (e.g. public, private, protected, etc).
- and a body file (.cpp) which is like the instructions on what to do with the ingredients and contains:

An include statement that references the .h file
All of the code to fill in the function prototypes.

## Setup, update, draw, and event functions

###Setup
The code inside `void testApp::setup()` is run once at the start of the program. Here is where you will put all of your settings functions for things like frame rate, anti-aliasing, stroke size, etc... As well as instantiating an assigning values to initial variables.

###Update
`void testApp::update()` is called (executed) once per frame __before__ `draw()`. Put all of the calculations/variable updates that occur every frame in here. 

###Draw
`void testApp::draw()` is called once per frame __after__ `update()`. It is reserved for code that handles actually drawing to the screen, also called rendering, only.

###Events

Unlike `setup()`, which is called only once when the app launches, and `update()` and `draw()` which are both called once per frame, each of the 9 basic event functions included in `testApp.cpp` are called only when that even is triggered. For instance, the code inside of `void testApp::mousePressed(int x, int y, int button)` is called as soon as the user presses the mouse.

Here is a list of all 9 basic event functions:

- `void keyPressed(int key);`
- `void keyReleased(int key);`
- `void mouseMoved(int x, int y);`
- `void mouseDragged(int x, int y, int button);`
- `void mousePressed(int x, int y, int button);`
- `void mouseReleased(int x, int y, int button);`
- `void windowResized(int w, int h);`
- `void dragEvent(ofDragInfo dragInfo);`
- `void gotMessage(ofMessage msg);`

##Variables and their types

C++ is strongly typed which means that variables types must be declared. Variable __decleration__ looks like this:

`int x;`

A variable is assigned, or __initialized__, when it is given a value;

`x = 10;`

Both variable __declaration__ and __initialization__ can occur on the same line like this:

`int x = 10;`

###Basic variable types

- `int`
- `float`
- `char`
- `string`
- `vector`

####Int
An `int` stores any whole number like `1`, `5`, or `5986`

####float
A `float` stores any floating point number. Basically any number with a decimal: `1.01`, `56.9`, `789.00645`.

####char
A `char` (pronounced like car) holds any single 8-bit ASCII character. Chars in code are wrapped in single quotes. 

`'h'`, `'t'`, and `'9'` are examples of chars. Like `'9'` illustrates, a char can be a representation of any single character, including numbers, as long as it is surrounded by single quotes.

####string
A string is an ordered list of chars. Strings are used to represent words, or any set of more than one char. Unlike chars, strings are wrapped in double quotes. `"house"`, `"hot dog"`, and `"h8ers"` are examples of strings.


###Other variable types
####vector
A c++ vector is a type of container (like an array) that allows the storage of multiple elements (numbers, strings, objects, etc...) in one variable.

####Custom classes
Any custom classes that you make, and all preset openFrameworks classes like `ofRectangle` (or the 100s more openFrameworks classes), become their own variable types.

##Variable Scope
A Variable's scope refers to the place in a program where that variable can be accessed or manipulated (read or changed). 

There are two main types of variable scope:

- global scope - the variable can be accessed from anywhere in the program.
- local scope - the variable can be accessed only inside of the function where it exists.

###Global variables

In openFrameworks global variables can be used anywhere in the program once they have been declared and initialized. To use a global variable, it must be declared in the `testApp.h` header file. That looks like this:

```c++
class testApp : public ofBaseApp{
	
	public:
		int myVar; //global variable

	public:
		void setup();
		void update();
		void draw();
		
		void keyPressed(int key);
		etc...
};
```
`myVar` can now be used in the `testApp.cpp` file.

```c++
#include "testApp.h"

//--------------------------------------------------------------
void testApp::setup(){
	myVar = 0; // initialize myVar
}

//--------------------------------------------------------------
void testApp::update()
	myVar = myVar + 10; // increment myVar by 10 each frame
	cout<<myVar<<endl; // print the value of myVar to the console
}
```

It is important to notice that because `myVar` is a global variable it can be used in both the `setup()` and `update()` functions.

###Local variables
Local variables exist only inside of the function where they were declared. They are faster to write because you don't need to include them in any `.h` files, but they can't be used inside of other functions.

```c++
#include "testApp.h"

//--------------------------------------------------------------
void testApp::setup(){

}

//--------------------------------------------------------------
void testApp::update(){
	int myVar = 0; // initialize myVar
	myVar = myVar + 10; // increment myVar by 10 
	cout<<myVar<<endl; // print the value of myVar to the console
}
```

In this situation, the value printed to the console will always be 10 because this local variable must be re-assigned (initialized) each frame. The above program is functionally equivalent to: 

```c++
#include "testApp.h"

//--------------------------------------------------------------
void testApp::setup(){

}

//--------------------------------------------------------------
void testApp::update(){
	int myVar = 10; // initialize myVar
	cout<<myVar<<endl; // print the value of myVar to the console
}
```

##Links

- [openFrameworks documentation](http://openframeworks.cc/documentation/)
- [Markdown Basics](https://daringfireball.net/projects/markdown/basics)

##Homework due next class
- Read [openFrameworks for Processing users](http://openframeworks.cc/tutorials/first%20steps/002_openFrameworks_for_processing_users.html)
- Build and play at least 8 example apps that come with openFrameworks. 
- Choose three that interest you most. Write a description of each using [markdown](http://support.mashery.com/docs/customizing_your_portal/Markdown_Cheat_Sheet). We will discuss them next class.
- Create a sketch that uses at least three variables of two different types.