autorev 1


Truly i was almost entirely lost on how to start with this. Since there were no hints provided for this assignment i decided to look up a writeup and try to understand the solution rather than come up with it myself. The code that ive used is from that writeup, however i will now explain the working as i understand it. First of all we need to import pwntools so that we can solve the question. Then we need to open up a tcp connection to the server and make it possible to read and write programmatically. Since there are 20 secrets we need to run the loop 20 times. Inside the loop, first we use r.recvuntil() to read and discard everything until the selected text shows up. then we use recvline().script() to read the line till the next newline and then the strip() removes the newline character and any spaces. Recvline returns the received bytes which are then turned into a string using .decode(). then, bytes.fromhex() converts the pair of hex digits into one byte. So: c745fc turns into b"\xc7\x45\xfc".C745FC is important since it is followed by the 4 byte secret. C7 is the opcode for mov, which is used to copy data from a source to another destination. I do not understand what 45 and fc do. However, the next 4 bytes following this are the secret. Since it is in x86 it is stored as a 32 bit little endian integer. Then, we use idx to find the first occurrence of it in the binary. Then, once we find the location of it, we first do idx + 3 to skip the first 3 signature bytes(b"\xc7\x45\xfc") and then binary[idx+3:idx+7] picks out the 4 bytes after the signature. u32 interprets them as the unsigned little endian of 32 bits. r.recvuntil(b"What's the secret?") waits until the server asks for the answer so that it only sends when asked. r.sendline(str(secret).encode()) is used after. str() is used to turn the number into text, and then .encode() is used to convert it back into bytes since the server will only accept byte answers. sendline sends the bytes along with a newline, to mimic pressing enter after sending the secret. this entire process loops 20 times. After the loop is over, we use print(r.recvall().decode()). recvall() keeps reading until the server is closed and returns everything that it sends out. decode turns it into text and then it is printed. This is where the flag shows up. 


Code:
from pwn import *
import sys

# Usage: python solve.py [host] [port]
HOST = sys.argv[1] if len(sys.argv) > 1 else "chatelaine.cylabacademy.net"
PORT = int(sys.argv[2]) if len(sys.argv) > 2 else 13346

r = remote(HOST, PORT)

for i in range(20):
    r.recvuntil(b"Here's the next binary in bytes:\n")
    hex_blob = r.recvline().strip()
    binary = bytes.fromhex(hex_blob.decode())

    sig = b"\xc7\x45\xfc"
    idx = binary.find(sig)

    secret = u32(binary[idx + 3 : idx + 7])

    r.recvuntil(b"What's the secret?")
    r.sendline(str(secret).encode())

print(r.recvall().decode())


Flag: academy{4u7o_r3v_g0_brrr_78c345aa}

Takeaway: Learnt how to access a server using code
		   pwntools lib use
		   finding patterns in binary
		   