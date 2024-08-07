# 4-bit Full-Adder
*Mô phỏng mạch dùng LTspice, MICROWIND cho layout, glade cho LVS.

*Dùng công nghệ 130nm "130nm_bulk.lib"

I. Thiết kế 

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/fb010385-2dbd-41ea-ab31-6e20cf8c5d6b)

1. Biểu thức hàm.
   
![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/d1884059-e506-4408-881d-bb09d6ac068c)

Từ bảng trạng thái trên ta thấy có 2 giá trị ngõ ra S, CO tương ứng với 3 ngõ vào A, B, C. Vì vậy, ta cần rút gọn hai biểu thức S và CO.
Biểu thức logic rút gọn dưới dạng SOP (sum-of-products, tổng của tích). 

a. Ngõ ra CO:

CO = (A ) ̅.B.C + A .(B .) ̅C + A.B. (C ) ̅+A.B.C
Dùng bìa K – Map để rút gọn ta được CO = AB +AC +BC 

b. Ngõ ra S

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/6c2e4be8-4314-4af5-b86a-b43f540425ee)

2. Mạch ở mức transistor
 
 ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/c2a2612d-b0cc-4fc7-bdb2-33caa68d8e67)

Pull up: dùng pMOS chỉ bật khi ngõ vào là 0
Pull down: dùng nMOS chỉ bật khi ngõ vào là 1
Vẽ các transistor ở nhánh pull down trước sau đó đổi ngược lại nhánh pull up.
Transistor được mắc theo quy tắc tương ứng với dấu “.” Là nối tiếp, “+” là song song. Nhánh pull up thì ngược lại.
Ngõ ra CO = A.B + C.(A + B) 
Ngõ ra S = (A + B +C).(CO) ̅ + A.B.C


![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/802ede52-f0d8-49af-8e41-8118871523cc)

3. Mô phỏng ở mức schematics
   
   a. Định kích thướt

Kích thước của bóng bán dẫn có thể được thực hiện bằng cách sử dụng xấp xỉ độ trễ RC. Mô hình độ trễ RC giúp ước tính độ trễ mạch CMOS. Mô hình độ trễ RC xử lý các đặc tính dòng điện-điện áp IV và điện áp CV của tụ điện phi tuyến tính với mô hình điện trở và điện dung tương đương của chúng.
Mô hình độ trễ RC này xấp xỉ một bóng bán dẫn như một công tắc có một loạt điện trở hoặc điện trở hiệu dụng R (Là tỷ lệ giữa giá trị trung bình của Vds với Ids). Kích thước của một bóng bán dẫn đơn vị xấp xỉ bằng 4/2 lambda. Các mô hình mạch RC tương đương cho các bóng bán dẫn PMOS và NMOS được hiển thị bên dưới.

  ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/9e778190-1729-45f2-90e0-a9a6a5e14269)

  - Kích thướt PMOS: 
Đối với một bóng bán dẫn PMOS đơn vị, điện trở hiệu dụng với độ rộng k được cho bởi 2R/k.
Bằng cách xem xét mạng pull-up trong mạch trên, chúng ta sẽ tìm ra trường hợp xấu nhất (the worst-case) hoặc đường dẫn dài nhất đến VDD. Trong mạng trên, con đường B-A-A là con đường dài nhất (đường màu đỏ). Vì vậy, chúng ta có thể viết phương trình (2R/k)+(2R/k)+(2R/k) = R, trong đó R là điện trở hiệu dụng. Phương trình đưa ra giá trị của k = 6. Do đó, giá trị k của các bóng bán dẫn B, A và A sẽ là 6.

  - Kích thướt NMOS:

Đối với một bóng bán dẫn NMOS đơn vị, điện trở hiệu dụng với độ rộng k được cho bởi R/k.
Trong mạng trên, trường hợp xấu nhất hoặc đường dẫn dài nhất có thể được nhìn thấy là với hai bóng bán dẫn. (Các con đường AB, AC, và BC). Vì vậy, chúng ta có thể viết mối quan hệ 2 * R/k = R, Vì vậy, giá trị k của tất cả các bóng bán dẫn NMOS sẽ là 2 vì tất cả đều nằm trong đường dẫn dài nhất.

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/f53109b8-dff4-4719-9951-816bdfb8ed65)

 
   b. Mô phỏng dùng LTSpice
 ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/1769457e-5408-4545-a46c-56c68d6fc38e)

   c. Kết quả:
 ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/ae7cff42-c4e6-4280-893c-271fd6f0c769)

4. Layout mạch và kiểm tra DRC, LVS 
   a. Stick diagram
   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/0a67eb5a-f9d1-4056-b903-0e9433d0bf35)

   b. Layout trên phần mềm GLADE
 ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/128b0b60-a1a1-4f76-a69e-04086d20a340)

   d. DRC (design rule check)
  ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/de9025df-54ee-437b-91c2-4ed6fb3a7c68)

   e. LVS (layout vs schematic)
      Schematic trên GLADE
 ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/dab2b8ed-a4c9-42e2-9d23-41c2de1baf45)
![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/9b4e8f70-ed8f-4931-a586-ee24d7a257e3)

5. Microwind
   
   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/4a95b25f-9980-404c-94a2-0acc14c0777a)

- Kết quả mô phỏng sau layout:

   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/1860ebbf-2edb-4490-b0d5-5e05cdb16fb8)

   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/201fe404-580a-40b6-87f4-9bf7c2effdac)
II.Full adder 4 bit

1. Full adder 4-bit là gì ?
   
- Mạch cộng Full Adder 4-bit là một mạch logic kết hợp được sử dụng để thực hiện phép cộng số học cho hai số 4-bit. Nó sử dụng bốn mạch Full Adder để thực hiện phép cộng từng bit và tạo ra kết quả 4-bit và bit nhớ cộng (carry-out).
  
2. Hoạt động

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/ceb219d9-7637-4079-88a2-bc808772969f)

- Mạch Full Adder 4-bit bao gồm bốn mạch Full Adder độc lập. Mỗi mạch Full Adder lấy hai bit đầu vào tương ứng từ A và B (A0, A1, A2, A3 và B0, B1, B2, B3) và một bit nhớ cộng (carry-in) tương ứng từ mạch Full Adder trước đó (Cin0, Cin1, Cin2). 
- Mạch Full Adder 4-bit sẽ thực hiện phép cộng 4 bit của A và B và sinh ra tổng S0, S1, S2, S3 cùng với bit nhớ cộng Cout.
  
3. Schematic

   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/ffdb039c-c12b-4a8e-80c5-5004e55c84c2)

Kết quả mô phỏng trên LTSpice

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/94dca7b5-1d59-46a3-9760-250ad60bcabd)

4. Layout và post-layout

   ![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/4a309bb4-2766-48ec-a079-e2306b14107a)

![image](https://github.com/MrKhai14/Full-Adder/assets/127326200/edc31e94-1da7-4f9c-9ac0-007f06328f3d)
                                                   
                                                   
                                                   HẾT!
