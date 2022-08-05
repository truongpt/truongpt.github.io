## Kế hoạch chuẩn nén video sau MPEG-HEVC/H.265

### 1. Công tác chuẩn bị.

Đến hẹn lại lên, sau chu kỳ trên dưới 10 năm lại cần có một chuẩn nén video mới, với nguyên nhân quan trọng nhất là tốc độ truyền data trên internet chỉ tăng gấp 2 trong khi đó với thì màn hình độ phân giải tăng gấp 4. Ngoài ra còn do xuất hiện nhiều xu thế ứng dụng mới mà chuẩn nén video hiện tại chưa đáp ứng phù hợp, cũng có thể thêm một lý do nữa là giải quyết công ăn việc làm cho đám chuyên gia về nghiên cứu kỹ thuật nén video.

Năm 2004 đánh dấu ra đời MPEG-AVC/H.264, cho đến 2009 thì việc bổ sung thêm các công cụ mã hóa đã hoàn thành. MPEG-HEVC/H.265 được phiên bản đầu tiên được thông qua vào 2013, và đến đầu 2017 thì công bố profile SCC(Screen Content Coding Extension) hướng tới các ứng dụng nén hình ảnh không tự nhiên (tức là video các cảnh không phải thực tế, kiểu như phim hoạt hình, các ứng dụng chia sẻ màn hình …) đánh dấu về cơ bản hoàn thành việc phát triển các công cụ mã hóa trong HEVC.

ISO/IEC và ITU-T lại lên kế hoạch cho chuẩn nén video mới, dự định sẽ bản đầu tiên sẽ được công bố vào năm 2020.

Bước đầu tiên để đánh giá sự cần thiết làm ra chuẩn nén video mới bằng cách thực hiện các brainstorm (một kiểu thảo luận tự do nhằm đánh giá nhu cầu), để thu thập ý kiến từ các công ty, các tổ chức chuyên về mã hóa video[1].

### 2. Yêu cầu chính thức

Sau khi đi đến thống nhất cần một chuẩn nén video mới, thì ISO/IEC và ITU-T sẽ đưa ra tài liệu yêu cầu chính thức cho chuẩn nén video mới[2].

Tài liệu yêu cầu này sẽ miêu tả cụ thể những tiêu chí chuẩn nén video mới, để căn cứ vào đó sau này sẽ quyết định công cụ mã hóa (encoding tool) nào được thông qua để tích hợp vào đó.

Các yêu cầu bao gồm đặc trưng cụ thể của đối tượng mã hóa như kích cỡ khung hình (picture format), khả năng nén (compression performance)…, cũng như phạm vi ứng dụng.Ví dụ lần này đối tượng là 8K, khả năng nén gấp đôi HEVC, trong phần phạm vi ứng dụng đã có đề cập đến thực tế ảo, IoT, Automotive…

### 3. Thành lập dự án.

Để tiến hành nghiên cứu và thực hiện chuẩn nén mới, 2 bộ phận chuyên trách về mã hóa video, cụ thể là nhóm MPEG (Motion Picture Expert Group) của ISO/IEC và nhóm VCEG(Video Coding Experts Group) của ITU-T sẽ thành lập một nhóm liên kết giữa 2 bên, có tên là JVET(Join Video Explore Team) [3].

JVET được sự tham gia của hầu hết các chuyên gia về kỹ thuật nén video từ các công ty lớn về mảng video như Sony, Gopro, Samsung, Nikon, Qualcomm, Socionext …, và các trường đại học có chuyên môn về mã hóa video (chủ yếu là Hàn, Tàu và Đức).

JVET sẽ thực hiện thực hiện họp 4 lần trong 1 năm, cùng với chu kỳ họp hành của MPEG, để trao đổi các kết quả đạt được cũng như thống nhất nội dung cuộc họp tiếp theo. Toàn bộ tài liệu họp và nội dung các cuộc họp đều được phổ biến rộng rãi trên trang chính của JVET[6], [7].

### 4. Công cụ phát triển & qui trình làm việc.

Để phát triển chuẩn nén mới, JVET sử dụng công cụ có tên là JEM (Join Exploration Model) [5].

