Tôi đã quên mất khóa khi đi tìm kho báu hãy giúp tôi tìm lại mã khóa của chương trình để có thể lấy được báu vật.
https://ctf.infosecptit.club/files/ab90f64210654162d33fc6897c6a68a6/enc.cpp?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NH0.ZGGNRg.ZVaUrh86vMb9No4AfZjHAlwS54M

1. mở file enc.cpp:
```
#include <iostream>
using namespace std;

int main() {
    int enc_flag[] = {82, 89, 71, 65, 80, 64, 96, 82, 39, 112, 91, 69, 42, 122, 127, 49, 118, 89, 42, 121, 72, 113, 52, 89, 72, 59, 122, 114, 104, 53, 102};
    int key[] = {0, 0, 0, 0, 0, 0};
    string flag = "XXXXXXXXXXXXXXXXXXXXXXXXX";
    int lenKey = 6;

    for (int idx = 0; idx < flag.length(); idx++) {
        flag[idx] = enc_flag[idx] ^ key[idx % lenKey];
    }

    cout << "Decrypted Flag: " << flag << endl;
    return 0;
}
```
chạy file này ra kết quả: Decrypted Flag: RYGAP@`R'p[E*z⌂1vY*yHq4YH
-> key sai. ta thấy để có đc kí tự đầu của flag ta lấy enc_flag[0] ^ key[0] và kết quả kí tự này là I <vì form flag là: ISPCTF{...}>
vậy enc_flag[0]^key[0]=int('I'). tương tự ta có được các giá trị key còn lại
mặt khác độ dài của enc-flag > flag 5 đơn vị nên ta thêm 5'X' và chuỗi flag

2. đạon code để tìm ra giá trị đúng của key:
```
#include <iostream>
using namespace std;

int main() {
    int enc_flag[] = {82, 89, 71, 65, 80, 64, 96, 82, 39, 112, 91, 69, 42, 122, 127, 49, 118, 89, 42, 121, 72, 113, 52, 89, 72, 59, 122, 114, 104, 53, 102};
    string s="ISPCTF";
    for (int idx = 0; idx < 6; idx++) {
        cout<<(enc_flag[idx]^s[idx])<<" ";
    }
    return 0;
}
```

3. đoạn code được sửa lại như sau:
```
#include <iostream>
using namespace std;

int main() {
    int enc_flag[] = {82, 89, 71, 65, 80, 64, 96, 82, 39, 112, 91, 69, 42, 122, 127, 49, 118, 89, 42, 121, 72, 113, 52, 89, 72, 59, 122, 114, 104, 53, 102};
    int key[] = {27, 10, 23, 2, 4, 6};
    string flag = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX";
    int lenKey = 6;
    cout<<sizeof(enc_flag)/sizeof(int)-sizeof(flag)/sizeof(char);
    for (int idx = 0; idx < flag.length(); idx++) {
        flag[idx] = enc_flag[idx] ^ key[idx % lenKey];
    }

    cout << "Decrypted Flag: " << flag << endl;
    return 0;
}
```
4. kết quả in ra là: Decrypted Flag: ISPCTF{X0r_C1ph3r_1s_s0_S1mpl3}
