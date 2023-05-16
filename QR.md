Một nửa còn lại của mã QR đang ở đâu???
https://ctf.infosecptit.club/files/c0bd418ea92472b5bf342d7a0fec67b1/haidz.png?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6MzV9.ZGLr2g.eeanvQmR7w9zSct3BODnQpt7xIY

1. mở file lên xuất hiện ảnh QR bị cắt mất 1 nửa -> ảnh bị chỉnh sửa độ dài ở mã hex
2. check file thấy có độ rộng 2100 (hex: 08 34), dài 1000 (hex: 03 e8) (tool: kt.gy)
3. mở hxd lên sửa chiều dài để có hình ảnh trọn vẹn
4. Flag: ISPCTF{h4i_d3p_z4i_y34h_y34h}


