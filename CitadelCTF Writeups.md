# Omniscient Flag's Metadata

## Description 
As you step into the second chamber, a figure manifests. Before you stands a forgotten deity, a dead god spoken of only in whispers. Known by countless names: “Apostle of Epilogue and Eternity”, “Lone Messiah” and many more lost to time.

They leave nothing but a single image, a relic carrying his final secret. Hidden within its layers lies the key to ascend to the next chamber.

## Writeup:

- On opening the file attached in the challenge, it shows:
  
  <img width="640" height="1017" alt="image" src="https://github.com/user-attachments/assets/30ee5e21-3ab2-4af8-96a2-220206ddd7d7" />
  
- As the the question is about metadata, check EXIF metadata by running `exiftool challenge.jpg` in the terminal.
  ```sh
  Last login: Sat Oct  4 17:30:48 on console
  nehanandini@Nehas-MacBook-Air ~ % exiftool challenge.jpg
  zsh: command not found: exiftool
  ```
- This means that `exiftool` is not installed on the Mac.
- So install it first using `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` to install homebrew first but since homebrew is already there, use `brew install exiftool` to install exiftool.
- Run `exiftool challenge.jpg` to check its metadata.
  ```sh
  mdls challenge.jpg
  _kMDItemDisplayNameWithExtensions  = "challenge.jpg"
  kMDItemAuthors                     = (
      "kdj had a habit of hiding images within images"
  )
  kMDItemBitsPerSample               = 24
  kMDItemColorSpace                  = "RGB"
  kMDItemContentCreationDate         = 2025-10-04 12:40:00 +0000
  kMDItemContentCreationDate_Ranking = 2025-10-04 00:00:00 +0000
  kMDItemContentModificationDate     = 2025-10-04 12:40:01 +0000
  kMDItemContentType                 = "public.jpeg"
  kMDItemContentTypeTree             = (
      "public.jpeg",
      "public.image",
      "public.data",
      "public.item",
      "public.content"
  )
  kMDItemDateAdded                   = 2025-10-04 12:40:00 +0000
  kMDItemDisplayName                 = "challenge.jpg"
  kMDItemDocumentIdentifier          = 0
  kMDItemFSContentChangeDate         = 2025-10-04 12:40:01 +0000
  kMDItemFSCreationDate              = 2025-10-04 12:40:00 +0000
  kMDItemFSCreatorCode               = ""
  kMDItemFSFinderFlags               = 0
  kMDItemFSHasCustomIcon             = (null)
  kMDItemFSInvisible                 = 0
  kMDItemFSIsExtensionHidden         = 0
  kMDItemFSIsStationery              = (null)
  kMDItemFSLabel                     = 0
  kMDItemFSName                      = "challenge.jpg"
  kMDItemFSNodeCount                 = (null)
  kMDItemFSOwnerGroupID              = 20
  kMDItemFSOwnerUserID               = 501
  kMDItemFSSize                      = 371263
  kMDItemFSTypeCode                  = ""
  kMDItemHasAlphaChannel             = 0
  kMDItemInterestingDate_Ranking     = 2025-10-04 00:00:00 +0000
  kMDItemKind                        = "JPEG image"
  kMDItemLastUsedDate                = 2025-10-04 12:42:39 +0000
  kMDItemLastUsedDate_Ranking        = 2025-10-04 00:00:00 +0000
  kMDItemLogicalSize                 = 371263
  kMDItemOrientation                 = 1
  kMDItemPhysicalSize                = 380928
  kMDItemPixelCount                  = 650880
  kMDItemPixelHeight                 = 1017
  kMDItemPixelWidth                  = 640
  kMDItemProfileName                 = "sRGB IEC61966-2.1"
  kMDItemUseCount                    = 8
  kMDItemUsedDates                   = (
      "2025-10-03 18:30:00 +0000"
  )
  kMDItemWhereFroms                  = (
      "https://citadel.cryptonitemit.in/files/2378893c721bd88ce6e99b644c4ef130/challenge.jpg?token=eyJ1c2VyX2lkIjoyMTUsInRlYW1faWQiOjY3LCJmaWxlX2lkIjo0NX0.aOEVfA.ITrIVbCALijLLz16Cv7L39lg5sM",
      "https://citadel.cryptonitemit.in/challenges"
  )
  ```
