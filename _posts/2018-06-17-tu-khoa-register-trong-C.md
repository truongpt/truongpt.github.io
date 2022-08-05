## Từ khóa register trong C
Trong lập trình nhúng (embedded programming), thi thoảng hay bắt gặp từ khóa register, thường là những chỗ tính toán loằng ngoằng, bit biếc dịch ngược dịch xuôi. Register được dùng đặt trước kiểu dữ liệu khi khai báo biến. Tác dụng của từ khóa register, nói một cách ngắn gọn là làm tăng hiệu năng(performance) của chương trình.

Thêm cái của nợ này vào thì tại sao có thể tăng được hiệu năng?. Mà thực sự tăng thật thì tăng được bao nhiêu?
Để thêm phần sinh động, thử một ví dụ nhỏ dưới xem nó có ra cái gì không?
```
void main()
{
  clock_t start, end;
  double t;
  int i; // không dùng register
  //register int i; // sử dụng register
  start = clock();
  while(i < 0xFFFFFFFF) i++;
  end = clock();
   
  t = ((double) (end – start)) / CLOCKS_PER_SEC;
  printf("time used %f\n",t);
}
```

Biên dịch với gcc version 6.3.0
Chạy trên Raspberry Pi 2B (ARMv7 Processor rev 5 (v7l)).
- Sử dụng từ khóa register: time used 9.583080 giây
- Không sử dụng từ khóa register: time used 38.256520 giây

Ví dụ trên cho thấy dùng từ khóa register, thì hiệu năng nó tăng thật, riêng trong trường hợp này thì cũng đang kể đấy chứ nhỉ :-).Tất nhiên cải thiện được bao nhiêu thì phải tùy vào hoàn cảnh cụ thể khi sử dụng, mức độ sử dụng biến đó … Nhưng mà ngon lành vậy thì toàn bộ khai báo biến trong chương trình cứ mặc định thêm luôn từ khóa này thì chuyện gì xẩy ra?.\
Để hiểu được điều đó thì trước hết thử xem tại sao hiệu năng nó tăng?\
Quay lại với vấn đề cơ bản hơn một chút, trong kiến trúc của vi xử lý thì ALU (Arithmetic Logic Unit) là con trâu đóng vai trò xử lý các tính toán số học. Dữ liệu đưa vào làm việc với ALU phải chứa trong một vùng đặc biệt, gọi là các thanh ghi(register), và ALU chỉ làm việc với đống thanh ghi đó. Trong khi đó các biến khai báo trong chương trình thì đặt ở bộ nhớ ngoài (RAM chẳng hạn …). Do đó với khai báo biến thông thường, để thực hiện một phép tính thì cần có 3 bước.
- ① Nạp giá trị từ vùng nhớ chứa biến vào register
- ➁ Yêu cầu ALU xử lý register vừa được nạp giá trị.
- ③ Đưa kết quả vừa xử lý của ALU ra ngoài vùng nhớ chứa biến.
Hình dung thô thiển như hình vẽ dưới đây.

![alu](/assets/2018/06/alu.jpg)

Khi thêm từ khóa register để khai báo biến, thì tức là ta đã yêu cầu trình biên dịch ưu tiên đặc biệt dành luôn vùng register để chứa biến đó. Và hiển nhiên khi thực hiện tính toán trên biến đó thì giảm được bước ①&③, giảm bớt thủ tục thì hiệu năng nó tăng lên là chuyện dễ hiểu :-).\
Quay lại với ví dụ trên, để đảm bảo đúng như thánh phán, thử thêm option “-save-temps” để lấy tập mã lệnh assembly xem nó có thật vậy không.
```
gcc register.c -o test -save-temps
```

Đoạn mã assembly ở dưới tương ứng với vòng while loop ở ví dụ trên. Dễ thấy chỗ bôi màu đó khi không dùng từ khóa register tương ứng với bước ①&③ ở trên. Còn khi dùng từ khóa register thì trình biên dịch nó dùng luôn thanh ghi r4 cho việc chứa biến i.\
p/s: Nếu không dễ thấy thì tự tra　cứu lại lệnh assembly của ARM

Không sử dụng từ khóa register
```
ldr r3, [fp, #-8] // bước ①
add r3, r3, #1
str r3, [fp, #-8] // bước ③
.L2:
ldr r3, [fp, #-8]
cmn r3, #1
bne .L3
```

Sử dụng từ khóa register
```
.L3:
add r4, r4, #1
.L2:
cmn r4, #1
bne .L3
```

Đến đây, ta thấy rõ ràng khi dùng từ khóa register, thì thay vì dùng bộ nhớ ngoài đển lưu biến thì chương trình sẽ sử dụng luôn register để lưu biến đó. Cái gì ngon, quí thì dĩ nhiên hiếm, register cũng thấy, số lượng register rất nhỏ so với bộ nhớ ngoài, mà đây còn là tài nguyên dùng chung. Do đó không thể chơi kiểu vô tổ chức để thằng nào thích lấy làm đồ riêng thì lấy được. Tùy từng tình huống, yêu cầu để lựa chọn phần xử lý nào nên sử dụng register để tăng hiệu năng mà có thể chấp nhận cho nó xin một vài register về làm của riêng.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" />
