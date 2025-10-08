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

### Output:
```bash
ks: d1b21fe19736267cfc6a57750db72a154aaad8ac4254989cf4f6921e0ef67aa70abfd6e2761402b88cdd21baf4e2dce87834d55729199d8c6b1d974413fc7c05fc5bec533a142c4fb775347dee44233dd30bd212d33b5461a966dd529af15af6ba2af99337f6515046dde44cc0382d252a783acc550237d4bd30b62afce905d45c3074fd
bro i have a cRAzy story to tell you i went to ant4rctica and BOOM i saw a random citadel{pyr4m1d+x0r} it was crazy like how did it get there??
```

### Flag:
 ```citadel{pyr4m1d+x0r}```


 # A Memory's a Heavy Burden 

 ## Despcription 
 You now find yourself in the place where many climbers have been laid to rest. A cold wind moves through the temple grounds, carrying whispers of the departed. Stone lanterns and marble graves reflect Buddhist traditions, their shadows stretching across the frost-covered earth.

The temple rests in the shadow of a very iconic mountain, quiet and imposing. Every detail in the image, the arrangement of the graves, the lanterns, and the lingering scent of incense, holds clues to its true location. You need to uncover the exact coordinates of where you are to move on from here.

Note: round off coordinates to 3 decimal places.

Flag format: citadel{XX.XXX_XXX.XXX}

## Writeup 
- To get this flag, we have to find the coordinates of the place in the given picture below.
  <img width="1151" height="471" alt="Screenshot 2025-10-08 at 9 08 42 AM" src="https://github.com/user-attachments/assets/37545eab-d39f-496d-a5a4-851d3b1326c7" />
- Using the hint, " The view of the temple streets to the north of Mount Fuji 🗻  offers a splendid sight, doesn’t it? ", we realise that the mountain in the back is Mt. Fuji.
- From the compass at the bottom, it is seen that Mt. Fuji is to the south of the temple, which means we have to search for temples to the north of Mt. Fuji.

  <img width="1436" height="871" alt="Screenshot 2025-10-08 at 9 17 00 AM" src="https://github.com/user-attachments/assets/0eb4c170-2e07-46af-bfa5-868882f45d83" />


  <img width="1010" height="486" alt="Screenshot 2025-10-08 at 9 03 51 AM" src="https://github.com/user-attachments/assets/7b0ec8d7-f7bb-48cc-8be6-8076492f2941" />

- After this, we get the coordinates of the place, and when rounded off, we get the flag.

### Coordinate: 
```- 35.4856897, 138.6987448```

### Flag: 
```citadel{35.486_138.699}```

