# Booting

## 1. Booting là gì?

Để cho dễ hiểu Booting chính là quá trình khởi động của máy tính bắt đầu từ khi "Power UP" cho đến khi hệ thống khởi động hoàn tất (System running state). Toàn bộ quá trình booting có thể tham khảo ở hình bên dưới.

<img src="https://raw.githubusercontent.com/nyugennguyen/selfstudy/master/Images/linux_bootprocess.png">

NVRAM(ROM) chứa firmware quản lý tất cả các thành phần Hardware trên máy tính, tùy thuộc vào dòng mainboard đang sử dụng mà firmware sử dụng BIOS hay UEFI. Sự khác biệt giữa 2 loại system firmware sẽ được nói chi tiết sau.
  > Note: trong một vài loại mainboard sau này sẽ gọi BIOS là Legacy boot tùy thuộc vào nhà sản xuất để phân biệt giữa Legacy boot và UEFI

