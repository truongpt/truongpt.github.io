## Tản mạn về lịch sử chuẩn nén video

Chuẩn mã hóa video được rất nhiều công ty, tổ chức phát triển, nó cũng gần tương tự như các sản phẩm thương mại, có những chuẩn nén chết yểu mà cũng có những chuẩn nén rất thành công. Ở thời điểm bài viết này (12/2017) thì chuẩn H.264 phổ biến nhất đã thêm level 6, 6.1, 6.2 cho phép hỗ trợ nén lên đến format 8K(8192×4320), chuẩn H.265 gần như đã phát triển xong và rất nhiều công ty đã hỗ trợ như Sony, Apple, hay open source như x265, nhưng nó cũng gặp trở ngại lớn ngoài sự phổ biến của H.264  (giống như do WindowXP phổ biến quá làm các version mới hơn khó phổ biển) thì phí bản quyền quá cao nên Google (Youtube) vẫn chưa thấy kế hoạch support, và một liên minh non trẻ mới thành lập tuyên bố phát triển một chuẩn video mở có tên là AOM AV1 với độ nén vượt quá H.265 [5] chắc do bất mãn với phí bản quyền H.265 đã đi ngược triết lí của ISO là “kỹ thuật đi trước tiền bạc tính sau”.

Tuy nhiên cũng có những công ty đầu sỏ về xử lý video và có tiền bạc nên có thể tự đứng ra thiết kế chuẩn nén video như Google với VP8, VP9 hay Cisco System với Thor, nhưng nổi trội nhất vẫn là 2 tổ chức ISO/IEC và ITU-T. Tính từ năm 1984, 2 nhóm nghiên cứu về xử lý đa phương tiện của thuộc 2 tổ chức này cụ thể là VCEG thuộc ITU-T chuyên nghiên cứu về xử lý video tập trung vào các ứng dụng truyền thông, đàm thoại do đó thường ưu tiên những thuật toán để giảm độ trễ, birate thấp …, nhóm còn lại là MPEG thuộc ISO/IEC chuyên nghiên cứu về video cho các ứng dụng đa phương tiện, như truyền hình, hay phục vụ các trình xử lý play video nên ưu tiên các thuật toán liên quan đến hiệu năng nén.
Trong quá trình phát triển video codec được lãnh đạo bởi 2 tổ chức này, có những chuẩn video được mỗi tổ chức phát triển riêng, và cũng có chuẩn video được phát triển bởi sự hợp tác của 2 tổ chức này. Lược sử phát triển chuẩn video của 2 tổ chức tổng kết như hình dưới.


![history_video](/assets/2018/04/history_video.png)
(Hình vẽ trích dẫn trong slide 5 ở tài liệu [9]).

