CanYouSeeMe



As with all forensic challenges dealing with images, i immediately opened its metadata with exiftool. The attribution url looked suspiciously like a base64 encoded string and did not look anything like a url. This is what it was for my instance: "YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fYTgxZDk0MzF9Cg==". When decoded, it gives the flag


I only ran one command:
exiftool ukn_reality.jpg
then i used the website	https://www.dcode.fr/base-64-encoding to decode the string.


The flag was academy{ME74D47A_HIDD3N_a81d9431}. (this flag was not the original flag that i solved the challenge with, i resolved the challenge since i lost that flag)


Takeaway - If anything looks suspicious in the metadata, doesn't hurt to check it out






