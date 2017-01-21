# linux-keyboard-disable

## Install
`sudo apt-get install input-utils`

## Usage
Examine internal keyboard number
`less /proc/bus/input/devices`
```
I: Bus=0011 Vendor=0001 Product=0001 Version=ab54
N: Name="AT Translated Set 2 keyboard"
P: Phys=isa0060/serio0/input0
S: Sysfs=/devices/platform/i8042/serio0/input/input0
U: Uniq=
H: Handlers=sysrq kbd event0 
B: PROP=0
B: EV=120013
B: KEY=402000000 3803078f800d001 feffffdfffefffff fffffffffffffffe
B: MSC=10
B: LED=7
.
.
.
```

Keyboard number is event0 in this case. This number is different for each environment.

This command can know keymap.
`sudo input-kbd 0`
```
/dev/input/event0
   bustype : BUS_I8042
   vendor  : 0x1
   product : 0x1
   version : 43860
   name    : "AT Translated Set 2 keyboard"
   phys    : "isa0060/serio0/input0"
   bits ev : EV_SYN EV_KEY EV_MSC EV_LED EV_REP

map: 149 keys, size: 512/512
0x0001 =   1  # KEY_ESC
0x0002 =   2  # KEY_1
0x0003 =   3  # KEY_2
0x0004 =   4  # KEY_3
.
.
.
```
Be backup this result.

Create map file with last from `0x0001 = 1 # KEY_ESC`. This file name is map.txt in this case.
Create disable map. `255` is disable.
```
0x0001 = 255  # KEY_ESC
0x0002 = 255  # KEY_1
0x0003 = 255  # KEY_2
0x0004 = 255  # KEY_3
.
.
.
```

Disable internal keyboard.
`sudo input-kbd -f map.txt 0`

### Last
If internal keyboard, Reboot or `sudo input-kbd -f normal-map.txt 0`
