# XOR Slide 

## Description 
You realise that a previous climber has set up a puzzle in what was otherwise an empty room, blocking the entrance to the next floor on the ceiling. You must slide the blocks forming the pyramid to create a path above.

## Writeup 
- The provided text is encrypted with sliding XOR
  Ecrypted cipher text:
  ```b31113bd631c7207ec9587b32e686c8b6df255d66f4a987adacf6c283875ded5d1633b5f8823fa0b9bbbfab3195f1a51506afd54e03392ae338d872445c9025d88c8d4425a00a9b4478f86acadbd781df6a4194e376c09145a6f9afcbe02d36b5709f74d910edf94552dc4680041d6717fea824718c21385bdfd6176f722100548336d10ead87f01a95c5497dcb6c2```
- The following code is used to decipher and get the flag 

```bash

from binascii import unhexlify

ct = bytes.fromhex(
    'b31113bd631c7207ec9587b32e686c8b6df255d66f4a987adacf6c283875ded5d'
    '1633b5f8823fa0b9bbbfab3195f1a51506afd54e03392ae338d872445c9025d88'
    'c8d4425a00a9b4478f86acadbd781df6a4194e376c09145a6f9afcbe02d36b570'
    '9f74d910edf94552dc4680041d6717fea824718c21385bdfd6176f72210054833'
    '6d10ead87f01a95c5497dcb6c2'
)

wrapper = [
    b'bro i have a cRAzy story to tell you i went to ant4rctica and BOOM i saw a random citadel{',
    b'} it was crazy like how did it get there??'
]

lf = len(ct)
lks = len(wrapper[0] + wrapper[1])
lr = lf - lks

def xor_single_with_sequence(first_byte: int, seq: bytes) -> bytes:
    v = first_byte
   
    for b in seq:
        v ^= b
    return bytes([v])

ks = bytearray(lks)


for i in range(len(wrapper[0])):
   
    arr = ks[max(0, i - lr):i]
   
    ks[i] = int.from_bytes(xor_single_with_sequence(ct[i] ^ wrapper[0][i], arr))


for i in range(-1, -len(wrapper[1]) - 1, -1):
    # a corresponds to the slice used in original code
    a = ks[lks + i : min(lks + i + lr + 1, lks)]
   
    ks[i] = int.from_bytes(xor_single_with_sequence(ct[i] ^ wrapper[1][i], a))

print(f'ks: {ks.hex()}')


flag = bytearray(ct)
for i in range(len(flag) - len(ks) + 1):
    for j in range(len(ks)):
        flag[i + j] ^= ks[j]


print(flag.decode(errors='replace'))
```
