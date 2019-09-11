# Booting

## 1. Booting là gì?

Để cho dễ hiểu Booting chính là quá trình khởi động của máy tính bắt đầu từ khi "Power UP" cho đến khi hệ thống khởi động hoàn tất (System running state). Toàn bộ quá trình booting có thể tham khảo ở hình bên dưới.

<img src="https://raw.githubusercontent.com/nyugennguyen/selfstudy/master/Linux-RoadtoLPI/Images/linux_bootprocess.png">

### 1.1. System firmware

NVRAM(ROM) chứa firmware quản lý tất cả các thành phần Hardware trên máy tính, tùy thuộc vào đời và năm sản xuất dòng mainboard đang sử dụng mà firmware sẽ sử dụng BIOS hay UEFI.
  > Note: trong một vài loại mainboard sau này sẽ gọi BIOS là Legacy boot tùy thuộc vào nhà sản xuất để phân biệt giữa BIOS Legacy boot và UEFI.

  - **BIOS** viết tắt của Basic Input/Output System có thể coi như là phần sụn của hệ thống, được chứa trong bộ nhớ flash hoặc EEPROM trên mainboard. Khi máy tính được mở qua công tắc bật điện hay khi được nhấn nút power, thì BIOS được khởi động và chương trình này sẽ tiến hành các thử nghiệm khám nghiệm trên các ổ đĩa, bộ nhớ, bo hình, các con chip có chức năng riêng khác và các phần cứng còn lại.
  
  <img src="https://raw.githubusercontent.com/nyugennguyen/selfstudy/master/Linux-RoadtoLPI/Images/bios.PNG">

  ###### Tham khảo Wiki [BIOS](src="https://vi.wikipedia.org/wiki/BIOS")

  - **UEFI** viết tắt của Unified Extensible Firmware Interface dịch là "Giao diện firmware mở rộng hợp nhất" là công nghệ thay thế cho BIOS đã có phần lỗi thời.
  - UEFI là một hệ điều hành tối giản "nằm trên" phần cứng (hardware) và firmware của máy tính. Thay vì được lưu trong firmware giống như BIOS, chương trình UEFI được lưu trữ ở thư mục /EFI/ trong bộ nhớ non-volatile (là bộ nhớ đảm bảo cho dữ liệu không bị hỏng mỗi khi mất điện). Vì vậy, UEFI có thể chứa trong bộ nhớ flash NAND trên bo mạch chính (mainboard) hoặc cũng có thể để trên một ổ đĩa cứng, hay thậm chí là ngay cả trên một vùng tài nguyên mạng được chia sẻ (network boot). UEFI sẽ giúp quá trình khởi động an toàn hơn nhờ tính năng Secure Boot

  <img src="https://raw.githubusercontent.com/nyugennguyen/selfstudy/master/Linux-RoadtoLPI/Images/UEFI.png">

  ###### Tham khảo Wiki [UEFI](src="https://vi.wikipedia.org/wiki/UEFI")

### Vậy tại sao lại thay thế BIOS bằng UEFI?
  - Đầu tiên là UEFI cung cấp 1 giao diện đồ họa, trực quan và nhiều option hơn cho người dùng cũng như người quản trị hệ thống, tiện lợi trong việc cấu hình.
  - UEFI hỗ trợ việc sử dụng ổ cứng lớn hơn 2TB, trong khi BIOS không hỗ trợ những ổ cứng với dung lượng lớn.
  - UEFI hỗ trợ network troubleshooting và khả năng kết nối mạng tích hợp sẵn bởi OEM.
  - UEFI hoạt động nhanh, hiệu quả và rút ngắn thời gian khởi động do BIOS chỉ chạy ở chế độ xử lý 16-bit với  1MB memory. Nó sẽ gặp sự cố khi khởi tạo nhiều thiết bị phần cứng cùng lúc, dẫn đến tốc độ khởi động chậm khi khởi tạo tất cả các môi trường và thiết bị phần cứng trên những hệ thống PC hiện đại.
  - UEFI hỗ trợ tương thích ngược với những hệ điều hành cũ chưa hỗ trợ UEFI (Legacy boot), secure boot giúp việc khởi động máy tính an toàn hơn.

### 1.2. Boot loader 
Hệ thống sẽ tự động load Boot loader(GRUB) nằm trong phân vùng ổ cứng được chỉ định . Các phiên bản Linux hiện thời đã hỗ trợ GRUB Version 2.
  
- GRUB (GRand Unified Bootloader) là một chương trình khởi động máy tính được phát triển bởi dự án GNU. GRUB cung cấp cho người dùng một lựa chọn cho phép khởi động một trong nhiều hệ điều hành được cài trên một máy tính hoặc lựa chọn một cấu hình hạt nhân cụ thể có sẵn trên các phân vùng của một hệ điều hành cụ thể.
  ###### Tham khảo Wiki: [GRUB](https://vi.wikipedia.org/wiki/GRUB)

Sau khi Bootloader hoàn tất loading boot image nó sẽ tự động khởi động Kernel đã được chỉ định.

### 1.3. Kernel
 > Kernel chính là trái tim của hệ điều hành bởi lẽ nó sẽ tương tác với phần cứng và đảm nhiệm việc chạy các tiến trình nền(Daemon process), cũng như quản lý file, bộ nhớ,...

Kernel sẽ tự động chạy tiến trình nền với PID 1, với các phiên bản Linux trở về trước tiến trình nền này được gọi là Init sau này nó được thay đổi bởi với Systemd.

Tới đây thì việc khởi động đã gần như hoàn tất, sau khi chạy startup script và khởi động xong tất cả các tiến trình nền hệ điều hành của chúng ta đã sẵn sàng hoạt động.



