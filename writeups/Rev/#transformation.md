Transformation


The first thing i did was start the install the file given and use the cat command to read it. This revealed something which looked like Chinese characters. My first thought was to run the characters through google translate. While it told me the language itself was traditional Chinese, it was unable to translate it. I also tried a few other translators but none worked. Then i saw the line of code provided along with the problem. i input the full code into google but that only opened writeups for this specific challenge. So, i fed the code into claude and told it to tell me what every part of the code did. The last part of the statement was a for loop which was quite easy to understand. ord was used to give the ascii code for a number. After to using ord to give the ascii chord, "<<8" would then shift it to the left by 8 bits. It would then be added to the ord of the character after the one at position i, however that would be added into the low byte. So, the upper byte would have the ascii of the first number and the lower would have the ascii of the second. the function chr then turns this 16 bit number into the Unicode character. Then ' '.join joins all these Unicode characters to give a string. So, to decode the initial string, all that had to be done was reverse this process. To do this, first we need to write a new for loop which runs as long as the length of the encoded string. Then for each character, we have to separate the upper byte by shifting it right by 8 bits and add it to the lower one. However, to extract only the lowest byte, we have to accompany the lower character with a 0xFF to keep only the lowest 8 bits and clear all the rest. This is known as a bitmask. After this, once added instead of the one 16 bit Unicode character, we will be left with 2 combined 8 bit characters in their ascii values. So, we will also have to specify to turn it back into characters using chr() before printing. However this will have to be done before adding since it is not possible to concatenate int to string. This will leave us with the following code. 



flag1 = '灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸形㝦㘲捡㕽'
flag = ''
decoded =''
for i in range(len(flag1)):
    flag = ord(flag1[i])
    decoded += chr(flag >> 8)
    decoded += chr(flag & 0xFF)
print(decoded)


The flag after running this code is: picoCTF{16_bits_inst34d_of_8_b7f62ca5}


Takeaway: Combining separate bytes into one character is possible, and so is reversing it. 