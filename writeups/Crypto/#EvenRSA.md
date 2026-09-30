EVEN RSA CAN BE BROKEN?


I have a bad habit of immediately opening the hints since I feel a bit lost without them. As soon as I opened the second hint which told me to focus on something interesting about N. Due to the induction ctf I already had a clue on how RSA worked, mainly about the 2 primes and the mod N being factored off of them. I noticed that N was an even number, so I figured out that one of the 2 primes had to be 2 which meant that phi N(or modN as in the program) had to equal the other prime -1. I tried a few websites which could maybe solve the question for me such as decoders, etc. however these did not work. So, I made a python code and looked up how to do a modular multiplicative inverse calculation in python. To proceed with this, I first had to learn what in the world a modular multiplicative inverse calculation was. I used geeksforgeeks to learn about modular multiplicative inverse. Then, I used the inbuilt pow(e, -1, modN) function to calculate d, the private key. After this I knew that to decrypt i had to use d which I had just calculated for which I used another triple power. However, after all this I was left with something that I could not read since it was still in the raw integer form. I had to find a way to convert the number into readable text. I looked up how to do this and it showed me a function called .to_bytes, so i used this to convert into readable form and get the flag. 


This is the code I used:
N = 16382422720915285631524725937435632372091321713918149533055051858269696398848308971395083740090726433058925589074276462089150062466497082377826436649024178
e = 65537
c = 4783011867842028128462764477759831949044123318334210754013549500798400212416258690001819910335045964621239306364005833316667816341951713162223871546346127
q = N // 2
modN = q-1
d = pow(e, -1, modN) 
decrypt = pow (c, d, N)
byte_length = (decrypt.bit_length() + 7) // 8
word = decrypt.to_bytes(byte_length, byteorder='big')
print(word)


the flag for this particular instance was picoCTF{tw0_1$_pr!m305af7255}

Main takeaway - RSA is difficult to break simply because of how hard it is to factor N by those 2 primes. If one of those primes is 2(or something else easy) RSA becomes quite easy to break. 