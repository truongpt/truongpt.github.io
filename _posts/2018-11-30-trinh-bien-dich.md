## Trình biên dịch

Làm phần mềm ít ai không biết đến cái gọi là trình biên dịch, tuy nhiên cũng đặc thù từng công việc mà mức độ hiểu biết về trình biên dịch có khác nhau.
Tôi làm về hệ thống nhúng (rất không muốn dùng từ này thay từ embedded trong tiếng Anh, nhưng cũng phải dùng cho đậm đà bản sắc dân tộc), là mảng công việc rất rất cần hiểu sâu sắc về trình biên dịch, nhưng đáng buồn là giờ tôi mới tìm hiểu, thôi thì chậm hơn là không.

Trong công việc phần mềm, thì trình biên dịch được hiểu ngắn gọn là phần mềm chuyển từ mã nguồn do lập trình viên viết ra, biến thành mã máy (trong trường hợp dotNET hay Java chắc phải hiểu khác chút).

Trình biên dịch thường là do các công ty phát triển môi trường phát triển (IDE) cho lập trình viên viết ra, nổi bật như Microsoft, với trường hợp này trình biên dịch tích hợp trong môi trường phát triển nên lập trình viên cũng không cần để ý quá nhiều. Bên cạnh đó các trình biên dịch mã nguồn mở cũng chả kém cạnh, mà đứng đầu là GCC.

Có thể tham khảo về các thể loại trình biện dịch trên [Wiki](https://en.wikipedia.org/wiki/List_of_compilers), với trình biên dịch cho ngôn ngữ C thì chỗ [này](https://en.wikipedia.org/wiki/List_of_compilers#C_compilers).

Trình biên dịch phải được phát triển rất cẩn thận, vì nếu trình biên dịch mà có lỗi thì ảnh hưởng rất lớn trong việc phát triển các phần mềm dùng trình biên dịch đó. Nếu xuất hiện tình huống lỗi phần mềm đang phát triển, mà nó lại do cái lỗi kia của trình biên dịch thì đúng là ác mộng, không khác gì việc vẽ đường thẳng bằng một cái thước cong. Tuy nhiên trên thực tế lỗi của trình biên dịch vẫn như sao trời mùa hạ, ví dụ [danh sách lỗi](https://gcc.gnu.org/bugzilla/) được báo cáo của GCC chẳng hạn, biết làm sao được nó cũng chỉ là phần mềm thôi mà. Cách đấy hơn 2 năm, tôi cũng đã từng ăn quả đắng khi trình biên dịch cho hệ thống firmware video encoder bị lỗi khi biên dịch phép tính 64bit, do không thể đợi lỗi này được xử lý ở trình biên dịch, mà phải đi vòng (workaround) bằng cách thay thế toàn bộ tính toán 64bit bằng một thư viện mới xử lý thông qua trình toán 32bit.

Công việc từ trước đến này tôi chỉ dùng GCC, ngoài việc hỗ trợ nhiều ngôn ngữ, nó còn hỗ trợ hầu hết các platform, thành ra tôi luôn nghĩ nó là “độc cô cầu bại” trong thế giới công việc nhúng. Nhưng ai có ngờ lời ~xưa đã chứng~, đâu ra lại xuất hiện 1 thằng [clang](https://clang.llvm.org/) đã có chiều hướng đè bẹp GCC? Tôi chưa thử so sách xem chất lượng mã máy được biên dịch ra thế nào, còn về tốc độ biên dịch thì GCC hít khói. Nói về clang thì nó chỉ là mặt tiền (bước phân tích mã nguồn) của một thứ đang sợ hơn là [LVMM](https://llvm.org/), dự án này bắt đầu từ nghiên cứu của [Chris Lattner](http://www.nondot.org/sabre/). Cầu thủ này được Apple thuê hơn 10 năm, trong thời gian đó thì clang xuất hiện và thay thế GCC trong các môi trường phát triển của Apple. Sau khi không đá cho Apple nữa mà chuyển sang chơi ô tô với Elon Musk, nhưng chỉ đá được gần 6 tháng chắc thấy đá không vừa chân nên chuyển qua chơi AI với google.

Cưỡi ngựa xem hoa thế là đủ rồi, đã đến giờ “học đi đôi với hành”, để hiểu hơn về trình biên dịch thì cũng nên một lần trong đời thử viết 1 con compiler be bé xem nó ra cái gì. Để làm được cái “be bé” đó trước hết chắc phải đọc kỹ cái đống dưới.

#### BOOK.
- [1] https://www.amazon.com/dp/0321486811/?tag=stackoverflow17-20
- [2] https://www.amazon.com/dp/0471976970/?tag=stackoverflow17-20
- [3] https://holub.com/goodies/compiler/compilerDesignInC.pdf

#### Other.
- [1] https://www.quora.com/How-do-I-make-a-compiler-using-C-language
- [2] https://holub.com/compiler/
- [3] https://norasandler.com/2017/11/29/Write-a-Compiler.html
- [4] http://scheme2006.cs.uchicago.edu/11-ghuloum.pdf
- [5] https://softwareengineering.stackexchange.com/questions/165543/how-to-write-a-very-basic-compiler
- [6] https://www.codeproject.com/articles/30353/designing-a-compiler