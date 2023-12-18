# Wargames.my 2023 Writeups

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/3cc54c6b-65c5-4a43-8403-78a580f6ab8d)

## Web - Warmup

- open the given link you will get the password form `Enter password to get flag!`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/b6092705-3410-457d-8f88-f9de0a25c988)

- view page source and and goto `/static/script.min.js`, thare are function that has been obfuscate

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/bc150520-cd35-4a37-9ffe-3e3fb19cb3d7)

- using this online deobfuscate [JavaScript Deobfuscator](https://obf-io.deobfuscate.io/) to view the souce code and find the password

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/09a69afa-ab1b-4d62-9859-448c0b0550bf)

- after entered the password, there are popup says `here your flag in comment`, looking at network tab there are new get request

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/d6a58ace-2bf2-4ad7-b795-c229f92b68cd)

- view the source code, you will get this

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/77753943-2214-451d-b04c-8f68180c54b2)

- looking at the URL give me idea that is parameter that can use for `File Inclusion/Path traversal`, open the burp suite and do some testing

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/ed26ec9d-0e78-43f4-a450-695030959a2a)

- using this payload `x=php://filter/convert.base64-encode/resource=flag_for_warmup.php` refer form [hacktrics](https://book.hacktricks.xyz/pentesting-web/file-inclusion), get this response `did you just mention "convert"?? i'm quitting now`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/a13583fc-f9fc-4039-b249-10d1b9cae98f)

- so i decide to url encode the strings `convert` still did not bypass, after that i try to double url encoding and it works, `convert -> c%256f%256e%2576%2565%2572%2574`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/12808b50-cb6f-4e3a-8ca5-5511c94899e7)

- decode the base64 and get the flag

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/0b56ee93-745e-4632-aa9a-896da4d246ad)

flag `wgmy{1ca200caa85d3a8dcec7d660e7361f79}`

## Forensic - Compromised

- download and extract the given file `evidence.zip`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/8c4ef906-a211-4d7c-9629-5552cef6058b)

- after analyze the size of the folder and identify what file have the biggest sizes, found that the file locate at `\AppData\Local\Microsoft\Terminal Server Client\Cache\Cache0000.bin`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/854e0266-3c9b-4ecc-8f00-c2a2e900a102)

- open the file using notepad, google what is this `RDP8bmp`, and found others writeups [link](https://medium.com/@yashkumarnavadiya/htb-no-place-to-hide-easy-forensics-challenge-b025c864607a)

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/2ed75b75-4128-414a-9475-df19e6367f76)

- i just follow the writeups and use this github tools [RDP Bitmap Cache parser](https://github.com/ANSSI-FR/bmc-tools) to extract data from `Cache0000.bin`, there are thousand of bmp images

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/fcda9a2b-8a18-456c-93de-8304a83cb3bd)

- after that using this github tools [RdpCacheStitcher](https://github.com/BSI-Bund/RdpCacheStitcher) to arrange the bmp images, and found interesting part which is password for zip file

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/03cef38f-2502-405a-a178-4ce5aa67b963)

- goto `\Desktop` directory found `flag.png`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/5aced1e5-1aa0-43cc-974a-e85b9b1818e4)

- inspect the file and get the file actually zip file

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/44d832c7-96b7-4c35-be0f-f5e97fab5e9d)

- change the extension, and extract the zip file using the password you get before this, open `flag.txt`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/f41e9469-2302-4d3d-84a0-ddda40a614d4)

flag `wgmy{d1df8b8811dbe22f3dce67ef2998f21c}`

## Reverse - Defeat the boss!

- download the given file `Game_boxed.exe` and open the file, actually this is RPG Maker Game

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/2fccc6b7-9102-4630-8a95-a96b7c57dc69)

- after exploring the whole game, there is a chest in the game but the chest is outside the map

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/ab7535ab-0bce-4723-a8f4-9bf2394ceda5)

- i am gamer before this, i know some mechanics of the game, so i need to find place where i can exit the map, i found that 2 places you can get out the map, refer to image below

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/5f23c07a-5d18-4b0e-b69c-c5802d84bcb2)

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/36817119-bad8-4a02-9ad2-e2e17366e6c8)

- goto chest outside the map, got the some pieces of the base64 flag, this game have 4 pieces of flag

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/c23f2047-0852-40b4-9ccf-db8b435c1c38)

- goto merchant like this and buy the `Dead Sea Scroll 500000`, but i cannot afford to buy, so decided to do some modification of the save game using [save editor online](https://www.save-editor.com/tools/rpg_tkool_mz_save.html)

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/26b8347c-f8aa-4ad5-a725-b40b17488efa)

- so how to know the location of the savegame, first just save the game, then goto same directory of the game it automatically create a folder name `save`, goto folder `save`, and upload the file `rmmzsave` to save editor online

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/f2e95821-7d9c-4596-bf1a-6b8bb66bf102)

- after edited the save game, download and replace the same name file, open game and load the new edited save game, and buy `Dead Sea Scroll 500000` and use the item, and got another pieces of the base64 flag

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/c1a9ee9b-f13b-43c6-9d1b-d99263e3b62f)

- kill the boss, got another pieces of the base64 flag

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/154a67bd-e676-4457-9a25-9fd4331d01f1)

- last part is i need to guess the number, from this part i dont how to continue the game

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/da685690-b237-4e86-8a2d-77b7c6db101d)

- so i decided to check strings of the file and grep the keyword `Hey hey`

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/35eea658-4014-4ecd-b0e3-a0143404ac69)

- combine all the pieces base64 and decode

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/38779e2c-7b0d-48b3-831e-508578841190)

flag `wgmy{9dedace597929c5316d6443d2783d291}`

## Misc - Splice

- given 3 part of QR pages

| page 1 | page 2 | page 3 |
|--------|--------|--------|
| ![page1](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/37c41282-c66a-4a25-866c-4c4ce19164c3) | ![page2](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/c24dc7d2-1805-4724-b837-2fe45fc230be) | ![page3](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/779ede0a-af9e-40ba-a802-cab957dbb6ef) |

- there are 2 part of QR, i just create

| QR 1 | QR 2 |
|------|------|
| ![qr1](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/a4f9aec3-266d-469c-b9de-6a6c5fe18d68) | ![qr2](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/7f1b3d99-6977-4bd1-b11a-7c580b47b128) |
| QR 1 = Page 1 \(Dark) \+ Page 3 \(Dark) | QR 2 = Page 2 \(Dark) \+ Page 3 \(Dark) \+ \[Page 3 \(Gray) - \[Page 3 \(Gray) ∩ QR1 \(Dark)\]\] |

- just combine the result of both QR will get flag in base64

![image](https://github.com/0hanif0/WGMY2023CTF-Writeups/assets/23289982/a45d8818-ad30-469c-903c-bf3ea867e8c4)

flag `wgmy{5d7bdea65472ca9e615fcbd0f90a3b49}`