JEM được hiểu đơn giản là một phần mềm thực hiện mã hóa video dựa trên các kết quả đạt được hiện tại. Tức là JEM sẽ là codec đầu tiên cho chuẩn nén video mới, nó được xây dựng trên cơ sở thừa kế của công cụ HM (HEVC model)[12], vốn là công cụ để phát triển HEVC. JEM được sử dụng để kiểm tra các công cụ mã hóa trong quá trình phát triển chuẩn nén mới.

Đồng thời các công ty hay tổ chức khi đưa ra đề nghị công cụ mã hóa mong muốn tích hợp và chuẩn nén mới đều phải có bản sửa JEM có tích hợp công cụ mã hóa đó và kết quả kiểm tra đạt được đó trên JEM đi kèm.

Trong mỗi cuộc họp của JVET sẽ đánh giá kết quả đạt được trong 3 tháng từ cuộc họp lần trước, chủ yếu là xem xét các kết quả đề xuất về công cụ mã hóa lần trước, cùng nhau xem xét những đề xuất mới, ngoài ra cũng không kém phần quan trọng là cùng nhau xem xét lựa chọn ra tập hợp dữ liệu dùng để làm cơ sở đánh giá các các công cụ mã hóa đang được nghiên cứu.

Để phục vụ cho việc xây dựng chuẩn nén video mới, ISO/IEC & ITU-T phát hành thông báo chính thức đến các tổ chức chuyên về video để đề nghị đóng góp về kỹ thuật[4], đóng góp về kết quả kiểm tra[8],[9], cung cấp thêm về dữ liệu phục vụ cho việc đánh giá chuẩn nén mới[10].

Khi một công ty hay tổ chức đưa ra đề xuất công cụ mã hóa trong các cuộc họp của JVET, nếu công cụ mã hóa đó được đánh giá khả thi thì JVET sẽ tiến hành thực hiện việc đáng giá bằng cách kêu gọi 1 nhóm tình nguyện, độc lập đứng ra đánh giá, thông thường thì cũng là các công ty hoặc nhóm ở trong JVET, kết quả đánh giá sẽ được công bố vào cuộc họp kế tiếp, và từ kết quả đó để quyết định công cụ mã hóa này có được chấp nhận đưa vào chuẩn nén mới hay không.

Đến khi có đủ công cụ mã hóa tích hợp vào chuẩn nén mới để đạt được như yêu cầu thì JVET sẽ công bố tài liệu đặc tả chính thức.

### 5. Kết quả hiện tại.

Ở thời điểm hiện tại (04/2018), cuộc họp mới nhất là cuộc họp lần thứ 10 của JVET đang diễn ra vào 10/04/2018 ở San Diego, Mẽo.

Theo kết quả cuộc họp trước đó, vào 20/1/2018 thì khả năng nén đã đạt được tầm 20~40% so với HEVC.

Ngoài ra có thể tham khảo thêm tổng kết bảo cáo[11] của Sullivan (làm việc ở Mirosoft, đại diện cho MPEG làm trùm trong đội JVET).

### 6.Tài liệu tham khảo.
- [1] https://mpeg.chiariglione.org/standards/exploration/future-video-coding/presentations-brainstorming-session-future-video-coding
- [2] https://mpeg.chiariglione.org/standards/exploration/future-video-coding/requirements-a-future-video-coding-standard-v3
- [3] https://www.itu.int/en/ITU-T/studygroups/2017-2020/16/Documents/video/JVET-ToR-TD-PLEN-0155A1.pdf
- [4] https://www.itu.int/en/ITU-T/studygroups/2017-2020/16/Documents/video/JVET-H1002-CFP-VCBHEVC-Final-v6.pdf
- [5] https://jvet.hhi.fraunhofer.de/
- [6] http://wftp3.itu.int/av-arch/jvet-site/
- [7] http://phenix.it-sudparis.eu/jvet/
- [8] https://www.itu.int/en/ITU-T/studygroups/2017-2020/16/Documents/201701/Video-CfE-Final.pdf
- [9] https://mpeg.chiariglione.org/tags/call-evidence
- [10] https://mpeg.chiariglione.org/tags/future-video-coding
- [11] http://www.cs.brandeis.edu//~dcc/Programs/Program2016KeynoteSlides-Sullivan.pdf 
- [12] https://hevc.hhi.fraunhofer.de

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />