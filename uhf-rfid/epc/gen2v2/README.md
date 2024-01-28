# EPC Gen2V2

## Commands

The EPC Gen2V2 commands have two categories, mandatory and optional.

* Mandatory - Select, Query, QueryAdjust, QueryRep, ACK, NAK, Req_RN, Read, Write, Kill, and Lock.

* Optional - Access, Authenticate, BlockPermalock, BlockWrite, ReadBuffer and Untraceable.

> Note I think this is the reason why the Zebra ZT411 printer doesn't support the advance security features by NXP UCODE DNA.

## NXP UCODE DNA

The security commands under the mandatory are ___Kill___ and ___Lock___.

Meaning that any EPC Gen2V2 tag must at least support the following security features.

1. Able to lock the TID, EPC and USER memory block by using access password (write protection).

2. Able to void the tag by using kill password.


The security commands under the optional are ___Untraceable___, ___Authenticate___, ___ReadBuffer___ and etc.

They are implemented according to EPC Gen2V2 and is designed to be compliant with ISO/IEC 29167-10 standard.

1. Able to make the data untraceable (read protection). Can only read by TAM2 operation.

2. TAM1 - authentication only, protected by AES key0.
   For example, we have a common area among of our products. Then we can use this area for proof of origin.
   This can be used to authenticate a group of people as long as using the same key0.
   Logically, the speed is faster than TAM2.

3. TAM2 - reading the untraceable data, protected by AES key1.
   Normally, the key1 is unique for each tag to protect user data.
   Because of that, TAM2 can only read one tag at one time.
   Logically, the speed is slower than TAM1.
