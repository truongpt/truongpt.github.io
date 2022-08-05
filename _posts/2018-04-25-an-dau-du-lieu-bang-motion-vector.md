## Ẩn dấu dữ liệu bằng motion vector

### 1. Information Hiding, Digital Watermarking and Steganography
Đây là các khái niệm nói việc việc mã hóa, nhúng thông tin vào trong đối tượng (có thể là picture, audio, video …), có liên quan đến vấn đề bảo mật thông tin, hoặc bảo vệ bản quyền.
Đây là vấn đề rộng, chỉ đưa ra keyword chứ không dám lạm bàn, kẻo thành nói ngu, mà nói ngu thì cực kì nguy hiểm cho cả bản thân với ai đó chưa biết mà không may đọc phải.

### 2. Ẩn dấu dữ liệu bằng motion vector
Motion compensation (bù chuyển động) là thuộc loại công cụ nén quan trọng và mang về tỉ lệ nén rất cao trong việc nén video.
Với các ảnh liên tiếp nhau, về cơ bản là đối tượng trong ảnh phần lớn giống nhau (trừ tình huống chuyển cảnh), chỉ khác nhau do vị trí của nó bị xê dịch. Kỹ thuật bù chuyển động đưa ra nhằm tận dụng đặc trưng này của luồng video, thay vì lưu lại toàn bộ ảnh thì nó chỉ lưu lại phần chuyển động của bằng các vector, gọi là motion vector. Dĩ nhiên là cả điểm khác nhau sau khi đã bù chuyển động (DPCM), nhưng sự khác nhau này đã giảm đi đáng kể sau khi có tính đến bù chuyển động. Trong việc nén video, thì quá trình tìm kiếm vùng giống nhau giữa các ảnh sẽ quyết định motion vector tối ưu.

![mv1](/assets/2018/04/mv1.png)

Vấn đề muốn đề cập ở đây, là ta có thể tận dụng chính bộ vector này để đồng thời mã hóa dữ liệu mong muốn trong quá trình nén video. Đầu tiên bộ encoder sẽ tìm motion vector tối ưu, trước khi đưa motion vector đó vào thực hiện nén video, thì chỉnh sửa nó một cách có chủ ý nhằm nhúng dữ liệu vào đấy, tất nhiên giá trị motion vector không còn tối ưu nữa, nên ảnh hưởng ít nhiều đến chất lượng video. Việc chỉnh sửa thế nào tuân theo 1 qui tắc nào đó mà chỉ có encoder, và tiết lộ cho bên decoder mà được phép nhận chia sẻ dữ liệu đó biết, bên phía decoder khi giải mã video đó thì dựa vào motion vector sẽ lấy được thông tin được ẩn dấu trong đó.
Để dễ hình dung có thể xem hình vẽ dưới.

![hidedata1](/assets/2018/04/hidedata1.png)

### 3. Thử chơi với H.264
Áp dụng cho H.264, bằng cách chọn một codec có sẵn nào đó, sửa motion vector theo 1 qui luật nhất định.
Để dễ dàng thực hiện thì sử dụng codec hàn lâm nhất jvt codec[2], cái này là codec do JVT sử dụng trong quá trình xây dựng chuẩn nén H.264.
Nếu xem xét motion vector nhỏ hơn 1 giá trị ngưỡng nào đấy (threshold value) thì sẽ sửa nó về giá trị nhỏ hơn hoặc bằng sqrt(2), tức là motion vector nhỏ hơn giá trị ngưỡng luôn có giá trị trong tập (0,0); (0,1) ; (1,0) ; (0,-1);(1,1)… Bằng cách qui định dữ liệu ứng với với các giá trị này thì ta có thể mã hóa 1 chuỗi bit nhị phân bằng motion vector (tham khảo file insert_data.c trong source code[3]).
Sau khi chỉnh sửa jvt codec[2], bộ codec mới của H.264 ở [[3]](https://github.com/truongpt/jm19.0_watermarking) đã hỗ trợ việc sử dụng motion vector để nhúng dữ liệu vào ở bộ encoder, còn bộ decoder thì có thể giải mã nó và lưu thành 1 file có kết quả giống như dữ liệu đã nhúng.

![h264_1](/assets/2018/04/h264_1.png)

Thông tin và cách sử dụng có thể tham khảo readme.txt của source code[3], khi thay đổi data video đầu vào như frame size, số frame thực hiện mã hóa … thì cần sửa lại file cấu hình (config) của bộ encoder cho phù hợp.

- Hạn chế: làm lâu rồi nên không nhớ, nhưng hình như khi nhúng data bằng cả motion vector trước và sau (backward & forward) thì có bug, ai đó fix hộ đi 😀 .

### Tài liệu tham khảo
- [1] https://en.wikipedia.org/wiki/Digital_watermarking
- [2] http://iphome.hhi.de/suehring/tml
- [3] https://github.com/truongpt/jm19.0_watermarking

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />