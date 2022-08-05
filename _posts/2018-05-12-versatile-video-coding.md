## Versatile Video Coding

### 1. Tên gọi chuẩn nén video mới.
Cuộc cuộc họp thứ 10 diễn ra ở San Diego – Mẽo, từ 10~20/04/2018 của JVET, nhóm hợp tác để thiết kế chuẩn nén video mới của ISO/IEC và ITU-T, đã đánh dấu mốc quan trọng của dự án, khi toàn bộ các đề xuất công cụ nén bắt đầu được đánh giá, thảo luận để tích hợp vào đặc tả. Thêm vào đó tên của chuẩn video tiếp theo sau HEVC được chính thức đặt là VVC, viết tắt của cụm từ Versatile Video Coding, nghe có vẻ khá uyên bác, và trông nguy hiểm.
Bản thân ISO/IEC và ITU-T sẽ quản lý chuẩn nén bằng tên mã riêng của từng tổ chức nên thường có qui định rõ của mỗi bên, còn cái tên VVC một kiểu tên riêng của dự án, thường đặt do ngẫu hứng nên nó trở nên rất thú vị, mặc dù chỉ mang tính hình thức. Trước đó đã có ý kiến thảo luận muốn chấm dứt kiểu tên gọi xVC bằng một kiểu đặt tên mới, đại loại như đặt theo địa điểm mà đội JVET chưa bao giờ đặt chân tới là Antarctica (châu Nam Cực)… Tuy nhiên với tên gọi VVC thì ISO/IEC và ITU-T vẫn tiếp tục duy trì phong cách như 2 chuẩn video trước đây AVC, HEVC. Xem chừng tiếng anh khá phong phú.
Về quá trình thành lập dự án và cách làm việc có thể xem lại tại đây

### 2. Kết quả hiện tại và kế hoạch tiếp theo.
Hưởng ứng kêu gọi đề xuất, trong cuộc họp lần thứ 10 này 32 tổ chức (công ty, học viện, trường đại học) khác nhau đã công bố 46 đề xuất. Các công cụ mã hoá được đề xuất gồm có 22 thuật toán nén cho SDR (standard dynamic range) , 12 mục HRD (high dynamic range), và 12 đề xuất cho video 360.
Toàn bộ các đề xuất được thảo luận vào đánh giá, chi tiết có thể tham khảo ở tài liệu[1].

Kết quả hiện tại đã đạt được khả năng nén lên tới 40% so với HEVC. Bản đặc tả chuẩn nén phiên bản tạm đầu tiên đã được thiết lập[2].
Cuộc họp lần này cũng đã quyết định sử dụng test model mới có tên là VTM (Versatile Video Coding Test Model)[3] thay thế cho JEM. Bản chất VTM được tái cấu trúc từ JEM do Fraunhofer HHI[6] thực hiện và đề xuất. So với JEM thì VTM được cải thiện thiết kế phần mềm, hiệu năng, nên dễ dàng tích hợp các thuật toán đề xuất vào hơn, đồng thời cho phép disable/enable các coding tool lúc runtime trong khi đó JEM bắt buộc phải biên dịch lại giúp tăng hiệu suất làm việc.

Như vậy theo như kế hoạch lúc JVET đưa ra lúc kêu gọi các đề xuất[7] thì còn tầm 30 tháng nữa, phiên bản đặc tả chính thức sẽ ra mắt, cùng lúc với Olympic ở Tokyo.
- 2018/04 Test model selection process begins
- 2018/10 Test model selection established
- 2020/10 Final standard completed

### Tài liệu tham khảo.
- [1] http://phenix.it-sudparis.eu/jvet/doc_end_user/current_document.php?id=3489
- [2] http://phenix.it-sudparis.eu/jvet/doc_end_user/current_document.php?id=3538
- [3] http://phenix.it-sudparis.eu/jvet/doc_end_user/current_document.php?id=3539
- [4] http://blog.chiariglione.org/the-mpeg-machine-is-reasy-to-start-again/
- [5] http://www.streamingmedia.com/PressRelease/Versatile-Video-Coding-(VVC)-Project-Starts-Strong-with-the-Joint-Video-Experts-Team_47071.aspx
- [6] https://www.hhi.fraunhofer.de/en.html
- [7] https://www.itu.int/en/ITU-T/studygroups/2017-2020/16/Documents/video/JVET-H1002-CFP-VCBHEVC-Final-v6.pdf

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />