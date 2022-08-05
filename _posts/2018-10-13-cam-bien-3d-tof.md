## Cảm biến 3D – TOF

Từ khi ~ipornX~ Iphone X của Apple được giới thiệu, cảm biến 3D trở thành 1 hot keyword, làm cho nhà nhà đua nhau tích hợp 3D vào điện thoại, người người thi nhau mua điện thoại có cảm biến 3D. Ông trùm SONY về mảng điện tử một thời của Nhật, mà hiện giờ mảng cảm biến đang mang lại một trong những nguồn sống chính, đã nhanh chân mở ví ra mua luôn [Softkinetic](https://en.wikipedia.org/wiki/Softkinetic), một startup của Bỉ với tầm 77 nhân sự vào 2015.   
Tôi vô tình cũng bị cuốn vào xu thế đó khi tham gia dự án làm platform & driver cho con hợi này. Do đó vừa học vừa viết lại đôi điểm cho đỡ quên, nội dung rút ra từ tài liệu [1] ở phần tham khảo. Có thể học thêm về TOF ở kho tài liệu của Texas Instrument [2], rất phong phú và chi tiết.

Trong vấn đề xử lý hình ảnh, việc thu và tái hiện lại hình 3D không phải vấn đề gì mới, trước TOF đã có 2 phương pháp được sử dụng để tái tạo hình ảnh 3D.
- Stereo Vision : Sử dụng 2 camera để tái hiện lại 3D, vị trí của 1 điểm sẽ được xác định nhờ vị trí tương đối của nó đối với 2 camera. Phương pháp này sử dụng tương tự hệ thống mắt người.

![stereo-vision](/assets/2018/08/stereo-vision.png)  
Nguyên lý Stereo Vision (Ảnh lấy trong tài liệu[1])

- Structured-light: Phương pháp này sử dụng 1 chùm tia sáng với mô hình xác định trước (dạng lưới, quét ngang …) , để chiếu lên vật thể cần quan sát, thu lại hình ảnh khi tia sáng đập lên bề mặt vật thể để xây dựng lại hình ảnh 3D của nó.

![structure-ligh](/assets/2018/08/structure-ligh.png)  
Nguyên lý Structured-light  (Ảnh lấy trong tài liệu[1])

Vậy TOF là gì? so với 2 thằng ở trên thì TOF có gì khác? TOF là viết tắt của Time Of Flight, dựa trên nguyên lý đo khoảng cách bằng sóng điện từ (sóng ánh sáng ở dải mắt người không nhìn thấy). Trong hệ thống TOF, sử dụng 1 nguồn phát sóng ánh sáng, quan sát nguồn phản hồi từ đối tượng quan sát, bằng cách đo thời gian từ lúc phát ra đến lúc phản hồi thì sẽ tính được vị trí của đối tượng đó.

![tof](/assets/2018/08/tof.png)
Nguyên lý TOF (Ảnh lấy trong tài liệu[1])

Dễ thấy nguyên lý của TOF giống hệt như dùng sóng siêu âm để đo độ sâu đáy biển, tất nhiên từ lý thuyết đến thực tiễn là 1 khoảng cách không nhỏ về thời gian cũng như tiền bạc.

Bảng dưới đây cho thấy hình ảnh tổng quan của TOF khi so sánh với 2 kỹ thuật còn lại. Công nghệ thay đổi chóng mặt chả khác gì “chó chạy ngoài đồng” , nên cần chú ý rằng thông tin trong bảng này chỉ đúng với tầm thời điểm hiện tại (~2018).

![tof](/assets/2018/08/tof1.png)  

So sánh TOF với Stereo Vision và Structured-light (Ảnh lấy trong tài liệu[1])

### Tham khảo:
- [1] http://www.ti.com/lit/wp/sloa190b/sloa190b.pdf
- [2] http://www.ti.com/3dtof
- [3] https://en.wikipedia.org/wiki/Structured_light
- [4] https://en.wikipedia.org/wiki/Time-of-flight_camera
- [5] https://en.wikipedia.org/wiki/Computer_stereo_vision

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />