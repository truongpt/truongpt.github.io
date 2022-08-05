## Phân biệt “video codec” và “video coding format”

Khi bàn về việc nén video thường có sự nhầm lẫn giữa video codec và video coding format (chuẩn nén video). Sự nhầm lẫn này thường thấy trong bộ phận kỹ sư liên quan đến phát triển sản phẩm mã hóa video, chứ không phải trong lĩnh vực nghiên cứu (đã đi nghiên cứu thì chắc chả thằng nào nhầm) . Hầu hết đều mặc định video codec chính là video coding format, do đó nhiều lúc sinh ra những nhầm lẫn về mặt kiến thức cơ bản, không đáng để xẩy ra do đó cũng nên phân biệt rõ ràng.

### 1. Video coding format.
“Video coding format” hay còn gọi là “video compression format” tạm dịch tiếng Việt là chuẩn mã hoá video ( riêng chữ video không biết dịch tiếng Việt là gì luôn :D), là tài liệu miêu tả cách biểu diễn dữ liệu dùng để mã hoá video. Nói một cách dễ hiểu hơn là dựa vào tài liệu đặc tả thì có thể giải mã một tệp (hoặc 1 luồng dữ liệu) video để tạo ra một chuỗi hình ảnh, sẽ phục vụ cho việc hiển thị.

Một chú ý quan trọng là dựa vào tài liệu đặc tả video chỉ chắc chắn có thể thực hiện được quá trình giải mã, còn chiều thực hiện mã hoá thành dữ liệu nén video, ngoài đặc tả chuẩn video thì một số quá trình cho phép mỗi cách thực hiện cho thể tự tối ưu bằng những thuật toán khác nhau, ví dụ như quá trình xử lý dự đoán chuyển động giữa các hình ảnh, quá trình chọn mức độ nén để đảm bảo đầu ra được tối ưu nhất (đạt được chất lượng tối ưu với ràng buộc của bitrate)…

Ví dụ về chuẩn H.264 và H.265 là các tài liệu đặc tả lần lượt theo đường dẫn dưới.
- H.264(MPEG4-Part10): https://www.itu.int/rec/T-REC-H.264-201610-P/en
- H.265(MPEG H Part2): https://www.itu.int/rec/T-REC-H.265-201504-I/en

### 2. Video codec.
Chữ CODEC là kết hợp viết tắt của 2 chữ enCOder và DEcoder, từ đó có thể hiểu đơn giản video codec bao gồm video encoder và video decoder (trên thực tế thì chỉ cần Decoder hoặc Encoder đã có thể gọi là codec), tức là một chương trình  thực hiện quá trình mã hóa và giải mã hóa, việc thực hiện như thế nào thì phụ thuộc vào chương trình đó thực hiện dựa trên video coding format nào.

Nói cách khác thì video codec là cách thức thực thi mã hoá hoặc giải mã video theo tài liệu đặc tả, ví dụ với đặc tả H.264 thì có rất nhiều video codec như x264 được phát triển với Videolan hay openh264 được phát triển bởi cisco, hay kiểu tên gọi codec của Sony trong các thiết bị sản xuất bởi Sony, codec của Apple trong Iphone, Ipad …

Do đặc tả chuẩn video ràng buộc chi tiết về quá trình giải mã, do đó phần giải mã trong video codec cho dù được thực hiện bởi chương trình nào thì cũng phải cho ra một kết quả giải mã giống nhau, nhưng quá trình mã hoá, ngoài phần bắt buộc tuân theo chuẩn mã hoá thì còn có phần cho phép mỗi chương trình tự tối ưu theo nhu cầu riêng để đạt được bộ mã hoá (encoder) tối ưu, thường là đạt chất lượng tốt theo hạn chế của hiệu năng hệ thống và yêu cầu bitrate.

Ví dụ về video codec theo chuẩn H.264 & H265..
- x264: http://www.videolan.org/developers/x264.html
- x265: http://x265.org/

### 3.Tài liệu tham khảo.
- [1] https://en.wikipedia.org/wiki/Video_coding_format
- [2] https://en.wikipedia.org/wiki/Video_codec
- [3] THE H.264 ADVANCED VIDEO COMPRESSION STANDARD – Iain E. Richardson

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />