### **EIUCUBES2**
- Xây kim tự tháp
- Biết:
    - Có k loại gạch. Mỗi loại gạch xây được 1 kim tự tháp 
        => Xây k kim tự tháp
    - Mỗi loại gạch có n_i viên gạch
- Yêu cầu: tính chiều cao của mỗi kim tự tháp

Giả sử: Xét loại gạch i bất kỳ
- Số lượng: N
- Điều kiện: 1 <= N <= 10^18

Ý tưởng: binary search
- low = 0
- high = 2_000_000
- mid 

Giả sử: chiều cao của kim tự tháp h => có h layers

Công thức tính số viên gạch cần cho layer h:
    bricks for layer h = 1 + 2 + 3 + ... + (h-1) + h
=> rút gọn công thức:
    bricks for layer h = (1 + h)*h/2


Công thức tính tổng số viên gạch cần cho toàn bộ kim tự tháp có h layers:
    total_bricks = bricks_for_layer_1 + bricks_for_layer_2 + ... + bricks_for_layer_h
    
    layer 1: 1              => h = 1: số gạch = 1 * (1 + 1)/ 2 = 1
    layer 2: 1 + 2          => h = 2: số gạch = 2 * (2 + 1)/ 2 = 3
    layer 3: 1 + 2 + 3
    ..
    layer h: h*(h + 1)/2

    Gọi i là biến đếm layer. i nằm trong khoảng từ 1 tới h
    => total_bricks = sum(i*(i+1)/2) với i chạy từ 1 tới h

    Gọi: total_bricks = A1 + A2, với:
    
long height = 0;
while (low <= high)
    long mid = (low + high) / 2;
    long h = mid;

    long total_bricks = h(h+1)(h+2)/6;

    if (total_bricks <= n)
        height = mid;
        low = mid + 1;
    else 
        high = mid - 1;


### **EIUCHRMS**
- Input:
    + n: số lượng hóa đơn
    + n số tương đương với giá trị của n hóa đơn (lần lượt)
- Output: tổng thu nhập của cửa hàng
    total_income = tổng giá trị của tất cả các hóa đơn sau khi chiết khấu.

VD:
n = 5
bill_1 = 10_000 
bill_2 = 1_000_000 
bill_3 = 3_000_000 
bill_4 = 5_000_000 
bill_5 = 100_000_000

total_income = 100_659_700

Xét lần lượt từng hóa đơn:
+ bill_1 = 10_000 => chiết khấu: 3%
=> bill_1 = 10_000 - 10_000/100*3 = 9_700
+ bill_2 = 1_000_000 => chiết khấu: 3%
=> bill_2 = 1_000_000 - 1_000_000/100*3 = 970_000
+ bill_3 = 3_000_000 => chiết khấu 4%
=> bill_3 = 3_000_000 - 3_000_000/100*4 = 2_880_000
+ bill_4 = 5_000_000 => chiết khấu: 4%
=> bill_4 = 5_000_000 - 5_000_000/100*4 = 4_800_000
+ bill_5 = 100_000_000 => chiết khấu: 8%
=> bill_5 = 100_000_000 - 100_000_000/100*8 = 92_000_000

=> total_income = bill_1 + bill_2 + ... + bill_5
                = 9_700 + 970_000 + 2_880_000 + 4_800_000 + 92_000_000
                = 100_659_700

Tổng quát hóa:
- Có 8 ngưỡng: 
    1. <=2tr 
    2. <=5tr
    3. <=10tr
    4. <=20tr
    5. <=50
    6. <=100
    7. <=200
    8. >200
- Xét lần lượt từng hóa đơn:
    long bill = sc.nextLong();
    - So sánh với từng ngưỡng, xem hóa đơn thuộc ngưỡng nào
        => biết được số % chiết khấu
            rate = ?
    - Tính số tiền sau khi trừ chiết khấu: là số tiền thực tế khách hàng phải trả
        long actual_pay = bill - bill/100*rate;
    - Cộng vào biến tổng thu nhập:
        total_income += actual_pay;

Hướng dẫn:
long total_income = 0;
Cách 1: if-else
    long bill = sc.nextLong();
    if (bill <= 2_000_000)
        int rate = 3;
        long actual_pay = bill - bill/100*rate;
        total_income += actual_pay;
    else if (bill <= 5_000_000)
        int rate = 4;
        long actual_pay = bill - bill/100*rate;
        total_income += actual_pay;


### **EIUSALES**
- Input:
    figure: doanh số bán hàng của nhân viên X
- Output:
    bonus: tiền thưởng của nhân viên X

VD:
figure = 10

Hướng dẫn: dùng array

long figure = sc.nextLong(); //doanh số

long[] rate = {2, 3, 4, 5, 6, 7};

Cách 1:
long[] limit = {0, 20, 50, 200, 500, 2000};

double bonus = 0;
for (int i=0; i<limit.length-1; i++)
    if (figure > limit[i])
        long current_limit = Math.min(figure, limit[i+1]) - limit[i];
        bonus += current_limit / 100 * rate[i];
if (figure > 2000)
    bonus += (figure - 2000) /100 * 7;

Cách 2: tương tự bài DISCOU (Lab 2)
long[] limit = {20, 50, 200, 500, 2000, Long.MAX_VALUE};


### **EIMEMCARD**
- Input:
    n: số lượng mua sắm
    n số nguyên => giá trị hóa đơn của từng lần mua
- Output:
    n số => số tiền được giảm ở từng lần mua

VD: 1 khách hàng mua 5 lần tại cửa hàng, với hóa đơn mỗi lần mua lần lượt như sau
n = 5
1 khách hàng mua 5 lần tại cửa hàng, với hóa đơn mỗi lần mua lần lượt như sau:
bill_1 = 500_000            => discount = 0 => chưa được xếp membership 
bill_2 = 2_000_000          => discount = 0 => xếp hạng Starter 
bill_3 = 6_000_000          => discount = 120_000 => duy trì hạng Starter
bill_4 = 50_000_000         => discount = 1_000_000 => tăng hạng Diamond
bill_5 = 3_000_000          => discount = 150_000 => duy trì hạng Diamond

Hướng dẫn:

double total_pay = 0;
for (int i=0; i<n; i++)
    double bill = sc.nextDouble();
    
    double discount = 0;

    if (total_pay >= 200_000_000)
        discount = bill * 0.07;
    else if (total_pay >= 50_000_000)
        discount = bill * 0.05;
    else if (total_pay >= 20_000_000)
        discount = bill * 0.03;
    else if (total_pay >= 1_000_000)
        discount = bill * 0.02;
    
    total_pay += bill;

    sysout(discount);
