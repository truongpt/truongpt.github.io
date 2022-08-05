## Zero start with USB

### 1. Lược sử USB.
Viết tắt của chữ Universal Serial Bus, cái tên nói lên tất cả. Và không hổ danh với tên gọi, đây là chuẩn kết nổi phổ biến nhất, đã và đang thay thế dần các kết nối ngoại vi khác.
Đồ sộ về cả đặc tả lẫn mã nguồn (ví dụ USB stack trong Linux), nếu không phải thánh thì nên tiếp cận từ từ, tránh “đột-thức” (đột quị vì nhiều kiến thức cần nắm).

Lịch sử tóm gọn, có vẻ khi ứng dụng cách mạng nhất là USB Mass Storage(usb flash, thường gọi tắt là USB) bị lấn lướt bởi việc phát triển mạnh mẽ của điện toán đám mây(cloud) và các dịch vụ trực tuyến, thì USB 3.0 lại vùng lên, tuy chưa rõ có nên cơm cháo gì không.
- Khai sinh 1/1996: USB 1.0, Low Speed 1.5Mbit/s, Full Speed 12Mbit/s
- 04/2000: USB 2.0, High Speed 480Mbit/s
- 11/2008: USB 3.0, SuperSpeed 5Gbit/s
- 07/2013: USB 3.1, SuperSpeed+ 10Gbit/s
- 09/2017: USB 3.2, SuperSpeed+ 20Gbit/s

### 2. Lướt qua đặc tả USB.
Đầu tiên cần nắm đặc tả, vào [1] để lấy đặc tả. Đặt tả là một ma trận chữ nghĩa và khái niệm, nên đọc [3] để biết tiếp cận đặc tả, nếu lười đọc tiếng Anh thì đọc nội dung ở [4], của 1 blog rất có tâm. Ở đây chỉ giới thiệu các tiếp cập đặc tả phiên bản USB 2.0[2], tuy nhiên các chắc các phiên bản tiếp theo cũng có thể tiếp cận theo cách tương tự.
Đồ sộ quá nên cần nắm vững những câu thần chú cơ bản. Đây là chân lý, không bao giờ được buông. NHƯNG nó chỉ đảm bảo cho các phiên bản trước USB 2.0, về sau có thể có thay đổi, sử dụng cần tỉnh táo.
- USB là chuẩn giao tiếp đơn, chỉ có HOST(chủ) và DEVICE(thiết bị, client-khách) giao tiếp với nhau, không phải là giao thức mạng.
- DEVICE chỉ nghe và trả lời khi có lệnh từ HOST, kể cả trường hợp giao tiếp theo interrupt.

Về mặt đặc tính truyền dữ liệu, thì có 4 loại cơ bản:
- Control Transfers: Sử dụng để truyền command (lệnh) hoặc status (trạng thái), ở quá trình DEVICE bắt đầu kết nối với HOST.
- Bulk Data Transfers: Dùng kết nối truyền lượng dữ liệu lớn, không cho phép mất mát, ex: usb flash.
- Interrupt Data Transfers: Dùng cho kết nối đảm bảo tính phản ứng nhanh, ví dụ chuột, bàn phím…
- Isochronous Data Transfers: Dùng cho các kết nối có tính realtime, tốc độ ổn định, ex: Camera, Audio …

Song song với sự phát triển của các thiết bị nhúng　(embedded, lai tạp) thì sinh ra USB OTG (On-The-GO), cho phép nó có thể đóng vai trò HOST hoặc DEVICE. Việc lựa chọn vai trò quyết định trong quá trình đàm phán lúc kết nối.

### 3.Tài liệu tham khảo.
- [1] http://www.usb.org/
- [2] http://www.usb.org/developers/docs/usb20_docs/
- [3] https://www.beyondlogic.org/usbnutshell/usb3.shtml#USBProtocols
- [4] https://lazytrick.wordpress.com/category/usb/

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />