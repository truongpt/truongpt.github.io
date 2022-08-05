## Zero start with video coding

### Hoàn cảnh éo le.
Ra trường giữa 2009, tham gia 1 dự án làm về DTV (Digital Television) đến tận đầu 2012, vậy là 2 năm rưỡi, biết được một chút về video decoding do đàn anh  chỉ dạy cho lúc bắt đầu dự án, còn lại OT vật vã cho kịp deadline. Sau này ngẫm lại thấy đa phần kiến thức cơ bản về video coding bị sai → quá nguy hiểm.\
Vào 7/2013 sang Nhật làm việc đến 4/2017 trong dòng dự án về 4k – Television và Camera recorder. Trong thời gian đó có tầm 1 năm rưỡi cuối làm về video encoding. Về công việc thì test nhiều hơn là code. Do  rảnh rỗi không biết làm gì, nên học thêm chút về video encoding cho qua ngày.
Rút ra được vài ba kinh nghiệm quí báu, khi làm việc trong cái mảng việc này (mảng khác chắc cũng thế).
- ① Nên theo từ lúc đang đi học, như thế sẽ được chỉ dạy kiến thức cơ bản bởi những người biết về kiến thức cơ bản.
- ➁ Nếu ko có cơ hội ①, khi vào dự án chiến luôn mà nghe trong team chém gió (sợ nhất là các thánh phán), phải điều tra cẩn thận trước khi coi đó là chân lý.
- ③ Cái số ➁ cực kì nguy hiểm, nếu không may mắn có cái ① thì nên tìm sư huynh cho thật ngon mà học, vừa nhanh vừa an toàn.\
Mình là nạn nhân con số ➁, sau nhiều năm mới sửa sai được một số vấn đề cơ bản, mà suýt bị nó làm cho tẩu hỏa nhập ma. Ngoài ra công việc gián đoạn không làm video coding nữa, nên giờ ngồi viết lại, lỡ sau này may mắn có cơ hội làm tiếp về video coding thì có chỗ mà tra cứu cho nhanh :-).

### Một vài điểm bắt đầu.
Có mail hỏi 1 ông anh, chuyên gia video coding ở Đức, thì đại ka gợi ý đọc quyển [này](http://iphome.hhi.de/wiegand/assets/pdfs/VBpart1.pdf). Mình nhai mãi chưa xong (vẫn tiếp tục nhai khi có thời gian), toàn kiến thức nền tảng, phù hợp cho ai thích đi theo hướng nghiên cứu. Còn giờ đang cần tiếp cận theo hướng ứng dụng.\
Bắt đầu một vài gạch đầu dòng cơ bản.
- Video thực ra là một chuỗi ảnh(picture) sắp xếp liên tục theo thời gian (có lẽ ai cũng biết?), vì vậy nén video chẳng qua là nén lần lượt các ảnh này.
- Nén video cơ bản là nén mất dữ liệu (lossly), nhưng bất kì chuẩn nén video nào cũng chứa 2 giai đoạn. Giai đoạn 1 nén lossly (transform + quantization) và giai đoạn 2 nén lossless (entropy coding). Một số chuẩn nén như AVC/H.264, HEVC/H.265… cho phép chỉ nén lossless bằng cách cho phép bỏ quá trình nén lossly.
- Xét ở đặc điểm sau khi nén của picture, có thể chia thành 2 loại kỹ thuật nén là INTRA (nén trong ảnh) & INTER (nén liên ảnh). INTRA là cách nén picture chỉ dựa vào thông tin chứa trong bản thân picture đó, ngược lại INTER có sử dụng thông tin các picture lân cận để thực hiện nén picture đó.
- Quá trình nén picture được thực hiện theo từng block có kích thước vuông giống nhau. Đối với chuẩn nén H.264 trở về trước gọi là Macroblock kích thước 16×16 pixel, còn đối với H.265 gọi là Coding Tree Unit và nó cho phép chọn từ 16×16 ~ 64×64 pixel. Với các chuẩn nén không phải của ISO or ITU-T, ví dụ VP8, VP9 của google, tên gọi các block đó có thể khác nhưng cơ bản đều mang ý nghĩa giống nhau.

Sẽ có rất nhiều thắc mắc, ví dụ INTRA & INTER được thực thi cụ thể thế nào? nó thể hiện thế nào trong quá trình xử lý các block trong từng picture?, google phát toàn ra 1 đống như motion vector nó nằm ở đâu trong khái niệm trên? vân vân và vân vân. Với một cơ số khái niệm, cùng với đống tài liệu trên mạng (rác cũng nhiều), vội vàng dễ bị chết đuối cho nên đừng vội tham lam, đi từ từ rồi sẽ đến.
- P/S: Kiến thức mình chia sẻ thuộc trường hợp số ➁, cẩn thận khi có ý định sử dụng nhé!

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />