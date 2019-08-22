# GPLC - General Purpose Logic Cell

## Theory of Operations

The Cell waits for a SPRG and a SADR command to be sent by some external cell or logic tasked to initialize this new GPLC do ````db.Setting```` as per normal ComBus commands.

Then it Loads program execution code with the number ````Program```` from the central  Code Storage into the stack.

When it is ready to execute it communicates to the ````Parent```` ComBus cell to be up.

Then it starts executing the previously loaded code.

## Register and IO Mappings

| Short | Alias      | Description                                              |
| ----- | ---------- | -------------------------------------------------------- |
| d0    | Parent     | The parent ComBus Cell to communicate with other devices |
| db    | DeviceBase | The base where the IC is situated                        |
| r0    | Cursor     | Cursor register                                          |
| r1    | tRa        | temporary save value of ````ra````                       |
| r2    | pram       | numbers of parameters to readin                          |
| r14   | Address    | Address of the Logic Cell                                |
| r15   | Program    | Number of loaded program                                 |

## Script

[Stationeering PermaLink](----)

```mips
# StationeersOS
# General Purpose Logic Cell
bootup:
alias Parent d0
alias Program r15
alias Address r14
define MinAdr 254
alias Cursor r0
alias tRa r1
alias param r2
beqzal Program readinLoop
beqzal Address readinLoop

# Load program execution code with
# the number <Program> from the central
# Code Storage.

# When it is ready to execute it communicates
# to the <Parent> ComBus cell to be up.

# Start executing loaded code.

readinLoop:
l Cursor db Setting
s db Setting 0 # ready for next readin
beq Cursor 0 readinLoop # NOP
bgtz param paramsReadIn
beq Cursor 1 setProgram # SPRG
beq Cursor 2 setAddress # SADR

paramsReadIn:
push Cursor
move Cursor 0
sub param param 1
bgtz param readinLoop

bgtz ra ra
j readinLoop

setProgram:
sub tRa ra 1   # preserve ra
move param 1   # we have to readin 1 parameter
jal readinLoop
pop Program
j tRa

setAddress:
sub tRa ra 1   # preserve ra
move param 1   # we have to readin 1 parameter
jal readinLoop
peek Cursor
blt Cursor MinAdr readinLoop
pop Address
j tRa
```