- The `mdls` output shows
  ```sh
  kMDItemAuthors = (
    "kdj had a habit of hiding images within images"
  )
  ```
- This hint is important to solve the challenge.
- It means that the image contains another image hidden within it.
- Three techniques that causes the above scenario exist:
  - Steganography which means hiding an image inside another
  - Double file meaning an image appended after the JPEG end
  - LSB (Least Significant Bit) steganography
- First check if theres an appended data after the JPEG end.
- For that, use `xxd challenge.jpg | tail -20`.
   ```sh
  nehanandini@Nehas-MacBook-Air ~ % xxd challenge.jpg | tail -20
  xxd: challenge.jpg: No such file or directory
  ```
- It shows the above as the directory has to be Downloads where the challenge.jpg is located.
- Run 
  ```sh
  cd ~/Downloads
  grep -a "CTF{" challenge.jpg
  ```
- The above changes the directory to Downloads and then checks if theres data after the JPEG end marker.
- The output would be
  ```sh
  cd ~/Downloads
  nehanandini@Nehas-MacBook-Air Downloads % grep -a "CTF{" challenge.jpg
  nehanandini@Nehas-MacBook-Air Downloads % xxd challenge.jpg | tail -20
  0005a900: 4d53 1405 09d8 8e24 f2e2 2bf9 6ac9 ee87  MS.....$..+.j...
  0005a910: 996a effc cea9 8aad 4899 f5a8 a072 8368  .j......H....r.h
  0005a920: 62a1 555b 3cc7 54ad 79f1 0df7 d82e 9b1f  b.U[<.T.y.......
  0005a930: 90f7 dd06 48b4 ad0f 64ea da83 18e7 5c9a  ....H...d.....\.
  0005a940: a6d3 2654 5555 96e5 d243 ebaa 723d e6b4  ..&TUU...C..r=..
  0005a950: 38e7 b0ea b765 719e 6f96 579a e02e 3dd7  8....eq.o.W...=.
  0005a960: 7bc1 e6ac b76e 8a6d 86e2 a2d7 b3a5 f7e5  {....n.m........
  0005a970: d263 9ce7 5fcf b6d0 a1ff 8d77 f9dc e5cd  .c.._......w....
  0005a980: 256f cf80 6f69 06f9 b6df 78ff c9e6 4ef7  %o..oi....x...N.
  0005a990: 85d7 981e 0f97 d105 31a5 f5d0 fefc 9f1c  ........1.......
  0005a9a0: 2e59 6d8e d5c4 5740 148e eb75 7bb4 12d9  .Ym...W@...u{...
  0005a9b0: 1bfd 5b3b 77a8 4188 70db 41e6 adc7 8e2b  ..[;w.A.p.A....+
  0005a9c0: 633d 033e a7c6 b04e 1978 b960 72fd b77a  c=.>...N.x.`r..z
  0005a9d0: db3d f4a0 1b81 e2b5 7c1d 5718 b8f0 6de6  .=......|.W...m.
  0005a9e0: 635b e6b7 2055 fd5e 87c8 6fcd 02d7 f78b  c[.. U.^..o.....
  0005a9f0: 7642 6806 0c0b eeb7 55d8 e082 a9ed f99f  vBh.....U.......
  0005aa00: 78be 97ed 0602 af37 821f 96ae 56fa 422e  x......7....V.B.
  0005aa10: 7291 e71f 573b fd71 cef5 6c0c 1dd6 7f65  r...W;.q..l....e
  0005aa20: d7eb e999 cfe5 6246 efff 035a 0819 3f6d  ......bF...Z..?m
  0005aa30: 3040 cf00 0000 0049 454e 44ae 4260 82    0@.....IEND.B`.
  ```
- The `xxd` output ends with `IEND` and `B` which is a PNG file signature.
- There exist a PNG image hidden after the JPEG data.
- Use Python to extract data after the JPEG marker.
  ```sh
  cd ~/Downloads
  python3 -c "
  data = open('challenge.jpg', 'rb').read()
  jpeg_end = data.find(b'\xff\xd9')
  if jpeg_end != -1:
      hidden_data = data[jpeg_end + 2:]
      open('hidden.png', 'wb').write(hidden_data)
      print(f'Extracted {len(hidden_data)} bytes to hidden.png')
      print('PNG file should contain the flag!')
  "
  ```
- The following is the output.
  ```sh
  Extracted 310775 bytes to hidden.png
  PNG file should contain the flag!
  ```
- `hidden.png` has been extracted from the JPEG file.
- Use `open hidden.png` to view the flag.

  <img width="514" height="456" alt="image" src="https://github.com/user-attachments/assets/320fb246-4ce6-4c4b-802f-1df30dcf2380" />

  The exctracted file might not be a valid PNG or it might be corrupted.
- Check what has actually been exctracted by running 
  ```sh
  cd ~/Downloads
  file hidden.png
  xxd hidden.png | head -3
  strings hidden.png | grep -E "CTF{|flag{|citadel{|FLAG{"
  xxd hidden.png | tail -10
  ```
- Verification of the file type and structure is done by `file hidden.png`.
- `xxd hidden.png | head -3` checks if the file has a valid PNG header.
- `strings hidden.png | grep -E "CTF{|flag{|citadel{|FLAG{"` looks for any flag formats existing.
- The end of the file is checked by `xxd hidden.png | tail -10`.
- The terminal steps with commands and output are mentioned below.
  ```sh
  nehanandini@Nehas-MacBook-Air Downloads % cd ~/Downloads
  nehanandini@Nehas-MacBook-Air Downloads % file hidden.png
  hidden.png: data
  nehanandini@Nehas-MacBook-Air Downloads % xxd hidden.png | head -3
  00000000: 0651 4fda d46d 6a00 968a 1e9d b680 1b45  .QO..mj........E
  00000010: 3b6d 37ca f6a0 028a 3caf 6a3c af6a 003e  ;m7.....<.j<.j.>
  00000020: 4aaf 3cbb 76cd ff00 3c91 be4f ef55 8d94  J.<.v...<..O.U..
  nehanandini@Nehas-MacBook-Air Downloads % strings hidden.png | grep -E "CTF{|flag{|citadel{|FLAG{"
  nehanandini@Nehas-MacBook-Air Downloads % xxd hidden.png | tail -10
  0004bd60: 148e eb75 7bb4 12d9 1bfd 5b3b 77a8 4188  ...u{.....[;w.A.
  0004bd70: 70db 41e6 adc7 8e2b 633d 033e a7c6 b04e  p.A....+c=.>...N
  0004bd80: 1978 b960 72fd b77a db3d f4a0 1b81 e2b5  .x.`r..z.=......
  0004bd90: 7c1d 5718 b8f0 6de6 635b e6b7 2055 fd5e  |.W...m.c[.. U.^
  0004bda0: 87c8 6fcd 02d7 f78b 7642 6806 0c0b eeb7  ..o.....vBh.....
  0004bdb0: 55d8 e082 a9ed f99f 78be 97ed 0602 af37  U.......x......7
  0004bdc0: 821f 96ae 56fa 422e 7291 e71f 573b fd71  ....V.B.r...W;.q
  0004bdd0: cef5 6c0c 1dd6 7f65 d7eb e999 cfe5 6246  ..l....e......bF
  0004bde0: efff 035a 0819 3f6d 3040 cf00 0000 0049  ...Z..?m0@.....I
  0004bdf0: 454e 44ae 4260 82                        END.B`.
  ```
- The issue is clear now. The extracted `hidden.png` doesn't have a proper PNG header (`89 50 4E 47`) but it does have the PNG end marker (`IEND`) at the end.
- So the PNG data starts somewhere before it was extracted. The following find actual PNG header in the original file.
  ```sh
  python3 -c "
  data = open('challenge.jpg', 'rb').read()
  png_start = data.find(b'\x89PNG\r\n\x1a\n')
  print(f'PNG header found at position: {png_start}')
  if png_start != -1:
      png_data = data[png_start:]
      open('correct.png', 'wb').write(png_data)
      print(f'Extracted {len(png_data)} bytes as correct.png')
      import subprocess
      result = subprocess.run(['file', 'correct.png'], capture_output=True, text=True)
      print(f'File type: {result.stdout}')
  else:
      print('No PNG header found in the file')
  "
  ```
- The above searchwa for the actual PNG header in `challenge.jpg`, extracts the PNG properly if found, saves it as `correct.png` and then checks if it's a valid PNG file.
- The output given by the terminal for the above is:
  ```sh
  PNG header found at position: 87530
  Extracted 283733 bytes as correct.png
  File type: correct.png: PNG image data, 640 x 613, 8-bit/color RGB, non-interlaced
  ```
- It means a valid PNG file was found and exctrated.
- Run `open correct.png` to view the flag.
- This leads to:
  
  <img width="640" height="613" alt="image" src="https://github.com/user-attachments/assets/7cd596e6-d8c9-4b4e-b1b8-d851f9963aa2" />

### Flag: 

```
citadel{th1s_ch4ll3ng3_1s_f0r_th4t_0n3_ex1ft00l_4nd_b1nw4lk_enthus14st}
```

# Randomly Accessed Memories

## Description: 
clone it, pull it, reset it, stage it,
commit, push it, fork, rebase it,
merge it, branch it, tag it, log it,
add it, stash it, diff, untrack it.

On your ascent to this floor, you hear these fragments being played back 

```sh
You look around and discover a chamber containing a vast archive of Daft Punk’s music, intertwined with cryptic commits left behind by other musicians. They seem ordinary at first glance, but not everything in the history is what it seems.
```

Challenge: https://github.com/evilcryptonite/daft-punk-archive

## Writeup:

- `git clone https://github.com/evilcryptonite/daft-punk-archive` to clone the repository as mentioned in the challenge.
- `cd daft-punk-archive` to change the current working directory to it.
- `not eveyrthing in the history is what it seems` implies that something is hidden so check the past commits for the hidden information.
- `git log --oneline` shows all the previous commits.
  ```sh
  nehanandini@Nehas-MacBook-Air daft-punk-archive % git log --oneline
  168947c (HEAD -> main, origin/main, origin/HEAD) Routine update #300
  778eece Routine update #299
  6246c98 Routine update #298
  726a3bf Routine update #297
  f15c7e5 Routine update #296
  589a485 Routine update #295
  5bbbf2e Routine update #294
  421e1ab Routine update #293
  6cf2ca4 Routine update #292
  7d22c4b Routine update #291
  804adf1 Routine update #290
  b788a15 Routine update #289
  8f06b9a Routine update #288
  f096064 Routine update #287
  b5f3b1c Routine update #286
  1cffc9e Routine update #285
  2e3d91d Routine update #284
  e252558 Routine update #283
  451a2f9 Routine update #282
  7e103ab Routine update #281
  8d1aac6 Routine update #280
  18f8435 Remove secret chunk 3 file (history-only)
  79af115 Add secret chunk 3 (base64) [commit 279]
  168947c (HEAD -> main, origin/main, origin/HEAD) Routine update #300
  778eece Routine update #299
  6246c98 Routine update #298
  726a3bf Routine update #297
  f15c7e5 Routine update #296
  589a485 Routine update #295
  5bbbf2e Routine update #294
  421e1ab Routine update #293
  6cf2ca4 Routine update #292
  7d22c4b Routine update #291
  804adf1 Routine update #290
  b788a15 Routine update #289
  8f06b9a Routine update #288
  f096064 Routine update #287
  b5f3b1c Routine update #286
  1cffc9e Routine update #285
  2e3d91d Routine update #284
  e252558 Routine update #283
  451a2f9 Routine update #282
  7e103ab Routine update #281
  8d1aac6 Routine update #280
  18f8435 Remove secret chunk 3 file (history-only)
  79af115 Add secret chunk 3 (base64) [commit 279]
  df7c6e6 Routine update #278
  c2bc017 Routine update #277
  f5fe582 Routine update #276
  e50c0ac Routine update #275
  2efae35 Routine update #274
  7349c47 Routine update #273
  aa62762 Routine update #272
  f5ddbea Routine update #271
  2120217 Routine update #270
  31820c9 Routine update #269
  92fa8cf Routine update #268
  cfd3f85 Routine update #267
  c445bce Routine update #266
  ef72333 Routine update #265
  005278a Routine update #264
  17ae81d Routine update #263
  4d1f40b Routine update #262
  0f389d4 Routine update #261
  8fb5ba9 Routine update #260
  bcf8626 Routine update #259
  97e570d Routine update #258
  4df46ff Routine update #257
  f3fa389 Routine update #256
  :
  ```
- The above shows these 2 commits:
  - `18f8435 Remove secret chunk 3 file (history-only)`
  - `79af115 Add secret chunk 3 (base64) [commit 279]`
  This means a file containing the secret chunk 3 was added in commit `79af115` and then removed in `18f8435` but it still exists in the Git history.
- `git log --oneline --grep="secret chunk"` to check if multiple parts that need to be combined exist.
  ```sh
  nehanandini@Nehas-MacBook-Air daft-punk-archive % git log --oneline | grep -i secret
  18f8435 Remove secret chunk 3 file (history-only)
  79af115 Add secret chunk 3 (base64) [commit 279]
  977d650 Remove secret chunk 2 file (history-only)
  cc8b79a Add secret chunk 2 (base64) [commit 122]
  86fdefa Remove secret chunk 1 file (history-only)
  50474f3 Add secret chunk 1 (base64) [commit 56]
  ```
  3 secret chunks that need to be combined to get the flag were added and removed.
- `git show 50474f3`, `git show cc8b79a` and `git show 79af115` exctracts each of the 3 chunks.
  ```sh
  nehanandini@Nehas-MacBook-Air daft-punk-archive % git show 50474f3
  commit 50474f316ba2ff644b546437a032971874f43ecf
  Author: Thomas Bangalter <thomas@daftpunk.com>
  Date:   Fri Apr 4 11:06:26 2025 +0530

    Add secret chunk 1 (base64) [commit 56]

  diff --git a/secret_chunk_1.b64 b/secret_chunk_1.b64
  new file mode 100644
  index 0000000..815a643
  --- /dev/null
  +++ b/secret_chunk_1.b64
  @@ -0,0 +1,2 @@
  +# secret piece 1
  +Y2l0YWRlbHt3M180cjM=
  nehanandini@Nehas-MacBook-Air daft-punk-archive % git show cc8b79a
  commit cc8b79a83c2ef5997c728d1037368042af85214f
  Author: Abel Tesfaya <abel@weeknd.com>
  Date:   Sat May 10 07:03:11 2025 +0530

    Add secret chunk 2 (base64) [commit 122]
  diff --git a/secret_chunk_2.b64 b/secret_chunk_2.b64
  new file mode 100644
  index 0000000..6199d9c
  --- /dev/null
  +++ b/secret_chunk_2.b64
  @@ -0,0 +1,2 @@
  +# secret piece 2
  +X3VwXzRsbF9uMXQzXw==
  nehanandini@Nehas-MacBook-Air daft-punk-archive % git show 79af115
  commit 79af115d8b2cef0f3110f21f5475e1b5bea1a0af
  Author: Julian Casablacasn <julian@thestrokes.com>
  Date:   Wed Apr 16 20:18:52 2025 +0530

    Add secret chunk 3 (base64) [commit 279]
  diff --git a/secret_chunk_3.b64 b/secret_chunk_3.b64
  new file mode 100644
  index 0000000..46cced2
  --- /dev/null
  +++ b/secret_chunk_3.b64
  @@ -0,0 +1,2 @@
  +# secret piece 3
  +dDBfZzF0X2x1Y2t5fQ==
  nehanandini@Nehas-MacBook-Air daft-punk-archive %
  ```
- The 3 are base64 chunks and need to be decoded and combined to give the flag.
- `echo "Y2l0YWRlbHt3M180cjM=" | base64 -d`, `echo "X3VwXzRsbF9uMXQzXw==" | base64 -d` and `echo "dDBfZzF0X2x1Y2t5fQ==" | base64 -d` gives the parts of the flag.
  ```sh
  nehanandini@Nehas-MacBook-Air daft-punk-archive % echo "Y2l0YWRlbHt3M180cjM=" | base64 -d
  citadel{w3_4r3%
  nehanandini@Nehas-MacBook-Air daft-punk-archive % echo "X3VwXzRsbF9uMXQzXw==" | base64 -d
  _up_4ll_n1t3_%
  nehanandini@Nehas-MacBook-Air daft-punk-archive % echo "dDBfZzF0X2x1Y2t5fQ==" | base64 -d
  t0_g1t_lucky}%   
  ```
- Combine the 3 parts to get the full flag.

### Flag: 

```
citadel{w3_4r3_up_4ll_n1t3_t0_g1t_lucky}
```


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

