# ISP-CTF
Con số yêu thích của bạn là gì?
https://ctf.infosecptit.club/files/ca3121005db48ad2907c242dedc570c3/favorite_num.py?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NX0.ZGF8XA.k55Xyj6H6HNNWlm_lQZyA2bxbBE

1. Mở file, file yêu cầu nhập vào chuỗi số có 8 chữ số để check file
```
import hashlib

hashed_key = "b3d77ed0c460ef460792f07ad1e471d5fe70ac85c514e0b21b32e49d0f1b2c55"
hash_secret = 31580683746748870831459475506823890005573670692504809

def encrypt(key):
    result = hash_secret ^ key
    return result

def hash(user_input):
    salt = "ISP_Salt"
    return hashlib.sha256(salt.encode() + user_input.encode()).hexdigest()

def check_input(user_input):
    hashed_user_input = hash(user_input)
    return hashed_user_input == hashed_key

def main():
    my_string = input("What is your favorite number?: ")
    if len(my_string) == 8 and check_input(my_string):
        key = int(my_string)
        result_int = encrypt(key)
        result_bytes = result_int.to_bytes((result_int.bit_length() + 7) // 8, 'big')
        flag_str = ''
        for b in result_bytes:
            flag_str += chr(b)
        print(f"ISPCTF{{{flag_str}}}\n")
    else:
        print("That number isn't right!")

if __name__ == "__main__":
    main()
```
2. Do đó ta chạy 8 vòng for lồng nhau để check all trh
```
import hashlib
hashed_key = "b3d77ed0c460ef460792f07ad1e471d5fe70ac85c514e0b21b32e49d0f1b2c55"
hash_secret = 31580683746748870831459475506823890005573670692504809
def encrypt(key):
    result = hash_secret ^ key 
    return result
def hash(user_input):
    salt = "ISP_Salt"
    return hashlib.sha256(salt.encode() + user_input.encode()).hexdigest()   
def check_input(user_input):
    hashed_user_input = hash(user_input)
    return hashed_user_input == hashed_key
def main():
    #my_string = input("What is your favorite number?: ")
    for i in range(10):
        for o in range(10):
            for p in range(10):
                for a in range(10):
                    for s in range(10):
                        for d in range(10):
                            for f in range(10):
                                for g in range(10):
                                    new_string = chr(i+48) + chr(o+48) + chr(p+48) + chr(a+48) + chr(s+48) + chr(d+48) + chr(f+48) + chr(g+48)
                                    if len(new_string) == 8 and check_input(new_string):
                                        key = int(new_string)
                                        result_int = encrypt(key)
                                        result_bytes = result_int.to_bytes((result_int.bit_length() + 7) // 8, 'big')
                                        flag_str = ''
                                        for b in result_bytes:
                                            flag_str += chr(b)
                                        print(f"ISPCTF{{{flag_str}}}\n")
                                    #else:
                                        #print("That number isn't right!")  
if __name__ == "__main__":
    main()
```
3. Kết quả flag in ra là: ISPCTF{That_iS_Special_Number}
