# kbm-robot (Keyboard-Mouse-Robot)

kbm-robot is a module to help you emulate system wide keyboard and mouse actions. It uses java's robot class (a child process with stdio pipe communication) to help accomplish this.

Example:
```
var robot = require("kbm-robot");

robot.startJar();

robot.press("alt")
    .press("tab")
    .sleep(100)
    .release("tab")
    .release("alt")
    .sleep(100)
    .typeString("Hello World!")
    .go()
    .then(robot.stopJar);
```

# Install

```
npm install --save kbm-robot
```

# Documentation

### API functions
```
var robot = require("kbm-robot");
```
All functions except for startJar and stopJar are chainable. You must chain them and then call .go() to have things happen.

  - robot**.startJar(version)**
    - version - (String, optional, default is "6") - argument to specify which jar you want to run. Currently there is a Java 6 and Java 7 jar. Valid values are "6" or "7". If you are having trouble getting something to work, try using .startJar("7"); (You will need java >= 1.7 to run the 7 jar. Type java -version in a console to see your version).
    - This function must be called before any other api functions are used.
  - robot**.stopJar()**
    - Stops the child process that is running the jar.
  - robot**.press(key)**
    - key - (String, required)
    - Tells the robot to press (and hold) the specified key.
  - robot**.release(key)**
    - key - (String, required)
    - Tells the robot to release the specified key.
  - robot**.typeString(str, downDelay, upDelay)**
    - str - (String, required) - The string to type.
    - downDelay (int, optional, default is 0) - How long to wait after a key is pressed.
    - upDelay (int, optional, default is 0) - How long to wait after a key is released.
    - Tells the robot to type a series of keys. NOTE: it will only be able to type keys that have a one character long string code (it splits the string into 1 character parts). This is basically 0-9, a-z, punctuation, and any characters that you hold shift to type on your keyboard. \n will press Enter.
  - robot**.type(key, delay)**
    - key - (String, required)
    - delay (int, optional, default is 0) - How long to wait after the key is pressed.
    - Tells the robot to press and release the specified key.
  - robot**.sleep(delay)**
    - delay (int, required) - How long to sleep for in ms (1000 is 1 second).
    - Tells the robot to wait.
  - robot**.mouseMove(x, y)**
    - x - (int, required) - The X coordinate on your screen.
    - Y - (int, required) - The Y coordinate on your screen.
    - Tells the robot to move your mouse to the specified location.
  - robot**.mousePress(buttons)**
    - buttons (String, required) - A string containing 1, 2, or 3 or any combination of those. 1 is the left mouse button, 2 is the right mouse button and 3 is the middle mouse button. (Ex. "13" press mouse 1 and mouse 3).
    - Tells the robot to press (and hold) the specified mouse buttons.
  - robot**.mouseRelease(buttons)**
    - buttons (String, required) - A string containing 1, 2, or 3 or any combination of those. 1 is the left mouse button, 2 is the right mouse button and 3 is the middle mouse button. (Ex. "13" press mouse 1 and mouse 3).
    - Tells the robot to release the specified mouse buttons.
  - robot**.mouseClick(buttons, delay)**
    - buttons (String, required) - A string containing 1, 2, or 3 or any combination of those. 1 is the left mouse button, 2 is the right mouse button and 3 is the middle mouse button. (Ex. "13" press mouse 1 and mouse 3).
    - delay (int, optional, default is 0) - How long to wait after the mouse buttons are pressed.
    - Tells the robot to click the specified mouse buttons.
  - robot**.mouseWheel(amount)**
    - amount (int, required) - How many "notches" to move your mouse wheel. Negative values are "up" or "away" from you.
    - Tells the robot to scroll using the mouse wheel.
  - robot**.go(callback)**
    - callback (Function, optional) - The function to call after all actions are complete. If this argument is not given, then go() will return a promise.
    - Tells the robot to start the chained actions.

### Keys
All key strings are the same as you would find in Java's KeyEvent class: http://docs.oracle.com/javase/7/docs/api/java/awt/event/KeyEvent.html
For example the string "VK_UP" would represent the up arrow key.

However this library also supplies many "shortcut" strings to get your robot typing faster. (Also add on A-Z and 0-9 as shortcuts). When using a shortcut string of A-Z, case doesn't matter.
```
"ESC"
"F1"
"F2"
"F3"
"F4"
"F5"
"F6"
"F7"
"F8"
"F9"
"F10"
"F11"
"F12"
"CTRL"
"META"
"SUPER"
"ALT"
" "
"SPACE"
"LEFT"
"DOWN"
"RIGHT"
"UP"
"TAB"
"SHIFT"
"ENTER"
"\n"
"CAPS_LOCK"
"PRINT_SCREEN"
"SCROLL_LOCK"
"PAUSE_BREAK"
"BACKSPACE"
"DELETE"
"HOME"
"END"
"INSERT"
"PAGE_UP"
"PAGE_DOWN"
"NUM_LOCK"
"`"
"-"
"="
"["
"]"
"\\"
";"
"'"
","
"."
"/"
"KP_ADD"
"KP_-"
"KP_*"
"KP_/"
"KP_0"
"KP_."
"KP_1"
"KP_2"
"KP_3"
"KP_4"
"KP_5"
"KP_6"
"KP_7"
"KP_8"
"KP_9"
```

# License

MIT

P.S. If anyone knows how to ditch the java dependency while still having platform independent code, please let me know. I have a feeling it will be very hard to do.
