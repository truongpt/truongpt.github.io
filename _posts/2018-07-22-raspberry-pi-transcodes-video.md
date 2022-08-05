## Raspberry PI transcodes video

### 1. Transcode là gì.
Transcode là quá trình chuyển đổi từ định dạng mã hóa hiện tại sang một dạng mã hóa khác, ví dụ như chuyển đổi video, audio coding format …
Thông thường thì việc thực hiện transcode có 2 lý do chính:
- Giảm dung lượng lưu trữ mà có thể đảm bảo được chất lượng video, bằng việc sử dụng video coding format tân tiến hơn, tăng khả năng nén hơn, nên các dữ liệu video đang sử dụng coding format cũ thường chuyển sang format mới để giảm dung lượng lưu trữ.
- Thiết bị đầu cuối không hỗ trợ video or audio hiện tại, do đó cần convert sang cái dạng mà nó hỗ trợ.

Trên thực tế hiện nay thì dễ thấy nhất là khi upload 1 file video lên facebook hoặc youtube, thì file video đó luôn được youtube/facebook xử lý thành định dạng khác trong quá trình upload.

Cơ bản thì quá trình transcode có thể hình dung đơn giản như dưới.

input file/stream → |decode| → |encode| →　output file/stream

Từ dữ liệu đầu vào, có thể là multimedia file format (MKV, MP4 …) hoặc stream (udp, tcp/ip …). Bước đầu tiên là giải mã (decode) thành phần đầu vào (video or audio tùy thuộc vào cái nào cần transcode) thành raw data. Tiếp đó thực hiện mã hóa (encode) thành định dạng mới ở dữ liệu đầu ra.

Transcode có thể realtime or non-realtime tùy thuộc vào từng yêu cầu của hệ thống. Trong các dữ liệu cần transcode thì video là phức tạp, tốn nhiều hiện năng nhất, và thường quan tâm nhất , do việc nén video theo chuẩn mới có thể tiết kiệm rất nhiều dung lượng or bitrate.

## 2. Video decoder/encoder trên RPI.
Raspberry pi(RPI) hỗ trợ cả hardware decoder lẫn encoder, do đó rất phù hợp nếu sử dụng nó để thực hiện transcode.  
2 bộ decoder và encoder trên RPI được thiết kế theo API của openmax mà cụ thể là openmax-il.
Openmax là chuẩn các api do khronos đưa ra để thiết kế hệ thống xử  lý multimedia, nó gồm có 3 phần tương được với 3 layer, nhìn hình dưới lấy từ trang chủ có nó thì hiểu, khỏi cần giải thích.

![media_portability](/assets/2018/07/media_portability.png)

