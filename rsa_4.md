nc 157.245.150.103 7999
https://ctf.infosecptit.club/files/1828abb6eb640e1a1aca59f12f88418a/rsa_5.py?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NTJ9.ZGLKwA.QNmzpC3tANmlFtwFbMyJqgu4so0

1. Mở file rsa_5:
```
import socket,threading
from Crypto.Util.number import *
from random import choice
from string import ascii_letters, digits

def RSA():
    mess = "".join(choice(ascii_letters+digits) for _ in range(20))
    mess_num = bytes_to_long(mess.encode())
    p = getPrime(128)
    q = getPrime(128)
    n = p*q
    e = 65537
    d = pow(e,-1,(p-1)*(q-1))
    c = pow(mess_num,e,n)
    print(f"d: {d}\ncipher: {c}\n")
    user_input = input("Guess message: ")
    if user_input == mess:
        with open('flag.txt','r') as f:
            flag = f.readline()
            print(f"{flag}\n")
    else:
        print(f"wrong message !!!\n")
   ```
   from Crypto.Util.number import *: dùng để xử lý số trong mật mã học, trong trh này nó đc use để chuyển đổi giữa chuỗi và số nguyên dài
   from random import choice: lấy ngẫu nhiên 1 kí tự trong chuỗi
   from string import ascii_letters, digits: cung cấp các chuỗi các kí tự chữ cái và số
   Trong hàm RSA:
   - mess = "".join(choice(ascii_letters+digits) for _ in range(20)): chọn ngẫu nhiên 20 kí tự chữ cái và số đưa vào biến mess lưu trữ
   - mess_num = bytes_to_long(mess.encode()): chuyển chuỗi thành số nguyên dài bằng cách mã hóa nó sang dạng bit sau đó chuyển thành số nguyên dài
   - p = getPrime(128): tạo 1 số nguyên tố ngẫu nhiên có 128 bit
   - print(f"d: {d}\ncipher: {c}\n"): in ra c và d dưới định dạng chuỗi
   - đoạn code yêu cầu người dùng nhập vào đoạn chuỗi để check, nếu nố == mess thì nó sẽ in ra flag
   
   2. nhập lệnh: nc 157.245.150.103 7999 và terminal
   d: 69977796358125431109419993282330901882600172680709170613743368300479685121329
   cipher: 56938892237305065563401338602369575919497695787523845596497092175883381760253
   Guess message: 
   
   3. 
