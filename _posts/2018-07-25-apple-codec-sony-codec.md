## Apple codec vs Sony codec

### 1. Vô đề.
Nghỉ hè dẫn vợ con đi chơi Fuji-Q, vùng dưới chân nói Phú Sỹ. Nhân dịp này mang con Handycam HDR-CX470 của Sony đi quay thằng ku chơi để về up lên cho các cụ ở nhà xem.
Vì không phải dân biết chơi Camcorder nên không có ý định review đánh giá con Handycam, chỉ là về xử lý thấy dung lượng file lớn quá, trong chừng mức có thể (về công cụ lẫn thời gian) thử xem qua xem các thánh Sony đang thiết kế bộ codec thế nào.
Vì đang dùng iphoneSE thần thánh, nên cũng tiện tay lướt qua xem Apple bí hiểm có gì khác không.

### 2. Công cụ sử dụng.
#### 2.1. FFMPEG.
Trong thế giới multimedia processing, thì ffmpeg thì quá nổi tiểng nên không cần giới thiệu chi tiết. Đây là công cụ mã nguồn mở (opensource) mạnh mẽ, hỗ trợ đủ mọi video/audio đến multimedia file format (container).

FFMPEG được bắt đầu từ hồi “em mong ước đến năm 2000″(nhưng chiến tranh không tàn mà còn sống khỏe) bởi [Fabrice Bellard](https://bellard.org/) (một trong những lập trình viên đẳng cấp nhất thế gian mà đang còn sống cho đến thời điểm hiện tại 07-2018) cho đến 2004. Sau đó được dẫn dắt bởi Michael Niedermayer Từ 2004 đến 2015.

Đến 13/03/2011, sau một thập kỉ phát triên, do không đồng quan điểm, một số thành viên nhóm phát triển (chắc ngộ Clean Code) muốn ưu tiên nâng cao chất lượng code & API. Các thanh niên đó đã tách thành dự án libav, vụ này gây ra bao nhiêu phiền hà cho cộng đồng :-(. Tuy nhiên các sửa đổi của libav vẫn được merger vào ffmpeg, có vẻ công việc này nhàm chán quá nên Michael Niedermayer đã từ chức leader vào 2015 [[4]](https://ffmpeg.org/pipermail/ffmpeg-devel/2015-July/176489.html).

Ffmpeg được release theo package cho từng os riêng. Nếu không có mục đích tham gia phát triển ffmpeg hoặc cần sửa đổi source code thì strong recommend là lên trang chủ down về mà dùng luôn, vì nó đã enable rất nhiều lib phụ thuộc.

#### 2.2. JM tool.
Trái ngược với ffmpeg, thì không nhiều người biết đến công cụ này, chắc chỉ sử dụng trong giới nghiên cứu về video coding, vốn dĩ đấy cũng là mục đích của nó chứ không phải hướng đến lĩnh vực ứng dụng. JM là viết tắt của Join Model (nghe tên hơi cà rốt), đây là h.264 codec (jvt codec),được nhóm JVT (nhóm hợp tác MPEG và VCEG) phát triển và dùng để xây dựng chuẩn nén h.264. Làm gì có codec nào có trước khi public chuẩn nén, nên dĩ nhiên nó dành quán quân về h.264 codec đầu tiên trên thế giới :-).

JM là full codec,  đầy đủ cả decoder lẫn encoder h.264. Sử dụng decoder của JM cho phép phân tích các thông tin chi tiết hơn về h.264.
JM có thể down trên trang chủ của ITU-T ở đây [[3]](https://www.itu.int/rec/T-REC-H.264.2-201602-I/en), theo README là có thể biên dịch ^^.

### 3. Thực hành.
#### 3.1. Chuẩn bị video.
Đặt HDR-CX470 ở chế độ 1080P, 60fps, quay video nhiều cảnh động để đảm bảo bộ encoder làm việc tích cực nhất có thể. Sẽ phân tích tầm 1 phút, thời gian đủ dài để bộ encoder ổn định, do đó cần quay hơn 1 phút.

ffmpeg command cắt lấy 1 phút đầu tiên.
```
ffmpeg -ss 00:00:00 -to 00:01:00 -i 20180718125711.MTS -c copy sony.mts
```

#### 3.2. Phân tích thông tin video cơ bản.
Cần tham khảo [document](https://www.ffmpeg.org/documentation.html) của ffmpeg để hiểu các thông tin trong khi phân tích.
- Đầu tiên là xem thông tin cơ bản nhất về các stream video/audio, bằng command dưới.
```
ffprobe -show_streams sony.mts
```

Từ output log, lấy ra một số giá trị như dưới.

![str1](/assets/2018/07/str1.png)   
![str2](/assets/2018/07/str2.png) 

Từ đó có thể rút ra được vài thông tin sau.
- Birate 27 Mbps
- High profile, level 4.2. xem ý nghĩa profile/level ở [7].
- Khi encode, chỉ sử dụng 1 picture để tham chiếu đối với tham chiếu liên ảnh. (Với level 4.2 thì h.264 support tối đa có thể tham chiếu đồng thời 4 ảnh).

Phân tích chi tiết hơn chút về thông tin từng ảnh.
```
ffprobe  -show_frames -select_streams v:0 sony.mts
```

Chỉ tập trung vào 2 thông tin khoanh đỏ.

![str3](/assets/2018/07/str3.png)

Thông tin này thay đổi theo từng picture, hình ở trên chỉ là picture đầu tiên.
Sau khi kiểm tra toàn bộ thông tin ở trên với tất cả các picture thì được như dưới.
Về pict_type thì thấy được cấu trúc I,P,P …I,P,P … Có 29 ảnh P giữa các ảnh I, không có ảnh B.
- → GOP có dạng I,P,P …P (30 ảnh). Việc không có ảnh B làm cho độ phức tạp khi thiết kế bộ codec giảm đi đáng kể.
- → Theo thông tin trên chỉ số ảnh dùng tham chiếu (refs=1), do đó chỉ là ảnh sau tham chiếu ảnh trước.

pts (Presentation Time Stamp) để chỉ thời điểm mà picture đó được hiện thị, xem giá trị này với tất cả các picture thì ta thấy giá trị này tăng đều.
- → Các ảnh không bị thay đổi thứ tự trong quá trình encode.  Từ thông tin chỉ có ảnh I,P (không có B) cũng dễ đoán được điều này.

- Và nhiều thông tin cực kì chi tiết  
Dùng ffmpeg bằng các option của nó (ex: debug …) có thể phân tích thông tin rất chi tiết đến cả macroblock, nhưng nó ngoài phạm vi bài viết.

#### 3.3. Phân tích QP của picture.
QP là của mỗi picture, sinh ra từ quá trình rate control xem ở [5]. Xem QP của mỗi picture cho ta hình dung qua được độ phức tạp của chiến lược rate control trong bộ codec.

Tìm mãi không thấy command cho phép ffmpeg log giá trị trung bình QP của từng picture nên đành dùng JM. JM chỉ làm việc với element stream, tức là raw h.264 chứ không chơi với container, như mts, mp4 … Do đó đầu tiên vẫn phải nhờ ffmpeg bóc cái h.264 element stream ra.
```
ffmpeg.exe -i sony.mts -c:v copy sony.264
```

Đưa vào JM, và thực hiện decode bằng command dưới.

ldecod.exe -d decoder -P InputFile=sony.264

![qp](/assets/2018/07/qp.png)

Ôi, than ơi, các thánh chơi QP cố định = 30 cho các picture cmnl. Vậy ở level picture thì giá trị QP chả điều chỉnh gì hết, tất nhiên xuống mức macroblock có thể điều chỉnh quanh giá trị này.

### 4. IphoneSE của Apple thì sao.
- Birate 23.7 Mbps
- High profile, level 4.2.
- Khi encode, chỉ sử dụng 1 picture để tham chiếu.
- GOP: I,P,P ..P (60 ảnh).
- Không có ảnh B, tức là không có sự thay đổi thứ tự để hiển thị.
- Rate control có vẻ tích cực hơn, QP thay đổi từ 20 ~ 31 . I picture là ảnh quan trọng ảnh hưởng nhiều đến chất lượng,  vì thế nên nên được encoder với QP thấp hơn.
- Cơ bản Apple dùng QP thấp hơn, độ mất mát thông tin ít hơn, nhưng vẫn nén được bitrate thấp hơn Sony? ( thật ra phải cùng 1 data đầu vào mới nói được vậy).

### 5. Kết luận.
A/e được học video coding, bao nhiêu thứ phức tạp như ảnh B tham chiếu 2 chiều cả quá khứ lẫn tương lai, h.264 cho phép 1 picture có thể đa tham chiếu (multi refer) lên đến 16 picture, cấu trúc GOP của h.264 rất tự do cho phép reorder, tham chiếu thoải mái …
Nhưng thực tế phũ phàng là để đạt được realtime (chắc là thế) các bộ encoder trong các thiết bị có vẻ phải hi sinh nhiều thứ để giảm độ phức tạp. Thậm chí cấu trúc GOP trên của h.264 còn đơn giản hơn cấu trúc của MPEG2-Video có ảnh B.
Mặc dù có vẻ codec trong IphoneSE chỉnh chu hơn HDR-CX470, nhưng để so sánh codec là vấn đề rất phức tạp mà cái quan trọng nhất là phải chung 1 dữ liệu đầu vào, trong khi đã đóng gói trong sản phẩm thì điều đó là không thể. Bài viết cũng chỉ là ngó qua một số thông tin từ kết quả video để phán đoán 1 chút về bộ encoder.

Tuy nhiên, một thiết bị quay video tốt, thì bộ encoder không phải là tất cả, ngoài ra còn ống kính, tính năng room, chống rung … tác động rất lớn đến chất lượng video và trải nghiệm.

### Tham khảo.
- [1] https://www.ffmpeg.org/
- [2] https://en.wikipedia.org/wiki/FFmpeg
- [3] https://www.itu.int/rec/T-REC-H.264.2-201602-I/en
- [4] https://ffmpeg.org/pipermail/ffmpeg-devel/2015-July/176489.html
- [5] https://vcostudy.com/2018/04/21/rate-control-video-coding
- [6] https://www.ffmpeg.org/documentation.html
- [7] https://vcostudy.com/2018/04/14/profile-va-level-trong-ma-hoa-video

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />