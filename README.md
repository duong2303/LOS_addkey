Làm theo các bước sau:
step1: tạo key platform, media, networkstack, shared, bluetooth, cts_uicc_2021, nfc,sdk_sandbox,testkey
    1. Tạo khóa riêng tư (Private Key) và xuất file .pk8
    Sử dụng lệnh sau để tạo một khóa RSA 2048-bit và lưu nó dưới dạng file .pk8:
        openssl genpkey -algorithm RSA -out platform.pk8 -outform DER -pkeyopt rsa_keygen_bits:2048
    2. Tạo chứng chỉ x509 và lưu thành file .x509.pem
    Sử dụng khóa .pk8 vừa tạo để tạo một chứng chỉ tự ký (self-signed) dạng x509 và lưu vào file .x509.pem:
        openssl req -new -x509 -keyform DER -key platform.pk8 -outform PEM -out platform.x509.pem -days 10000   
Step2: ghi đè bộ key này vào đường dẫn:build/make/target/product/security
Step3: Thực hiện build lại bản phần mềm mới với yêu cầu chạy lệnh 
    source build/envsetup.sh
    croot
    make clean
    brunch bluejay