Cái gì mà được chuẩn hoá thì mục đích cao nhất của nó là giúp giảm thời gian tích hợp, 2 thằng không cần biết nhau trước đó mà chỉ cần cùng tuân theo 1 chuẩn là dễ dàng tích hợp với nhau.
Openmax-il có thể hiểu là lớp trung gian giữa phần cứng (hardware) và application hay còn gọi là firmware, đây cũng là phần API được sử dụng rộng rãi nhất của openmax. [Android media framework](https://source.android.com/devices/media), ffmpeg, gstreamer đều đã hỗ trợ openmax-il với tư cách là IL client, tức là layer ngay ở trên openmax-il . Do đó nếu bạn rảnh rỗi thiết kế 1 con chip hỗ trợ video decoder tuân thủ theo đúng api của openmax-il thì bạn có thể nhanh chóng tích hợp được vào các hế thống trên :-), và bán con chip đó luôn được để kiếm xèng.

Chi tiết openmax thì vào trang chủ của nó để tham khảo ở đây [[3]](https://www.khronos.org/openmax/).
Thông tin các openmax-il component trên RPI thì tham khảo chỗ này [[5]](http://www.jvcref.com/files/PI/documentation/ilcomponents/index.html).

### 3. Thực hiện transcode video trên RPI.
#### 3.1. Thực hành transcode với RPI.
Omxplayer là cli hoạt động rất ổn định khi dùng play video trên RPI. Mình vẫn dùng để mở clip tàu điện Nhật Bản phục vụ ông con thích tàu xe.
Omxplayer sử dụng hardware decoder của RPI, và tất nhiên là thông qua openmax-il, cấu trúc của nó như hình dưới.

![dec_rpi](/assets/2018/07/dec_rpi.png)

Xuất phát từ ý tưởng dùng RPI để chuyển đổi video streaming mpeg2-video đang có sẵn thành h.264 để giảm bitrate nhằm tiết kiệm băng thông. Dựa trên omxplayer
với một chút sửa đổi nhỏ sau:
- Bỏ audio decoder, vì audio chiếm băng thông không đáng kể, không cần thiết transcode nên audio vào thế nào cho ra thế đó.
- Cắt bỏ phần xử lý hiện thị (render component), vì chỉ cần chuyển đổi sang video format khác, kết quả sẽ streaming hoặc lưu thành file.
- Thêm component encoder, nối vào ngay sau decoder. Để thực hiện encode lại ảnh, kết quả của bộ decoder sau khi giải mã đầu vào.
- Thêm phần xử lý output streamer, module này có nhiệm vụ lưu audio + video sau khi convert thành file hoặc streaming qua udp hoặc tcp/ip hoặc protocol nào đấy.

Sau khi sửa đổi thì cấu trúc nó thay hình đổi dạng như dưới.
![transcode_rpi](/assets/2018/07/transcode_rpi.png)

Source code & readme hướng dẫn sử dụng chứa ở [đây](https://github.com/truongpt/omxtranscoder)

Kết quả chạy thử, đạt được realtime và bitrate giảm 1 nửa.
- input http streaming: mpeg2-video,size 720×576, 25fps, bitrate 4mbps.
- output udp streaming: h.264, size 720×576, 25fps, bitrate 2mbps.

Khi play stream gốc và stream sau khi đã transcode thì chất lượng theo đánh giá chủ quan là tương đương nhau. Cần chú ý rằng, đây chỉ là về mặt visual, còn nén video là nén mất dữ liệu (lossly) do đó cái output không bao giờ bằng được input nếu nói trên quan điểm thông tin.

- Hiện tại đang có các điểm hạn chế cần điều tra và cải thiện:
  - Chạy được tầm 1h ~ 2h thì tự dưng lăn quay là treo → bug cần điều tra.
  - Openmax-il có định nghĩa 2 kiểu kết nối để component truyền data cho nhau, là tunnel (kết nối trực tiếp) và non-tunnel (kết nối gián tiếp thông qua IL client). Định dùng tunnel cho đơn giản, nhưng thử mãi không được nên đang dùng non-tunnel, thành ra quản lý buffer đang hơi stupid nên output buffer của decoder được copy sang encoder. → Cần điều tra lại đển dùng tunnel hoặc improve việc quản lý buffer để bỏ xử lý copy.
  - Phần output streamer module cần design là 1 thread độc lập, nhận video/audio buffer ở component trước đó thông qua queue, nhưng hiện tại đang thực hiện như bằng context của video & audio (được buffer nào thì streaming luôn).

#### 3.2. Dùng ffmpeg.
Đợt này có chút thời gian, định quay lại xử lý mấy hạn chế & bug của 3.1 thì mới để ý thấy ffmpeg nó cũng support openmax rồi, như vậy đơn giản thế này thôi.
- Clone ffmpeg và tham khảo chỗ [này](https://github.com/legotheboss/YouTube-files/wiki/(RPi)-Compile-FFmpeg-with-the-OpenMAX-H.264-GPU-acceleration) để enable omx khi compile.
- Nếu ngại complile từ source code thì có thể cài đặt ffmpeg thông qua repo của RPI, package đã được enable omx: sudo apt-get install ffmpeg

Dùng command dưới là xong :-).
```
ffmpeg -c:v mpeg2_mmal -i http://address_input -c:a copy -c:v h264_omx -b:v 2000k -f mpegts udp://address:port
```

Tuy nhiên có vẻ có vấn đề với input streaming interlace, ngoài ra chưa stress test nên chưa biết thế nào. Từ POC (proof-of-concept) đến Mass Product là một khoảng cách lớn, haizz …

- 24/07/2018 update: Input stream đang sử dụng là interlace, trong khi đó bộ encoder h.264 trên RPI không support interlace nên aspect ratio output stream bị sai. Có thể cần xử lý de-interlace trước khi encode. Hoặc với video hiện tại thì có thể dùng encoder bằng software encoder (libx264) như command dưới, sử dụng option encode performance gần cao nhất, với video size 720×576 thì vẫn đạt được realtime, tuy nhiên con chip nóng quá, không dám chạy stress-test vì sợ nó ngỏm.
```
ffmpeg -c:v mpeg2_mmal -i http://address_input
-c:v libx264 -preset superfast -f mpegts -b:v 2000k -s 720×576
udp://address:port
```
- P/S: Lưu ý, RPI mặc định chưa enable hardware mpeg2-video codec, muốn dùng phải bỏ tiền ra mua ở [đây](http://www.raspberrypi.com/mpeg-2-license-key/).

### Tham khảo.
- [1] https://en.wikipedia.org/wiki/Transcoding
- [2] https://www.raspberrypi.org/forums/viewtopic.php?f=72&t=72260
- [3] https://www.khronos.org/openmax/
- [4] https://source.android.com/devices/media/
- [5] http://www.jvcref.com/files/PI/documentation/ilcomponents/
- [6] https://github.com/popcornmix/omxplayer
- [7] https://github.com/truongpt/omxtranscoder

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />