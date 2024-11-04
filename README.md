Làm theo các bước sau:
### Bước 1: Tạo key
Tạo các key: platform, media, networkstack, shared, bluetooth, cts_uicc_2021, nfc, sdk_sandbox, testkey
1. **Tạo khóa riêng tư (Private Key) và xuất file `.pk8`**:
   Sử dụng lệnh sau để tạo một khóa RSA 2048-bit và lưu nó dưới dạng file `.pk8`:
   ```bash
   openssl genpkey -algorithm RSA -out platform.pk8 -outform DER -pkeyopt rsa_keygen_bits:2048
   ```
2. **Tạo chứng chỉ x509 và lưu thành file `.x509.pem`**:
   Sử dụng khóa `.pk8` vừa tạo để tạo một chứng chỉ tự ký (self-signed) dạng x509 và lưu vào file `.x509.pem`:
   ```bash
   openssl req -new -x509 -keyform DER -key platform.pk8 -outform PEM -out platform.x509.pem -days 10000
   ```
### Bước 2: Ghi đè bộ key
Ghi đè bộ key này vào đường dẫn: `build/make/target/product/security`
### Bước 3: Tạo bản 101
 ```bash
    Sửa nội dung file: `build/make/tools/buildinfo.sh`
```
### Bước 3: Build lại bản phần mềm
Thực hiện build lại bản phần mềm mới với yêu cầu chạy lệnh:
```bash
source build/envsetup.sh
croot
make clean
brunch bluejay
```