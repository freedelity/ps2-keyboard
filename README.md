PS/2 Keyboard library for Arduino
=================================

That library implements the PS/2 protocol for keyboards.
You can then interface with an old PS/2 keyboard, or emulate key events to a computer with a PS/2 port.


Setup Instructions
------------------

Copy the folder `FidPS2` in your arduino libraries folder.

Then, include the header files in your project source file:
```
#include <FidPS2Keyboard.h>
#include <FidPS2Host.h>
```

Interfacing a keyboard
----------------------

First, you have to init the library by calling the function
```
void fid_ps2kb_init(int data, int clock)
```
where `data` is the Arduino pin number attached to the data pin of the keyboard, and `clock` is the arduino pin attached to the clock pin.

Then you can listen for incoming keys by using
```
bool fid_ps2kb_read(uint8_t* b)
```
This function returns `true` if there is a byte in the buffer and writes its value in the variable pointed by `b`.
The next call would write the next bytes and so on, until it returns `false` indicating that the buffer is empty.

And you can send bytes to the keyboard for commands (like changing LEDS for numlock or capslock states) with this function:
```
void fid_ps2kb_write(uint8_t b)
```

Emulating a keyboard
--------------------
The API is very close to the one for interfacing to a keyboard.

The initialization function is the following:
```
void fid_ps2h_init(int data, int clock);
```

You can send bytes to the computer with this function:
```
void fid_ps2h_write(uint8_t b)
```

And get the response back, or incoming commands with:
```
bool fid_ps2h_read(uint8_t* b)
```
It returns `true` as long as there is still bytes in the buffer, and write their values to the variable pointed by `b`.
