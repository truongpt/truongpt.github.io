## Liên minh chuẩn nén video mở (Alliance for Open Media)
### 1. Bối cảnh ra đời

Sau thành công của H.264 (AVC), ITU-T và ISO tiếp tục phát triển H.265 (HEVC), đặc tả kỹ thuật được hoàn thành 2013, và đến 2015 đã dần dần phổ biến khi nhiều công ty bắt đầu giới thiệu sản phẩm có hỗ trợ chuẩn nén này.
Lý do về chi phí bản quyền luôn là nguyên nhân để các công ty phải chi trả nhiều cho nó mong muốn phát triển một chuẩn nén free, tức là không tính tiền bản quyển, ví dụ như trước đây google giới thiệu dòng chuẩn nén VP8, VP9 song song với H.264, H.265 tuy nhiên nó không thực sự thành công, hay có thể vượt mặt được các các chuẩn nén có bản quyền, (riêng VP9 cũng đạt được ít nhiều thành công do nó là chuẩn nén của Google nên tất nhiên Youtube sẽ ưu tiên dùng nó nhất, cây nhà lá vườn mà).
Với H.265 thì chi phí bản quyền còn lớn hơn H.264 nhiều lần do rắc rối tùm lum vụ cãi cọ bằng sáng chế (patent) nên các vị không chơi chung quản lý bản quyền bằng một chỗ như H.264 phó mặc cho MPEG-LA nữa mà chia ra 3-4 chỗ, rồi còn chủ nghĩa địa phương tính xèng bản quyền theo vùng miền ( xem chi tiết ở [9]), chính vì vậy trước khi nó thực sự chiếm thị trường thì nhu cầu cần có 1 chuẩn nén free đối trọng với nó là rất cần thiết.

Trong bối cảnh đó, thì một liên minh chuẩn nén được thành lập với mục tiêu xây dựng được một chuẩn nén free lấn lướt được H.265, với tên là AOM/AV1 được gọi ngắn gọn là AV1. Nhiều công ty đã đưa công nghệ mà trước đó đánh quả lẻ nhằm tạo ra chuẩn nén riêng nhưng đã không gặt hái được nhiều thành công, mong góp phần xây dựng một chuẩn chung, như chuẩn nén Daala (Xiph/Mozilla), VP10(Google), Thor (Cisco).
Với sự tham gia đầu đủ từ các công ty phần mềm (Google, Mozilla …), phần cứng (ARM, AMD …) và cả các công ty cung cấp dịch vụ video( Netflix, Amazon …), có thể nói đây là liên mình video lớn nhất từ trước đến giờ. Đặc biệt có sự tham gia của Apple từ cuối năm 2017, hứa hẹn đây là một chuẩn nén có triển vọng trong tương lai.

### 2. Kế hoạch phát triển
Các tính năng được chốt vào 10/2017, đặc tả được chốt vào 01/2018, phần thời gian này chắc đã kiểm tra để có được bản chính thức (đoán vậy).

Cả chuẩn đặc tả lẫn open codec sử dụng đển phát triển đặc tả được lưu giữ ở git store dưới.
https://aomedia.googlesource.com

- Cập nhật: 11/04/2018
Tài liệu đặc tả bản draft (bản tạm) được công bố dưới dạng file pdf theo [14].
Phong cách viêt đặc tả tương đối giống tài liệu của ISO & ITU-T, tức là giống cách viết H.264, H.265, miêu tả cấu trúc luồng data, cách phân tích để ra các thông tin, cách decode nhưng không miêu tả thuật toán đứng đằng sau đó. Do lý do đó nên đặc tả thường chỉ dùng tham khảo trong quá trình phát triển codec, chứ không phù hợp cho việc học tập.

### 3. So sánh với H.264, H.265
Hiện tại do đặc tả cả AV1 vẫn chưa được hoàn thành, có vẻ như thế nên chưa có một báo cáo so sánh nào chi tiết khi so sánh với H.264, H.265. Do một báo cáo chi tiết cần có đánh giá trên phương diện chủ quan (sử dụng 1 tập các tình nguyện viên để xem demo video) nhưng đến thời điểm hiện tại mới chỉ có đánh giá khách quan ( tức là thông qua đo đạc matrix như PNSR …).

Theo báo cáo số [10] cho ta thấy phần lớn các trường hợp thì AV1 chất lượng ngang ngửa với HEVC. Tuy nhiên trong báo cáo [12] và [13] thì cho thấy các codec theo chuẩn nén hiện tại đều xách dép cho AV1. Nhưng ngạc nhiên thay trong báo cáo [11], một báo cáo rất đáng tin cậỵ vì nó được sự chấp thuận của IEEE, lại cho thấy codec theo chuẩn AV1 chỉ ngang ngửa với codec theo chuẩn H.264.

Tóm lại ai hơn ai kém, chắc phải đợi thêm thời gian :).

- Cập nhật: 26/05/2018.
Báo cáo [11] có vẻ thực hiện khi codec AV1 đang ở giai đoạn phát triển. Nên mình có mail hỏi ông anh làm paper đó về kết quả mới nhất thì nhận đc như báo cáo[15].
So với HM (codec dùng phát triển H.265) thì mức độ nén của AV1 codec vẫn kém 30% đến 47%.
Có vẻ về mặt kỹ thuật thì AV1 khó mà qua mặt được H.265 chứ chưa nói đến codec theo chuẩn nén mới mà ISO-IEC/ITU-T đang phát triển, chuẩn nén VVC. Tuy nhiên dưới  sự bảo kê của 1 loạt công ty công nghệ thì vẫn chưa biết ai sẽ là kẻ thắng.

### 4.Tài liệu tham khảo
- [1] http://aomedia.org
- [2] https://en.wikipedia.org/wiki/AV1
- [3] https://en.wikipedia.org/wiki/Daala
- [4] https://en.wikipedia.org/wiki/Thor_(video_codec)
- [5] https://medium.com/@voluntas/av1-の未来が開いた-38c5fd174630
- [6] https://hacks.mozilla.org/2017/11/dash-playback-of-av1-video/
- [7] https://www.telecompaper.com/news/apple-joins-alliance-for-open-media–1226820
- [8] https://hothardware.com/news/apple-joins-alliance-shrink-online-videos-royalty-free-codecs
- [9] https://en.wikipedia.org/wiki/High_Efficiency_Video_Coding
- [10] https://www.elecard.com/page/aom_av1_vs_hevc
- [11] http://ieeexplore.ieee.org/document/7906321/?reload=true
- [12] http://www.streamingmedia.com/Articles/Editorial/Featured-Articles/Bitmovin-Pushes-AV1-Forward-Joins-Alliance-for-Open-Media-117634.aspx
- [13] https://streaminglearningcenter.com/blogs/av1hevcvp9-comparison-streaming-media-east.html
- [14] https://aomediacodec.github.io/av1-spec/av1-spec.pdf
- [15] http://iphome.hhi.de/marpe/download/spie-2017.pdf

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />