## Rate control in video coding

### 1. Rate control là gì.
Cụm từ này không biết nên dịch sang tiếng việt thế nào, nên thôi tạm để nguyên từ gốc của nó.
Rate control là một trong những phần quan trọng nhất trong bộ encoder để quyết định video sau khi nén có đạt được bitrate đúng yêu cầu hay không. Ngoài ra nó còn có ảnh hưởng rất lớn đến việc giữ cho chất lượng của các hình ảnh (picture) trong video sau khi nén, có được sự ổn định, chất lượng đồng đều nhau.
Đây thuộc phần tốn rất nhiều mồ hôi và cả “chửi tục” của các kỹ sư trong quá trình phát triển video encoder. Do việc có được một xử lý rate control tốt cần rất nhiều thời gian, cũng như cần người giàu kinh nghiệm để có thể hiệu chỉnh được các hệ số hợp lý, và rất nhiều trường hợp mong muốn ra con bò thì nó ra con dê.

Các bộ encoder gần như được tự do sử dụng các phương pháp, các chiến lược (strategy) cho rate control, vì vấn đề này xem như nằm ngoài phạm vi phủ sóng của đặc tả chuẩn nén.

### 2. Vai trò của rate control.
Một bộ encoder khi thực hiện nén video luôn xác định mức độ cần nén là bao nhiêu, việc này được bởi yêu cầu bitrate đầu vào. Dựa trên thông tin đó, rate control sẽ quyết định mức độ nén của video, mà mang tính chất quyết định nhất là giá trị QP (Quantilization Parameter: Thông số lượng tử), con số này càng cao thì độ nén video càng lớn, và tất nhiên được cái lọ thì phải bỏ cái chai, độ mất mát thông tin cũng lớn theo tức là chất lượng video sẽ kém đi.

Ngoài giá trị độ lớn thì mỗi mảng ứng dụng lại có một yêu cầu riêng về thuộc tính đối với bitrate, ví dụ broadcast video thì thường yêu cầu bitrate cố định (constant bitrate, dĩ nhiên cũng chỉ là tương đối thôi), với IP television thì lại cho phép bitrate có thể thay đổi trong một phạm vi giới hạn.

Quay lại về việc thực hiện nén video, một điều hiển nhiên là các ảnh trong một luồng video luôn có mức độ nén không giống nhau, ảnh I sẽ có size (dung lượng) lớn hơn ảnh P,B, do 2 ảnh này được phép sử dụng tham chiếu đến ảnh khác, nên độ nén tăng lên đáng kể. Trong khi đó frame rate (số hình ảnh được hiển thị trong 1 giây) thường là cố định, do đó nếu không có sự điều chỉnh hợp lý thì bitrate sẽ thay đổi không phù hợp với ứng dụng tương ứng. Đây là nhiệm vụ cơ bản của rate control.

Về vấn đề ổn định chất lượng, nếu xem video lúc thì hình ảnh rõ nét, lúc thì xấu như ma lem thì thà xấu toàn bộ chắc xem còn dễ chịu hơn. Rate control cũng là nhân tố quan trọng trong vấn đề này. Do rate control liên tục điều chỉnh độ nén của từng ảnh liên tiếp để thỏa mãn yêu cầu bitrate, nhưng nó cũng phải ràng buộc để các ảnh liên tiếp nhau chất lượng không quá khác nhau nhiều quá, tránh tạo ra video dek thằng nào muốn xem. Một video tốt cần có chất lượng đồng đều nếu có thay đổi cũng nhẹ nhàng như chứng khoán chứ không được đột biến như đồ thị bitcoin. Dĩ nhiên đến làm được điều này thì không chỉ mỗi rate control mà còn các xử lý khác, nhưng có thể nói rate control là con bài át chủ.

### 3. Rate control làm việc như thế nào.
Trên thực tế cũng như lý thuyết đây là một phạm vi rất rộng, vì rate control thực ra là một mô hình dự đoán trước để quyết định tham số nén quan trọng là QP, do đó với mỗi chuẩn nén khác nhau lại cần một phương pháp khác nhau. Mỗi khi một chuẩn nén ra đời lại kéo theo một mớ chuyên gia mò ra chiến lược rate control phù hợp, âu cũng là tạo công ăn việc làm cho xã hội.

Trong ứng dụng thực tế, phải chấp nhận điểm cân bằng giữa chất lượng rate control đạt được và độ phức tạp của nó. Thậm chí có nhiều bộ encoder còn sử dụng luôn giá trị cố định QP cho từng loại picture.

Về cơ bản có thể hiểu một cách đơn giản thì rate control diễn ra như hình vẽ dưới. (Chú ý các khái niệm GOP, I,P,B picture đang hiểu theo định nghĩa của MPEG2-Video. Đây là khái niệm cơ bản cần nắm vững nên sẽ có bài ôn lại về cái mớ lộn xộn này sau).

![rate1]((/assets/2018/04/rate1.png))

