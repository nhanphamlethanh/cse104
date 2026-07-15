### **EIMONE**
Beo có b đồng. Beo muốn đổi b đồng này thành nhiều tờ tiền có mệnh giá 20, 10, 5, 1.
Beo muốn đổi được số tờ tiền ít nhất có thể. 
VD: Beo có 72 đồng
=> 3 tờ 20, 1 tờ 10, 2 tờ 1 (greed algorithm - thuật toán tham lam)

Ý tưởng:
- Sử dụng if-else:
    - Gọi số tiền còn lại cần đổi là left:
        Khai báo int left = b;
    - If left >= 20:
        num_20 = left / 20 (72/ 20 = 3)
        left = left - num_20*20 
    hoặc left -= num_20*20
    hoặc left = left % 20
    - If left >= 10:
- Sử dụng array kết hợp for loop:
    int[] d = {20, 10, 5, 1};
    int left = b;
    for (int i=0; i<d.length; i++) 
        int num = left / d[i];
        if (num > 0)
            sysout(d[i] + " " + num);
        left %= d[i];

### **EIPOINT**
Quy đổi điểm môn học:
- input: điểm dạng số
- output: điểm dạng chữ

ý tưởng:
- Sử dụng 2 array:
    - Lưu các ngưỡng điểm dạng số:
        int[] num = {90, 85, ...};
    - Lưu các ngưỡng điểm dạng chữ:
        String[] cha = {"A", "A-",...};
- Duyệt vòng lặp, kiểm tra điểm nhập vào thuộc ngưỡng nào => in ra điểm chữ ở ngưỡng đó:
    int score = sc.nextInt();
    for (int i=0; i<num.length; i++)
        if (score >= num[i])
            sysout(cha[i]);
            break;


### **EIUTHU**
Cho 2 chuỗi ký tự S1 và S2.
Phần đầu của S2 sẽ trùng lặp với phần cuối của S1. 
Tìm độ dài ngắn nhất của bức thư.

VD:
S1 = trunghoccosotran
S2 = trandainghia
=> overlap = 4

S1.length = 16
S2.lentgh = 12
=> Số ký tự tối đa có thể bị lặp ở 2 phần thư?:
    maxOverlap = Math.min(S1.length, S2.length);

Gợi ý: 
- phương thức .substring() để lấy 1 phần ký tự trong một chuỗi ký tự.
- phương thức .equals() để so sánh 2 chuỗi ký tự

Duyệt vòng lặp for "maxOverlap" lần:
int numOverlap = 0;
for (int i = maxOverlap; i>=1; i--) 
    // Lấy đuôi của S1
    String suffixS1 = S1.substring(S1.length - maxOverlap);
    String prefixS2 = s2.substring(0, i);
    if (suffixS1.equals(prefixS2))
        numOverlap = i;
        break;
int shortest = S1.length + S2.length - numOverlap;


### **EIEVERYN**
VD:
in:
m = 4
n = 3
int[] A = {1, 3, 2, 1}
out: Yes

Yêu cầu: kiểm tra array A có chứa đầy đủ các số từ 1 tới n.
Gợi ý:
- Tạo 1 array khác, đặt tên B, có độ dài n+1
=> B có length n+1 là để? 
=> B.length()=n+1 => index của array B bắt đầu từ 0 tới n
=> tồn tại đầy đủ các số từ 1 tới n

Với mỗi phần tử trong array A, nếu A[i] nằm trong khoảng từ 1 tới n => lưu lại trong array B.
boolean[] B = new boolean[n+1];
array B:
index: 0 1 2 3 4 ... n
value: 
for (int i=0; i<m; i++)
    if (A[i] >=1 && A[i] <= n)
        B[A[i]] = true;
Xét ví dụ:
A = {1, 3, 2, 1}
int[] B = new int[3+1];
trong vòng lặp:
i=0: A[0] = 1 => B[1] = true
i=1: A[i] = 3 => B[3] = true
i=2: A[2] = 2 => B[2] = true
i=3: A[3] = 1 => B[1] = true
sau vòng lặp, B được cập nhật:
B = {,true,true,true}

boolean hasEnough = true;
Duyệt thêm 1 vòng lặp, kiểm tra các vị trí từ 1 đến n trong array B:
    Nếu tồn tại 1 vị trí có giá trị false => A không có đầy đủ các số từ 1 tới n. 
    => cập nhật hasEnough = false;
Kết thúc:
Nếu hasEnough == true: in Yes
Ngược lại: in No


### **EIUTRIGLE**
- Cho array A chứa N số nguyên dương.
- Tìm số tam giác có thể hợp thành được từ 3 phần tử bất kỳ của mảng.
VD:
N = 5
A = {1 4 3 6 2}
sortedA = {1, 2, 3, 4, 6}
số tam giác: 2

Biết độ dài 3 cạnh a b c, 3 cạnh đó hình thành nên một tam giác, nếu:
   a + b > c
và a + c > b
và b + c > a

Nếu như biết được: a < b < c => c là cạnh lớn nhất
=> chỉ cần xét 1 điều kiện: a + b > c => đây là tam giác

Sắp xếp lại mảng A từ nhỏ đến lớn:
    Arrays.sort(A);
Cố định cạnh lớn nhất và lần lượt xét từng cặp cạnh nhỏ hơn
=> kiểm tra điều kiện
=> nếu thỏa mãn: count++;

Giá trị lớn nhất trong mảng A lúc này là A[n-1].

Gợi ý:
Duyệt vòng lặp với i chạy từ n-1 tới 2, với i là vị trí của cạnh lớn nhất(cạnh c):
    for (int i=n-1; i>=2; i--)
        int c = A[i];
        int a_index = 0;
        int b_index = i-1; //xuất phát từ n-2

        while (a_index < b_index)
            int a = A[a_index];
            int b = A[b_index];
            if (a + b > c) 
                count += b_index - a_index;
                b_index--;
            else 
                a_index++;


sortedA = {1, 2, 3, 3, 4, 6, 8, 9, 10}


### **EISNAIL**
Ốc sên bò lên 1 thân gỗ dài V mét.
Mỗi ngày: bò được A mét
Mỗi đêm: lùi xuống B mét

Hỏi sau mấy ngày, ốc sên bò hết thân gỗ?

=> Mỗi ngày, ốc sên bò bao nhiêu mét? (A-B)
=> Gọi số ngày trọn vẹn (bao gồm cả sáng và đêm) ốc sên đi qua là:
    fullDay
=> Sáng của ngày cuối cùng, ốc sên tới đích.

Giả sử: sáng ngày cuối cùng, ốc sên bò A mét và tới đích.
thì, những ngày trước đó, ốc sên bò bao nhiêu mét? => (V-A)
=> fullDay = Math.ceil((V-A)/(A-B))

=> số ngày ốc sên cần để bò tới đích?
    result = fullDay + 1



        
String[] finger = {"cai", "tro", giua",....} => 18 lần tương ứng vị trí 18 ngón trong 1 chù kỳ
String[] hand = {"trai", "trai", "trai", "trai", "trai", 
                "phai", "phai", "phai", "phai", "phai", 
                "phai", "phai", "phai", "phai", 
                "trai", "trai", "trai", "trai"}

N
index = N % 18;
if (index == 0) {
    index = 18;
}

sysout("Ngon " + finger[index-1] + " cua ban tay " + hand[index-1])