## Câu chuyện từ khóa Volatile

Về từ khóa volatile thì có rất nhiều bài giải thích rồi, ví dụ như [đây](https://kipalog.com/posts/Y-nghia-cua-tu-khoa-volatile-trong-C), [đây](https://stackoverflow.com/questions/246127/why-is-volatile-needed-in-c) và [đây](https://www.geeksforgeeks.org/understanding-volatile-qualifier-in-c/) nữa, tôi không muốn nhai đi nhai lại nhiều nữa.

Tuy nhiên vấn đề các tác giả đề cập đến thường là việc giá trị “biến thay đổi bất thường”, tôi không hiểu ý bất thường ở đây cụ thể là gì, bất thường đối với ai, nhưng có vẻ như là bất thường theo nghĩa trình biên dịch đọc code.
Để chắc bắp, nên tham khảo chính xác [đặc tả C](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1124.pdf) (or C++) xem nó nói gì, nhưng sờ vào đặc tả mới thấy nó không dễ đọc như tôi vẫn tưởng 😦

```
An object that has volatile-qualified type may be modified in ways unknown to the implementation or have other unknown side effects. Therefore any expression referring to such an object shall be evaluated strictly according to the rules of the abstract machine, as described in 5.1.2.3.
```

Có thời gian nữa thì chắc nên nghiền ngẫm thêm chút vì thuật ngữ nghe là lạ, nhưng có thể tạm hiểu là từ khóa volatile để chỉ ra rằng biến đó có thể được thay đổi theo cách không rõ, không nhận biết được (mk, tiếng việt mình ngu quá, dài dòng vậy chứ có khi dùng từ “bất thường” là hợp lý nhất), cho nên việc tham chiếu biến đó phải tuyệt đối tuân thử đúng qui tắc máy :-o. Kết hợp thêm các ví dụ tham khảo thì tôi đang tạm hiểu ý là những chỗ đã liên quan đến từ khoá volatile thì phải tuyệt đối làm theo đúng từng mệnh lệnh mà mã nguồn đã được viết ra.  
Dùng Google tìm kiếm thì có thể tóm tắt vài tình huống dưới, mà biến bị thay đổi một cách bất thường đối với trình biên dịch, làm cho nó không nhận thức được việc thay đổi đó.
- Trong chương trình có xử lý ngắt, vì xử lý ngắt tạo tình huống đặc biệt.
- Xử lý song song đa luồng, các luồng có sử dụng biến chung.
- Vùng nhớ sử dụng cho IO map.

Chính vì trình biên dịch không có khả năng (?) nhận thức, nhận biết được toàn bộ những thay đổi liên quan đến biến có mang từ khoá volatile, do đó nó phải tuân thủ từng dòng code chứ không được suy đoán, mà mục đích thường là để tối ưu khi biên dịch mã nguồn.  
Tôi thì vẫn nghĩ chỉ có trường hợp 3 do trình biên dịch không thể đủ thông tin nên mới có thể làm sai khi tiến hành tối ưu code, chứ trường hợp interrupt hay xử lý đa luồng, thì rõ ràng mọi thứ trình biên dịch đều có thể nhận thức được, tôi không cho rằng cái đó là biến được thay đổi một cách bất thường. Tuy nhiên vì chưa có hiểu biết gì về cách tối ưu của trình biên dịch nên tôi cũng chỉ đưa ra nhận định chủ quan.

Sau khi đọc bài viết [chỗ này](https://kipalog.com/posts/Embedded--Tu-Khoa-Volatile-Trong-C), tôi đã thử 1 sampe code để test với gcc 6.3.0, dùng signal interrupt từ bàn phím, nhưng tối ưu hóa đủ mọi option vẫn không bị lỗi. Sau khi được tác giả gợi ý dùng fake interrupt bằng timer thì lại đúng là bị lỗi nếu không dùng volatile thật.  
Dù sao chăng nữa thì tôi vẫn giữ quan điểm volatile chỉ cần trường hợp map IO do tác động thực sự từ yếu tố bên ngoài mà trình biên dịch có mắt cũng chả thấy được, à hoặc có thể một trường hợp là cố tình dump code theo ý người viết, mà thường thấy là tạo delay  cái này thường thấy khi lập trình cho vi điều khiển, do thư viện không hỗ trợ hàm delay, điều này cũng làm cho trình biên dịch phán đoán là đoán mã đó thừa và thực hiện tối ưu, do nó không hiểu “ngu ý” của người viết. Còn lại với những trường hợp mà bản thân trình biên dịch có đầy đủ thông tin nhưng vẫn biên dịch lỗi nếu không có volatile thì tôi nghĩ có khi phải xem xét lại bản thân trình biên dịch.

Tóm lại từ khóa volatile dùng để nói cho trình biên dịch đấy là vùng cấm, code thế nào thì hãy làm đúng như thế, mày mới chỉ biết 1 chứ chưa biết 2, phần mày đang biên dịch chỉ là 1 phần nhỏ trong hệ thống lớn, nên đừng có khôn lỏi vào chỗ đó, đừng dựa vào nhận định chủ quan mà tiến hành thay đổi code để thực hiện tối ưu.  

Câu chuyện đến đây có lẽ là xong rồi, tuy nhiên có lẽ  ta dễ thấy có gì đó hơi không tự nhiên lắm, do nó chỉ bị lỗi khi yêu cầu trình biên dịch thực hiện tối ưu, vậy nếu trình biên dịch “ngây thơ” bảo gì làm nấy thì có lẽ là ta chẳng cần từ khóa volatile làm gì. Mà về tính năng tối ưu trong trình biên dịch thì tôi nghĩ nó chỉ phát triển sau này. Lúc xây dựng C không rõ trình biên dịch mà cụ Dennis Ritchie dùng có những tính năng gì (tôi không rõ ông làm thế nào để xây dựng ra C nên chỉ phán đoán thôi, nhưng dù sao chắc cũng phải vừa xây dựng đặc tả thì cũng phải song song xây dựng 1 trình biên dịch để kiểm thử).

Kiểm ra lại [đặc cả ngôn ngữ C phiên bản đầu tiên](https://www.ccapitalia.net/descarga/docs/1978-ritchie-the-c-programming-language.pdf) thì chưa có thật, nó chỉ được thêm vào từ [phiên bản số 2](https://www.dipmat.univpm.it/~demeio/public/the_c_programming_language_2.pdf). Từ đó liệu ta có thể phán đoán là trong quá trình phát triển tính năng tối ưu code của trình biên dịch, nó lại yêu cầu ngược lại đặc tả phải thêm từ khóa volatile?

Như vậy “điều lệ” ban ra đã rõ ràng, tuy nhiên “chi bộ” Kernel Linux lại không tuân thủ, à cũng nói thêm là “chi bộ” này được “đồng chí” Tovard Linux thành lập từ 1990 (chú ý là [“đồng chí” Ngô Thời Nhiệm](http://vietinfo.eu/chuyen-phiem/dong-chi-ngo-thoi-nhiem-den-cac-vua-hung-deu-la-nguoi-ngoai-hanh-tinh.html) không nằm trong chi bộ này). “chi bộ” này đã ra 1 “thông tư” nói [không với volatile](https://www.kernel.org/doc/html/v4.17/process/volatile-considered-harmful.html) cơ bản có 2 điểm.

- Trong mọi trường hợp trong kernel linux đều không thấy cần volatile.
- Nếu cần thì đấy là BUG.

“Thông tư” đã viết rất rõ ràng nên ai muốn biết mời tham khảo. Tìm hiểu thêm về “chi bộ” này ta còn bắt gặp nhiều điểm bất thường khác nữa, phải chăng chính điều đó tạo nên đặc trưng cho Kernel Linux.

#### Tham khảo
- http://publications.gbdirect.co.uk/c_book/chapter8/const_and_volatile.html
- http://publications.gbdirect.co.uk/c_book/

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />