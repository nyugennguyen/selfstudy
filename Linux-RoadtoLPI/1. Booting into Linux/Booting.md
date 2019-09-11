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

**Boot loader** có nhiệm vụ chính là nhận dạng và khởi động kernel hệ điều hành. Hầu hết các boot loader đều hỗ trợ một giao diện UI đơn giản để người dùng có thể chọn lựa kernel hoặc hệ điều hành được cài đặt trên máy ở đây chúng ta sẽ quan tâm tới boot loader mặc định của hệ điều hành Linux. 
Sau khi pass qua quá trình khởi động system firmware, Boot loader(GRUB) nằm trong phân vùng ổ cứng được chỉ định sẽ chạy một cách tự động. Các phiên bản Linux hiện thời đã hỗ trợ GRUB Version 2.
  
- GRUB (GRand Unified Bootloader) là một chương trình khởi động máy tính được phát triển bởi dự án GNU. GRUB cung cấp cho người dùng một lựa chọn cho phép khởi động một trong nhiều hệ điều hành được cài trên một máy tính hoặc lựa chọn một cấu hình hạt nhân cụ thể có sẵn trên các phân vùng của một hệ điều hành cụ thể.
  ###### Tham khảo Wiki: [GRUB](https://vi.wikipedia.org/wiki/GRUB)

> Note: Hệ điều hành FreeBSD có boot loader riêng tuy nhiên nó hoàn toàn có thể sử dụng GRUB như là boot loader mặc định nhất là trong trường hợp người dùng cài nhiều hệ điều hành trên cùng một máy tính, nếu như bạn không có nhu cầu thì boot loader mặc định của FreeBSD cũng đã hoàn toàn có thể đáp ứng nhu cầu sử dụng thông thường.

Quay lại với GRUB, GRUB hoàn toàn có thế được cấu hình bằng việc thay đổi cấu hình mặc định trong file grub.cfg, file này thường đặt trong *boot/grub* hoặc *boot/grub2* trong hệ điều hành Redhat/Centos.
 - Bạn có thể tự tạo file grub.cfg bằng cách generate sử dụng grub-mkconfig (update-grub đối với hệ điều hành Debian và Ubuntu). Việc tạo ra file này có thể đơn giản thực hiện bằng việc chỉnh sửa các cấu hình có sẵn trong file /etc/default/grub sau đó chạy grub-mkconfig để biên dịch ra file grub.cfg mới.
 - Để thay đổi thứ tự khởi động kernel được list ra trong boot menu hoặc để set boot password,.... Chúng ta cần chỉnh sửa file /etc/grub.d/40_custom. Sau khi chỉnh sửa xong ta lại chạy file grub-mkconfig để biên dịch ra file config mới.
 - GRUB hỗ trợ việc sử dụng command line trong thời gian boot, để bật giao diện command line ta phải ấn "c" khi đang trong giao diện GRUB boot screen. Các câu lệnh GRUB tham khảo tại [GNU.org](src= "http://www.gnu.org/software/grub/manual/grub/").
 - Nhờ việc cho phép thay đổi và lựa chọn kernel trước khi tiến hành khởi động OS, sysadmin có thể dễ dàng hơn trong việc update các bản vá cho kernel hoặc thay đổi kernel mới mà không phải quá lo lắng trong trường hợp OS không khởi động được. Hãy luôn nhớ tạo 1 kernel backup trong mọi thời điểm và trong trường hợp bản vá mới nhất không hoạt động hãy chạy lại phiên bản kernel trước đó (Stable version).

Sau khi Bootloader hoàn tất loading boot image nó sẽ tự động khởi động Kernel đã được chỉ định.

### 1.3. Kernel & System Daemon Process
 **Kernel** chính là trái tim của hệ điều hành bởi lẽ nó sẽ tương tác với phần cứng và đảm nhiệm việc chạy các tiến trình nền(Daemon process), cũng như quản lý file, bộ nhớ,...

Kernel sẽ tự động chạy tiến trình nền với PID 1, với các phiên bản Linux trở về trước tiến trình nền này được gọi là Init sau này nó được thay đổi bởi với Systemd.

Tới đây thì việc khởi động đã gần như hoàn tất, sau khi chạy startup script và khởi động xong tất cả các tiến trình nền hệ điều hành của chúng ta đã sẵn sàng hoạt động.



