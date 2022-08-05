## Profile và level trong mã hóa video

### 1. Profile và level trong mã hóa video.

Khái niệm về profile và level trong lĩnh vực nén video xuất hiện lần đầu tiên trong chuẩn nén MPEG2-Part2(video)/H.262, đây là chuẩn nén đầu tiên có sự hợp tác giữa ITU-T và ISO/IEC.

ITU-T phát triển và sử dụng các kỹ thuật nén video hướng đến ứng dụng về truyền thông, về đàm thoại, video hội nghị … do đó thường ưu tiên các tính năng như độ trễ thấp (low delay), bền vững và dễ dàng khôi phục với nhiễu, tính phức tạp các công cụ mã hóa thấp (do thường sử dụng trên các thiết bị có hiệu năng xử lý thấp).

Trong khi đó ISO/IEC lại thiên về các ứng dụng về truyền hình, broadcast television, lưu trữ nội dung video số. Thành ra ISO/IEC ưu tiên hơn về các kỹ thuật nén để có thể đạt mức độ nén cao, độ phân giải lớn, không ưu tiên nhiều tài nguyên hệ thống (toàn các thiết bị chuyên dụng trâu chó).

Vì lý do trên để MPEG2-Part.2/H.262 để có thể thỏa mãn yêu cầu của cả 2 tổ chức, thì khái niệm profile & level được đưa ra, nhằm phân chia toàn bộ công cụ mã hóa trong đặc tả kỹ thuật chung thành các tập hợp con phù hợp với từng ứng dụng, đồng thời cũng tránh việc lãng phí không cần thiết, kiểu như dùng búa tạ để đập ruồi.

Dễ hiểu nhất có thể hình dung nôm na giống như có rất nhiều loại dao, dao thái thịt, dao mổ gà, dao bổ củi …Profile sinh ra để phân loại ứng loại dao đó. Trong mỗi loại dao, ví dụ dao thái thịt thì có loại to, loại nhỏ và để sắp xếp kích cỡ thì khái niệm level được sinh ra. Tất nhiên nếu có thể thì tồn tại một số dao đa năng, cái gì cũng chiến, nhưng như thế không hiệu quả và còn gây lãng phí không cần thiết (đi mổ gà thì không cần thiết dùng đến cả loại dao có thể xử lý được trâu bò). 

### 2. Vấn đề tương thích

Với decoder, để có thể nói được bản thân nó hỗ trợ profile & level nào, thì bắt buộc bộ decoder đó phải hỗ trợ toàn bộ các công cụ mã hóa được giới hạn bởi profile & level đó. Về phía encoder trong giới hạn profile & level thì nó có thể lựa chọn công cụ mã hóa trong đó để thực hiện, không cần thiết (mà cũng hiếm khi) sử dụng hết toàn bộ.

Do đó thông tin về decoder chỉ cần profile & level là đủ biết phạm vi nó hỗ trợ, còn encoder thì cần kèm theo chi tiết nó đã hỗ trợ những công cụ mã hóa nào, mới biết chính xác khả năng của nó.

### 3. Profile

Profile sẽ phân loại và giới hạn các công cụ mã hóa thành các tập con, tương ứng với từng ứng dụng khác nhau.

Tuy nhiên ở trong đặc tả chuẩn nén thì sẽ miêu tả cụ thể giá trị trong luông dữ liệu (bitstream) thông qua đó sẽ giới hạn các công cụ mã hóa của profile tương ứng. Do đó nếu từ đặc tả mà không có hiểu biết tương đối trước thì rất khó hiểu được với giá trị đó sẽ hạn chế công cụ mã hóa nào nếu không dành thời gian điều tra.

Xem xét kỹ với chuẩn H.264 [1] phiên bản (version) 12.0, ở mục A.2 miêu 15 profile khác nhau. Baseline Profile phù hợp với các ứng dụng cần độ phức tạp không cao, cần đảm bảo độ trễ thấp (không support slide B, nguồn gốc lớn nhất gây ra độ trễ do làm đảo thứ tự hiện thị) kiểu như các ứng dụng đàm thoại, truyền thông video trên mobile.

Sau phiên bản đầu tiên đưa ra sử dụng thì 2 công cụ mã hóa FMO, ASO rất ít được sử dụng, do hiệu quá không cao, mà cách thực thi thì phức tạp, loại bỏ 2 công cụ này đã tạo ra Constrained Baseline Profile.

Extended Profile được xây dựng dựa trên Constrained Baseline Profile bằng cách đưa thêm các công cụ mã hóa dành cho network streaming (truyền video qua mạng?). Main Profile dành cho các ứng dụng giải trí, như truyền hình kỹ thuật số, DVD player.

Hight Profile ưu tiên các công cụ mã hóa để có thể thực hiện nén video mức độ cao nhất, hỗ trợ nhiều không gian màu gồm cả YUV 444 (High 4:4:4 Profile) và mở rộng độ rộng bit lên 10 bit (High 10 Profile), do đó nó hướng đến các ứng dụng video cần độ phân giải cao.

Intra Profile chắc sẽ là profile buồn cười nhất nếu không hiểu về vấn đề ứng dụng, là profile chỉ hỗ trợ ảnh I, tức là không hỗ trợ công cụ đưa đến độ nén nhiều nhất là dự đoán liên khung (inter prediction), các kỹ thuật về bù trừ chuyển động xem như quảng đi hết. Tuy nhiên đây là profile hướng đến các ứng dụng chuyên nghiệp trong xử lý video ví dụ bên video editing, làm phim chuyên nghiệp, khi yêu cầu có thể dễ dàng chỉnh sử từng hình ảnh, mà chẳng cần ưu tiên cao về dung lượng lưu trữ.

### 4. Level
Level sẽ đưa ra giới hạn về kích thước khung hình, khả năng xử lý, bộ nhớ (memory), tốc độ truyền data phù hợp với ứng dụng đó. Ví dụ với mobile màn hình HD thì không cần thiết phải sử dụng bộ decoder có thể support lên tới FHD, lãng phí không cần thiết.

Có thể tham khảo thêm bảng “Table A-1 – Level limits” ở đặc tả của chuẩn H.264 có miêu tả kỹ càng giới hạn ứng với từng level như là giới hạn số Macroblock xử lý trong 1 giây, giới hạn kích thước khung hình, tốc độ bit tối đa, giới hạn buffer sử dụng tham chiếu …

### Tài liệu tham khảo
- [1] https://www.itu.int/rec/T-REC-H.264
- [2] http://iphome.hhi.de/wiegand/assets/pdfs/h264-AVC-Standard.pdf
- [3] http://blog.mediacoderhq.com/h264-profiles-and-levels/
- [4] https://www.vocal.com/video/profiles-and-levels-in-h-264-avc/
- [5] https://en.wikipedia.org/wiki/MPEG-2
- [6] THE H.264 ADVANCED VIDEO COMPRESSION STANDARD Second Edition, Iain E.Richardson

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />