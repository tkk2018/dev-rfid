# Summary

`TLV` where `T` is type, `L` is length, `V` is value.

Types:

```
0x01 = Lock control
0x02 = 
0x03 = NDEF
...
```

For example, the Memory content NDEF of a Mifare Ultralight Card.

Starting from Row 3: CC = Capability Container Bytes

```
[03] E1 10 12 00
```

where:

`E1` - Magic value, means NFC forum

`10` - Major and Minor of NFC forum

`12` - Size, `0x12` = 18 x 8 = 144 bytes

`00` - Access permission, `0x00` means access granted without any security.

```
[04] 01 03 A0 0C
[05] 34 xx xx xx
```

`01 03 A0 0C 34` - Lock Control TLV (This is not NDEF message. It must appear if is dynamic memory structure.)

```
[05] xx 03 0C D1
[06] 01 08 54 02
[07] 65 6E 68 65
[08] 6C 6C 6F FE
```

`03` - NDEF

`0C` - Length is 12.

`D1 01 08 54 02 65 6E 68 65 6c 6c 6F` - NDEF message

$\quad$ where:

$\quad$ $\quad$ `D1` - Record header byte

$\quad$ $\quad$ `01` - The type name field has a length of 1 byte.

$\quad$ $\quad$ `08` - The payload field has a length of 8 bytes.

$\quad$ $\quad$ `54` - "T" = RTD_TEXT

$\quad$ $\quad$ `65 6E` - en = english

$\quad$ $\quad$ `68 65 6C 6C 6F` - hello

`FE` - Terminate byte.

To check whether the entire mifare ultraligh card is locked, check the lock bytes in page `[02]`.

```
[02] 1C 48 00 00 [BCC1, INT, LOCK0, LOCK1]
```

`00 00` - Writable

`ff ff` - Read only

This is how Android API to change a NDEF tag to read only.

Reference

* https://stackoverflow.com/a/36234325/16027098

