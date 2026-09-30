RED


With any image based forensics challenge the first thing to do is use exiftool to check the metadata. This reveals a suspicious hidden poem. The capital letters in this poem spell out CHECKLSB. I did not know what LSB was but when i looked it up i found a tool called zsteg which is used to check the least significant bit(LSB) in png and bmp images. So i installed zsteg and ran it on red.png. This returned a suspicious string of characters in a section called text. These characters looked like something encoded in base64, so when i ran it through a decoder it returned the flag. 


First i ran:
exiftool red.png
followed by:
zsteg red.png
and then i ran it through the base64 decoder on https://www.dcode.fr/base-64-encoding


the flag obtained was academy{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_} (this flag was not the original flag that i solved the challenge with, i resolved the challenge since i lost that flag)

Takeaway - the least significant bit is one more place to hide data in a png or bmp file. 