Năm 1984, ITU-T ra mắt chuẩn nén video được coi là chuẩn nén video số đầu tiên với tên gọi H.120, nhưng theo wiki [H.120](https://en.wikipedia.org/wiki/H.120) thì không có bất kì một codec nào dùng chuẩn nén này, tức là về mặt ứng dụng không thằng nào dùng cả, nghe đâu do hiệu năng thấp.

Đến tháng 11 năm 1988, ITU-T tiếp tục giới thiệu H.261, với tài liệu đặc tả chỉ vẻn vẹn 29 trang quá khiêm tốn với hơn 400 trang của những chuẩn nén hiện tại. Tuy thế H.261 đưa ra những khái niệm quan trọng như Macroblock vẫn còn được dùng đến tận 20 năm sau ở H.264, chỉ đến lúc H.265 (năm 2013) mới dẹp tên gọi này mà sử dụng tên gọi mỹ miều hơn CTU (Coding Tree Unit) tuy bản chất vẫn là mở rộng của Macroblock. Đặc biệt hơn, từ H.261 bắt đầu đưa ra kiến trúc của việc hoạt động video coding “Hybrid Coding Concept” như là hoạt động của bộ mã hoá video. Toàn bộ các chuẩn mã hoá về sau MPEG2-Video/H.262, H.263, AVC/H.264, HEVC/H265 và chuẩn đang được xây dựng cho đến thời điểm này (08/2018) VVC/H.26x, đều dựa vào cấu trúc trên.

Cũng cùng năm đó ISO/IEC giới thiệu chuẩn nén video đầu tiên của mình, mang tên MPEG1 Part2 tức là MPEG1 video nằm trong hệ thống MPEG1, nhưng cũng chẳng lấy gì làm thành công cho lắm.

Vào năm 1995, lần đầu tiên 2 tổ chức này cùng hợp tác giới thiệu chuẩn nén chung. ISO/IEC thì gọi là MPEG2 Part2 (MPEG2 video), còn ITU-T thì gọi là H.262 (thuộc dòng chuẩn H.26L). Do mục đích phát triển chuẩn nén video của 2 tổ chức khác nhau nên cũng là lần đầu tiên xuất hiện các khái niệm profile & level trong chuẩn video, nhằm giới hạn thành các tập con trong chuẩn nén phù hợp với từng ứng dụng khác nhau.

Sau đó ITU-T tiếp tục giới thiệu thêm một chuẩn video riêng của mình là H.263 vào 1995, đồng thời ISO/IEC cũng chẳng kém cạnh đã đưa ra MPEG4 Part2, nhưng có vẻ cả 2 thằng đều không được thành công nếu dựa vào mức độ phổ biến.

Sau khi định đánh quả lẻ không thành, 2 tổ chức tiếp tục bắt tay hợp tác để rồi vào năm 2003 đưa ra MPEG-4 Part10/H.264. Chuẩn nén này được thừa kế rất nhiều những thuật toán ưu việt của những chuẩn nén trước đó, đồng thời cũng có sự thay đổi rất mạnh mẽ về cấu trúc bit stream, đưa ra những khái niệm như NAL, và có vẻ xa rời các khái niệm liên quan đến hình ảnh (picture header, sequence header …) do đó làm cho những ai đã quen với MPEG-2 thì khi tiếp xúc với H.264 rất khó nắm bắt.
H.264 chuẩn nén được xem là thành công nhất cho đến thời điểm hiện tại, theo thống kê vào năm 2010 thì mức độ sử dụng H.264 trên internet hơn 60%. Mặc dù lúc đầu đối tượng của H.264 là video format FHD (1920×1080) tuy nhiên đến thời điểm hiện tại (2017) phiên bản mới nhất của H.264 cho phép hỗ trợ đến tận 8K(8192×4320) .

Thành công nối tiếp thành công, ISO/IEC và ITU-T tiếp tục thành lập nhóm JVCT để thiết kế và đưa ra MPEG H Part2/H.265 vào năm 2013, với đối tượng là video 4K và yêu cầu độ nén gấp đôi H.264 với cho phép mức độ phức tạp gấp 10 lần (đo ước lượng bằng thời gian mã hoá trên cũng một hệ thống). Đến thời điểm hiện nay 2017 thì chuẩn nén này về cơ bản đã hoàn thành tuy vẫn đang được tiếp tục bổ sung chỉnh sửa nên JVCT vẫn tiếp hành họp hằng năm (1 năm 4 lần).

Với tần suất 10 năm cần có một chuẩn nén mới, do độ phân giải màn hình tăng lên gấp 4 nhưng tốc độ internet chỉ tăng lên gấp đôi 🙂 do đó cần một chuẩn nén mới để tăng hiệu năng nén gấp đôi chuẩn nén hiện tại. Trong bối cảnh đó JEVT là nhóm chung của 2 tổ chức được thành lập với kế hoạch năm 2020 đưa ra chuẩn nén mới ( chắc ITU-T gọi là H.266?) với yêu cầu độ nén gấp đôi H.265, đối tượng là video format 8K, có thêm các thuật toán phù hợp mới các ứng dụng video mới nổi như video 360 độ, VR/AR …

Trong khi chưa biết tương lai nào cho H.265 vì phí bản quyền H.265 rất cao, có những trường hợp gấp trên dưới 10 lần H.264, do đó nhưng công ty sử dụng nhiều chuẩn nén video như google (youtube) rất lo sợ một khi H.265 trở nên phổ biến. Chắc cũng vì nguyên nhân đó mà liên minh chuẩn nén video mở được thành lập, theo kế hoạch là trong năm nay (2017) sẽ hoàn thành đặc tả kĩ thuật đồng thời có cả codec open đi kèm, với sự tham gia cả những công ty về phần cứng như AMD, ARM hay những công ty về dịch vụ như Amazon, Netflix … thì liên minh này rất hi vọng AOM AV1, tên của chuẩn nén mở này, sớm cất cánh và hạ gục H.265.

Tương lai nào chờ đợi H.265? Liệu ISO/IEC & ITU-T có tiếp tục thắng thế so với các chuẩn mở.

- Update 14/04/2018: AV1 có vẻ đang hung hãn lên dần (đã công bố đặc tả pdf version, tuy vẫn là bản tạm thời), khoe rất nhiều ở [NAB](https://aomedia.org/news/aomedia-at-nab/).
- Update 01/08/2018: Chuẩn nén sau HEVC của ISO/IEC & ITU-T đã chính thức mang tên VVC.

### Tài liệu tham khảo
- [1] https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC
- [2] https://en.wikipedia.org/wiki/Video_coding_format
- [3] https://en.wikipedia.org/wiki/H.261
- [4] https://techcrunch.com/2010/05/01/h-264-66-percent-web-video/
- [5] http://aomedia.org
- [6] H.120: https://www.itu.int/rec/T-REC-H.120-199303-I/en
- [7] H.262: http://www.itu.int/rec/T-REC-H.262-201202-I/en
- [8] https://aomedia.org/news/aomedia-at-nab/
- [9] https://www.slideshare.net/MathiasWien/trends-and-recent-developments-in-video-coding-standardization

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />