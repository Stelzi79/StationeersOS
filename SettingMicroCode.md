# Setting Micro Code

## 00 => NOP

***No operation***: Reads Setting till there is another value

## 01 *````program````* => SPRG

***Load Program***: Sets the program from central program storage with the number *````program````* into the stack.

## 02 *````address````* => SADR

***Load Address***: Sets the address of this IC10 to the number *````address````*. Addresses lower than 255 (0 - 254) are reserved for special default ICs like ALUs or global function resolving.
