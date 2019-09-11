# Booting

## 1. Booting là gì?

Để cho dễ hiểu Booting chính là quá trình khởi động của máy tính bắt đầu từ khi "Power UP" cho đến khi hệ thống khởi động hoàn tất (System running state). Toàn bộ quá trình booting có thể tham khảo ở hình bên dưới.

<img src="https://raw.githubusercontent.com/nyugennguyen/selfstudy/master/Linux-RoadtoLPI/Images/linux_bootprocess.png">

NVRAM(ROM) chứa firmware quản lý tất cả các thành phần Hardware trên máy tính, tùy thuộc vào dòng mainboard đang sử dụng mà firmware sử dụng BIOS hay UEFI.
  > Note: trong một vài loại mainboard sau này sẽ gọi BIOS là Legacy boot tùy thuộc vào nhà sản xuất để phân biệt giữa Legacy boot và UEFI.

  - BIOS viết tắt của Basic Input/Output System có thể coi như là phần sụn của hệ thống, được chứa trong bộ nhớ flash hoặc EEPROM trên mainboard. Khi máy tính được mở qua công tắc bật điện hay khi được nhấn nút power,thì BIOS được khởi động và chương trình này sẽ tiến hành các thử nghiệm khám nghiệm trên các ổ đĩa, bộ nhớ, bo hình, các con chip có chức năng riêng khác và các phần cứng còn lại.
  ###### Tham khảo Wiki [BIOS](src="https://vi.wikipedia.org/wiki/BIOS")

Hệ thống sẽ tự động load Boot loader(GRUB) nằm trong phân vùng ổ cứng được chỉ định . Các phiên bản Linux hiện thời đã hỗ trợ GRUB Version 2.
  
- GRUB (GRand Unified Bootloader) là một chương trình khởi động máy tính được phát triển bởi dự án GNU. GRUB cung cấp cho người dùng một lựa chọn cho phép khởi động một trong nhiều hệ điều hành được cài trên một máy tính hoặc lựa chọn một cấu hình hạt nhân cụ thể có sẵn trên các phân vùng của một hệ điều hành cụ thể.
  ###### Tham khảo Wiki: [GRUB](https://vi.wikipedia.org/wiki/GRUB)

Sau khi Bootloader hoàn tất loading boot image nó sẽ tự động khởi động Kernel đã được chỉ định.
 > Kernel chính là trái tim của hệ điều hành bởi lẽ nó sẽ tương tác với phần cứng và đảm nhiệm việc chạy các tiến trình nền(Daemon process), cũng như quản lý file, bộ nhớ,...

Kernel sẽ tự động chạy tiến trình nền với PID 1, với các phiên bản Linux trở về trước tiến trình nền này được gọi là Init sau này nó được thay đổi bởi với Systemd.

Tới đây thì việc khởi động đã gần như hoàn tất, sau khi chạy startup script và khởi động xong tất cả các tiến trình nền hệ điều hành của chúng ta đã sẵn sàng hoạt động.