GOP là 1 nhóm picture có tính lặp đi lặp lại trong một chuỗi video, do đó rate control thường đi theo đơn vị là GOP.

- Bước 1: Ở lớp GOP, từ bitrate và frame rate thì dễ dàng tính được cần nén 1 GOP đạt được size bao nhiêu. Nếu GOP này là xuất phát của video thì cứ theo giá trị đó sử dụng, nếu không thì cần cân nhắc bù trừ vớ sai lệnh của GOP trước đó.

- Bước 2: Mỗi GOP thông thường có 1 ảnh I và số lượng ảnh P,B cố định. Từ size của GOP sẽ ước lượng được size ảnh I,P,B mà bộ nén cần đạt được, tất nhiên có cân nhắc đến độ lớn của ảnh I,P,B bằng các hệ số, mà hệ số này liên tục được thay đổi sau mỗi lần thực hiện nén ảnh để đảm bảo dần dần có độ chính xác nhất.
Từ size của mỗi ảnh, ví dụ ảnh I thì rate control sẽ dựa vào mô hình ước lượng đển ước tính giá trị QP của ảnh I đó.

- Bước 3: Từ size của ảnh, tiếp tục ước lượng giá trị size của MB(macroblock) cần đạt được, kết hợp với giá trị QP ở bước 2 sẽ ước lượng ra được giá trị QP của MB đó.

Sau bước 3 thì MB đã đủ điều kiện và sang bước tiếp theo để thực hiện chính thức nén. Sau khi có kết quả size thực tế của MB đó sau khi nén thì rate control lại so sánh với size dự đoán, dựa vào độ sai lệch đó để bù vào MB tiếp theo và cập nhật lại thông số mô hình dự đoán. Quá trình này tiếp diễn lên đến lớp GOP.

Tuy nhiên đời không như mơ, thực tế thì có những bộ encoder mà GOP có thể thay đổi, số ảnh trong GOP không cố định. Hay là có những vị trí chuyển cảnh (scene change), hay mức độ sai khác với ảnh trước rất lớn (fade in/out) thì nếu điểm đó là ảnh P, thì ngay cả ảnh P cũng cần chọn giảm hệ số nén để giữ chấp lượng vì sẽ ảnh hưởng lớn đến các ảnh sau. Do đó tùy sự ưu tiên của từng bộ encoder mà chiến lược rate control khác nhau.

### 4. Tương thích với đặc tả.
Mặc dù rate control là phạm vi nằm ngoài đặc tả chuẩn nén video, nhưng chuẩn nén cũng có một số ràng buộc tương đối khi kiểm tra video đó có tương thích với bộ decoder hay không.
Ở các mục lục của đặc tả chuẩn nén, với H.264 thì ở Annex C Hypothetical reference decoder, đều đưa ra yêu cầu nhằm đảm bảo bộ decoder sẽ không bị mất data hay data không đến kịp đển thực hiện decode mặc dù nó đã thực hiện tuân theo đặc tả chuẩn nén.

Hình vẽ dưới miêu tả tình trạng CPB (Coded picture buffer: vùng nhớ chứa dữ liệu đầu vào của bộ decoder). Dữ liệu vào vùng nhớ này tăng tuyến tính (giả sử với constant bitrate) vì đến thời điểm ảnh nào được decode thì bộ decoder sẽ lấy ảnh đó ra khỏi bộ đệm. Do đó nếu ảnh quá lớn thì sẽ gây CPB bị underflow như vùng màu xanh, ảnh tiếp theo không kịp đến là cho quá trình play video bị giật. Ngược lại nếu ảnh quá nhỏ thì sẽ gây CPB overflow dễ gây mất dữ liệu đầu vào.

![hrd1](/assets/2018/04/hrd1.png)

Để xử lý vấn đề này thì ở encoder luôn có mô hình giả lập để đảm bảo size các ảnh luôn ở phạm vi cho phép mà không xẩy ra tình trạng trên. Đây cũng là một việc của rate control.

### 5. TM5 (test model 5).
Về phương pháp rate control cho đến H.264 có thể tham khảo tài liệu [1], viết rất đầy đủ và chi tiết (tuy tác giả là của các chú Tàu khựa, nhưng mình nghĩ a/e nên đọc kỹ).
TM5 là chiến lược rate control cho MPEG2-Video, được giới thiệu vào 1993, tức là cách đây 25 năm. Đến hôm nay thì vẫn có công ty sừng sỏ về video của Nhật Bản vẫn dùng cho H.264, H.265 tất nhiên kèm sau sự chỉnh sửa đang kể.
Tham khảo [3] để biết chi tiết hơn về phương pháp này.

6.Tài liệu tham khảo.
- [1] https://www.intechopen.com/books/recent-advances-on-video-coding/rate-control-in-video-coding
- [2] THE H.264 ADVANCED VIDEO COMPRESSION STANDARD Second Edition, Iain E.Richardson
- [3] http://www.mpeg.org/MPEG/MSSG/tm5/Ch10/Ch10.html

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />