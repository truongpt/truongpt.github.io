## Video compression nhìn từ bên dưới

Ghi chép lại một chút về kiến thức cơ bản lượm nhặt được về vấn đề nén video, không đi sâu cụ thể vào điểm nào, chỉ loanh quanh ở dưới …

### 1. Nếu video không được nén.
Thử ngẫm xem thú vui xem phim ảnh bị ảnh hưởng thế nào nếu video không được nén.  
Xét trường hợp phổ biến nhất thời bấy giờ, full-HD (1920×1080), progressive, frame rate 24 fps (phò nhất có thể).  
Một pixel được xây dựng từ 3 mã màu RGB (Red-Green-Blue) → 1 pixel cần 8×3 bit.  
Vị chi là trong 1 giây sẽ có lượng dữ liệu: 1920 x 1080 x (8×3) x 24 = 1194393600bit ~ 1.2 Gbit.  
Vậy bitrate để có thể play được video này là 1.2 Gbits/s  
1 bộ phim tầm 1.5h sẽ có dung lượng: 806 GB  

Trong khi đó, đĩa [Blu-Ray DVD](https://en.wikipedia.org/wiki/Blu-ray) chứa được 25 GB (single layer), tốc độ đọc dữ liệu 36 Mbits/s, tốc độ TV Broadcast (truyền hình KTS) là 1 ~ 20 Mbits/s, tốc độ internet ~100 Mbps/s ( vừa kiểm tra bằng speedtest.net của internet đang dùng).

Con số trên đủ nói lên tất cả về khả năng trải nghiệm video nếu không được nén. Vậy nếu lấy dịch vụ dùng video phổ biến hiện giờ là internet, thì cũng cần ít nhất cần nén xuống > 12 lần mới ngang tầm bitrate của internet, còn nếu lấy theo [recommend bitrate](https://support.google.com/youtube/answer/1722171?hl=en) của youtube với fHD là 8 Mbits/s, thì cần nén tầm 150 lần.

Vậy nếu birate tầm 8 Mbps/s thì, theo cách tính trên thì sẽ xem được phim trên internet có format lên tới cỡ “kinh hoàng” là 160×120.

Thảm họa cho những ai thích xem phim nhỉ.

### 2. Nén video theo một cách khác.
Giả sử bỏ qua tất cả những cái gì gọi là phương pháp, thuật toán … nén video. Thử đi nén video bằng các công cụ như vẫn thường hay dùng để nén file thì chuyện gì xẩy ra, ví dụ dùng Zip chẳng hạn. Tạm thời chưa vội bàn về tỉ lệ nén có đạt được hay không (thật ra thì chắc chắn là không), thử xem xét xem sẽ vấp phải vấn đề gì.  
Theo hình thức đơn giản nhất, cho 1 file video raw 806 GB ở trên vào, nén Zip, vậy là xong. Vậy khi muốn xem thì làm thế nào, vì chỉ giải nén được khi có toàn bộ file mà không có giải nén từng phần, do đó phải nhận đầy đủ 1 file đó rồi giải nén ra sau đó dùng 1 chương trình nào đó hỗ trợ xử được dữ liệu video raw xem :-). Thêm vào đó, chơi kiểu này thì không thể thực hiện streaming video (broadcast, internet …) vì không thể giải nén được được nếu chỉ nhận được từng phần của file.  

Thử cố cải tiến nó lên 1 chút, bằng cách chia video raw đó ra nhỏ thành các picture rời nhau (có tất cả 24 fps * 1.5h * 60p * 60s = 129600 picture), và nén zip từng picture lại, rồi tìm cách truyền nó đi lần lượt để có thể xem được khi dùng dịch vụ xem trực tuyến. Nhưng ta sẽ gặp vấn đề sau.

- Tỉ lệ nén khó đạt được, vì zip là nén không mất dữ liệu( lossless) thì khó mà lên được nén 150 lần.★
- Ở trên đang mới xem đến việc xử lý các picture, giờ muốn truyền cái đó hay play như phim ảnh thì cần xem xét các yếu tố: Khi đóng gói đến gửi đi thì phải đánh dấu để phân biệt được vị trí các picture, cần đính kèm cả các thông tin để biết hiển thị video đó thế nào (frame rate, resolution …), cần thông tin thời gian từng picture để đồng bộ với audio … tóm lại cần qui định 1 format như MP4, MKV … để chứa loại dữ liệu video nén bằng zip đấy.

Ở trên ta thấy vấn đề bất khả thi nằm ở chỗ tỉ lệ nén, do zip là cách nén không mất dữ liệu nên không thể đạt được tỉ lệ nén như mong đợi. Thay vì dùng zip để nén từng ảnh thì dùng 1 cách nén lossly khác nén ảnh để đạt tỉ lệ nén cao hơn, ví dụ JPEG, tức là từ video raw, chia ra cách ảnh raw và nén nó lại bằng cách convert thành các ảnh JPEG :), nén JPEG chắc chắn đảm bảo được tỉ lệ nén, cùng lắm thì chất lường fò thôi ;-). Ngon rồi đây, giờ chỉ còn vấn đề số 2 như ở trên, với trường hợp này thì nó đã được giải quyết khi streamming thì nó đóng gói như [này](https://tools.ietf.org/html/rfc2435), còn lưu thành file thì nó theo format [này](https://staticky.com/dl/ftp.apple.com/developer/Development_Kits/QuickTime/Programming_Stuff/Documentation/QuickTime-JPEGSpec.pdf), do chính Apple xử lý, hay Microsoft hỗ trợ để lưu nó trong file AVI …
Đây là câu chuyển của 1 chuẩn nén video có tên là [MJPEG](https://en.wikipedia.org/wiki/Motion_JPEG) (Motion-JPEG), đúng như tên gọi, nó “đơn giản” chỉ là gồm các ảnh JPEG chuyển động.

Đến thời điểm hiện tại thì MJPEG có thể dùng làm đồ cổ được rồi. Tuy nhiên năm vừa rồi (2017) có tham gia 1 dự án thiết kế SOC cho Automotive (Lexus hẳn hỏi) vẫn có sử dụng MJPEG để record camera phía sau xe vì lý do xử lý nhanh, độ trễ thấp để đảm bảo driver delay thông tin nhìn từ sau xe.

### 3. Nền tảng cơ sở.
Nén video cơ bản là kiểu nén mất dữ liệu (lossly), cho dù các chuẩn nén mới từ MPEG2-Video trở đi đều hỗ trợ nén lossless, nhưng nó chỉ có ý nghĩa dùng để lưu trữ hơn là dùng trong lĩnh vực sử dụng, do tỉ lệ nén thấp. Khi nén lossless thì chỉ từ AVC/H.264 mới có thể nén thành file có dung lượng nhỏ hơn file gốc, điều này không có gì ngạc nhiên, do việc chuyển từ file video raw thành dạng có format phải mất 1 lượng overhead (thông tin header của các picture …). Tức là chỉ với AVC/H.264 trở đi thì việc nén dữ liệu video mới bù được lượng overhead trên.

Vậy nén mất dữ liệu thì cái gì được mất cái gì cần giữ. Vì ta biết “một nửa sự thật thì không còn là sự thật”, trong khi đó một nửa cục phân đất vẫn là cục đất. Thông tin trong video thuộc loại nào “sự thật” hay cục đất?
Để hiểu cơ sở nén video, thì xem lại chút về truyện ngụ ngôn học hồi lớp 7 (chương trình giáo dục trước khi bị ~tàn phá~ cải cách) [Ở đây có bán cá tươi](https://lazi.vn/truyen_cuoi/d/truyen-cuoi-treo-bien-o-day-co-ban-ca-tuoi), có thể rút ra 2 điểm.

- Thông tin thừa do bị lặp lại như: **ở đây**, **có**
- Thông tin ít được chút ý, ít tác động đến đối tương cần truyền đạt: **tươi**
- Thông tin quan trọng, phải giữ nguyên (trong truyện thì đi bỏ mất, thế mới là truyện ngụ ngôn): bán, cá

Vậy ra truyện ngụ ngôn ông cha ta từ lâu đã có liên hệ với kỹ thuật nén video hiện đại :-D.  
Cũng tương tự như vậy, nén video là quá trình loại bỏ các thông tin thừa, giữ lại thông tin quan trọng. Với thông tin thừa do tính lặp lại, hoặc do thông tin đó không cần thiết đến đối tượng sử dụng (cái này không hẳn là thừa) cụ thể [nhận thức trực quan](https://en.wikipedia.org/wiki/Human_visual_system_model) của mắt người.  
Cụ thể hơn, quá trình nén video là quá trình loại các thông tin dư thừa có thuộc tính dưới đây.

#### Dư thừa thuộc tính không gian (Spatial redundancy)
Việc dư thừa này chỉ xét trong từng ảnh, bản thân các vùng không gian trong 1 ảnh luôn có sự liên quan ít nhiều đến nhau, vì hầu hết các vùng trong ảnh thể hiện không gian liên tục. Thuộc tính này được tận dụng khi thực hiện nén video, tìm cách loại bỏ sự tương quan về mặt không gian này.  
Cụ thể như hình dưới đây, vùng màu đỏ đã được thực hiện nén trước đó, tiếp đến thực hiện nén block màu xanh. Việc nén block màu xanh, thì thay vì mang toàn bộ dữ liệu block màu xanh thì ta chỉ cần xử lý dựa trên block màu đỏ như sau.  
Từ block màu đỏ, thực hiện phép dự đoán (tùy thuộc vào từng loại chuẩn video sẽ qui định cách dự đoán) để tạo ra block trung gian, như trong hình là nó kéo dài toàn bộ các pixel ở rìa bên phải, từ đó có thể tạo ra 1 block nhiều điểm tương đồng với block màu xanh. Thay vì nén toàn bộ block màu xanh, ta chỉ cần thực hiện nén sự khác nhau giữa block màu xanh và block trung gian này. Do 2 block này nhiều điểm giống nhau nên dự liệu cũng giảm đi đáng kể.

![spatial](/assets/2018/08/spatial.png)  

Thuật ngữ của việc này là [Intra coding](https://en.wikipedia.org/wiki/Intra-frame_coding).

#### Dư thừa thuộc tính thời gian (Temporal redundancy)
1 luồng video thì tối thiểu cần lưu giữa 24 ảnh trong 1 giây (do tạo cảm giác liên tục đối với mắt con người). Một điều dễ nhận thấy là các bức ảnh cạnh chứa rất rất nhiều điểm giống nhau (trừ lúc chuyển cảnh), ví dụ như hình dưới đây.

![temporal](/assets/2018/08/temporal.png)

Vậy khi ảnh Frame 3 đã được nén, thì việc thực hiện nén Frame 4, thay vì nén toàn bộ ảnh Frame 4, ta chỉ cần nén sự khác nhau giữa Frame 4 và Frame 3 tức là Frame 4 -Frame 3. Nhìn vào hình trên ta thấy lượng dữ liệu cần nén chỉ còn vài vùng chỗ khuôn mặt cô gái.

Trên thực tế khi thực hiện ở các chuẩn nén video, còn có các kỹ thuật nằm đưa nó về dạng giống nhau nhất có thể. Cụ thể là việc thay đổi giữa các ảnh do đối tượng trong những ảnh có sự chuyển động theo thời gian, kỹ thuật bù trừ chuyển động ([Motion Compensation](https://en.wikipedia.org/wiki/Motion_compensation)) chính là để xử lý việc này.  
Việc nén này được biết đến với trên gọi là [Inter coding](https://en.wikipedia.org/wiki/Inter_frame).

Cách làm của MJPEG nói ở trên, không tận dụng được thuộc tính này, do nó là các ảnh JPEG độc lập nhau. Đây vừa là điểm yếu (tỉ lệ nén không cao) vừa là điểm mạnh do thực thi đơn giản của MJPEG, nên dù chuẩn nén cổ nhưng nó vẫn được dùng trong một số trường hợp ở thời điểm hiện tại (2018).

#### Dư thừa thị giác (Perceptual redundancy)
Chung qui lại, đối tượng của video là người xem, cụ thể hơn là con mắt người xem. Do đó trong quá trình nén video cần hiểu cách cảm nhận hình ảnh của mắt người. Mắt con người nhạy cảm với vùng có tần số cao (tức là vùng mà các pixel thay đổi nhiều, ví dụ như tóc cô gái dưới) hơn là vùng có tần số thấp (các pixel không thay đổi nhiều, ví dụ chỗ da ở má cô gái). Thực tế khi xem phim, những chỗ sắc nét (tần số cao) nếu bị nhiễu sẽ tác động rất nhiều đển việc cảm nhận chất lượng của video đó.  
Do đó trong nén video cũng ưu tiên hơn việc giữ lại dữ liệu ở tần số cao, loại bỏ dữ liệu tần số thấp. Yêu cầu bitrate càng cao thì càng bỏ càng nhiều. Đây chính là quá trình gây ra mất dữ liệu trong nén video.

![Perceptual.png](/assets/2018/08/perceptual.png)

Trong video nén, quá trình trên được thực thi bằng biến đổi Cosin ([DCT](https://en.wikipedia.org/wiki/Discrete_cosine_transform)) nhằm chuyển dữ liệu sang miền tần số, và sau đó lượng tử hóa ([Quantization](https://en.wikipedia.org/wiki/Quantization_(image_processing))) để bỏ bớt dữ liệu tần số thấp.

#### Dư thừa thống kê (Statistical redundancy)
Sau khi thực hiện 3 quá trình giảm thông tin dư thừa, và cắt bỏ bớt thông tin không cần thiết ở trên, đến giai đoạn cuối cùng, sẽ cố gắng nén bằng các kỹ thuật nén không mất dữ liệu, bằng cách tận dụng sự lặp đi lặp lại của dữ liệu theo đúng ý nghĩa của nó, hoặc là sử dụng mã code có kích thước nhỏ để mã hóa cho những đoạn bit data có tần số xuất hiện lớn .Đến lúc này về cơ bản nó được đối xử như dữ liệu thông thường, tức là sẽ áp dụng các kĩ thuật nén không mất dữ liệu kiểu như Zip, chỉ là “kiểu như thôi”, vì nó phải cân nhắc nhiều yếu tố khác do đặc thù nén video.  
Phase này trong nén video còn gọi là [Entropy coding](https://en.wikipedia.org/wiki/Entropy_coding).

- P/S: ★ Về việc nén lossless, có ai biết về mặt lý thuyết thì nén lossless sẽ bị giới hạn đế mức nào, thì nhờ chỉ bảo. Mình đang nghĩ là sẽ có sự ràng buộc nào đó vì lượng thông tin trong dữ liệu nhất định là cố định. Do tuỳ từng kiểu dữ liệu mà có tỉ lệ nén đạt được khác nhau nên chỉ dám kết luận là khó chứ không hẳn là không thể.  

Định ngồi vẽ hình nhưng hơi lười vả có vẽ thì cũng xấu và lại không giá trị lắm, nên các hình vẽ được lấy trong tài liệu [1] dưới ↓  

### Tài liệu tham khảo
- [1] https://pdfs.semanticscholar.org/presentation/6971/4ffd97c9b8b1af6f64f78dda3b920e576a7b.pdf
- [2] https://en.wikipedia.org/wiki/Data_compression#Video

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />
