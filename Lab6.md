Week 5: gửi tiết kiệm
Week 6: mua hàng trả góp

### **eipurchase**
Mua laptop trả góp.
- Giá laptop: V đồng
- Trả trước: N đồng
=> Nợ: (V-N) đồng
- Trả góp trong T tháng, M đồng/tháng.

=> sau T tháng, số nợ còn lại là?
    M*T - (V-N)

VD:
V = 20 triệu
N = 5 triệu
=> nợ = 20 - 5 = 15 triệu

T = 8 (tháng)
M = 2 triệu

=> số nợ còn lại sau T tháng: 0 đồng

Gọi số nợ ban đầu là X.
X = 15
Sau T1:
    - Cộng lãi:
        X = X * (1 + rate)
    =>  X = 15 * (1 + rate)
    - Trừ đi M (số tiền trả cố định mỗi tháng):
        X = X - M
    => X = 15 * (1 + rate) - M

Sau T2:
    - Cộng lãi:
        X = X * (1 + rate)
    =>  X = (15 * (1 + rate) - M) * (1 + rate)
    - Trừ đi M (số tiền trả cố định mỗi tháng):
        X = X - M
    => X = (15 * (1 + rate) - M) * (1 + rate) - M

Sau T3:
    - Cộng lãi:
        X = X * (1 + rate)
    =>  X = ((15 * (1 + rate) - M) * (1 + rate) - M) * (1 + rate)
    - Trừ đi M (số tiền trả cố định mỗi tháng):
        X = X - M
    => X = ((15 * (1 + rate) - M) * (1 + rate) - M) * (1 + rate) - M

Công thức tổng quát:
Sau T3:
  ((X * (1 + rate) - M) * (1 + rate) - M) * (1 + rate) - M
= X*(1 + rate)^3 - M * [(1 + rate)^2 + (1 + rate) + 1]

? Sau T4, công thức có trở thành:
    X*(1 + rate)^4 - M * [(1 + rate)^3 + (1 + rate)^2 + (1 + rate) + 1]

Chứng minh:
    (X*(1 + rate)^3 - M * [(1 + rate)^2 + (1 + rate) + 1])*(1 + rate) - M
=   X*(1 + rate)^4 - M * [(1 + rate)^3 + (1 + rate)^2 + (1 + rate)] - M


=> Công thức tổng quát:
Sau T tháng: 
số nợ còn lại = X * (1 + r)^T - M * [(1+r)^(T-1) + (1+r)^(T-2) + ... + (1+r)^0]
              = X * (1 + r)^T - M * sum ((1+r)^i) với i trong khoảng [0, (T-1)]

Rút gọn:       
    M * sum ((1+r)^i) với i trong khoảng [0, (T-1)]
=   M * (1 - (1 + r)^T) / (1 - (1 + r))
=   M * ((1 + r)^T - 1) / r

=> số nợ còn lại sau T tháng:
= X * (1 + r)^T - M * ((1 + r)^T - 1) / r

Biết: sau T tháng, số nợ còn lại phải bằng 0
=> X * (1 + r)^T - M * ((1 + r)^T - 1) / r = 0
=> tính r!

VD:
X = 15
T = 8
M = 2
=> r = ?

=> binary search

output: lãi suất r
1. nếu in r dạng r% (VD 5%) => in số 5 => giới hạn của r: low = 0; high = 100
2. nếu in r dạng thập phân => in 0.05 => giới hạn của r: low = 0.0; high = 1.0

=> bài này, output dạng 2
low = 0.0
high = 1.0




1. Tóm tắt đề bài
2. Thử tính toán với ví dụ => tìm calculating flow
3. Tìm công thức (với bài toán có công thức)

Cần chú ý: kiểu dữ liệu của input, output


Lab Test 2 và Final Exam. Format đề thi:
Q1: Lũy tiến
Q2: Lab
Q3: Binary search
Q4: Toán tư duy

Office Hour:


### **eiupurchase3**
Mua hàng trả góp
- Giá trị thật: P đồng
- Trả trước: M đồng
=> số nợ = (P - M)
- Thời gian trả góp: N tháng
- Lãi suất: R%/tháng

Yêu cầu: tính số tiền phải trả mỗi tháng (X)

X = (P-M) * R * (1 + R)^N / ( (1 + R)^N - 1 )



### **eibankloan2**
Vay tiền mua nhà.
- Số tiền: X đồng
- Lãi suất: r%/năm
- Mỗi tháng trả: Y đồng

Hỏi: sau bao lâu trả xong nợ => số tháng?

VD:
- Vay: 1 tỷ
- Lãi suất: 6%/năm
- Mỗi tháng trả 100 triệu
=> cần 11 tháng trả hết nợ.


Gọi số nợ còn lại là remainingDebt.
    double remainingDebt = X;
Mỗi tháng:
    + Cộng lãi:
        remainingDebt = remainingDebt*(1 + r/100/12);
    + Trừ số tiền trả góp:
        remainingDebt -= Y;

=> ý tưởng:
int months = 0;
while (remainingDebt > 0)
    remainingDebt = remainingDebt*(1 + r/100/12);
    remainingDebt -= Y;
    months++;
=> vòng lặp hoạt động khi chưa trả hết nợ => remainingDebt > 0



### **eibankloan3**
Mua xe trả góp.
- X: vay nợ
- Y: số tiền trả mỗi tháng
- N: số tháng trả góp
- r: lãi suất vay theo năm
- f: phí phạt trả sớm

Yêu cầu: tính dư nợ còn lại mỗi tháng.

VD:
- Vay: X = 1 tỷ
- Trả mỗi tháng: Y = 95 triệu
- Số tháng: N = 12
- Lãi: r = 6%
- Phí phạt: f = 3%

Vay 1 tỷ trong 12 tháng:
=> trung bình số nợ gốc cần trả mỗi tháng là?
    base = 1 tỷ / 12 = 83 triệu (83_333_333.33)

Tháng 1:
    - Nợ: debt = 1 tỷ
    - Tính lãi: 
        interest = debt * 0.06 /12 = 5 triệu
    - Biết, đã trả 95 triệu.
    => số tiền trả trước là?

    Trong 95 triệu bao gồm:
        - phần gốc cần trả trong tháng 1: base = 83_333_333.33
        - số lãi trong tháng 1: interest = 5 triệu
        => còn lại (95 triệu - 83_333_333.33 - 5 triệu) = 6_666_666.667
        => số tiền này bao gồm: số tiền gốc trả trước trong T1 + phí phạt
        Biết: phí phạt = 0.03 * số tiền gốc trả trước
        => có: số tiền gốc trả trước trong T1 
             + số tiền gốc trả trước trong T1*0.03 = 6_666_666.667
        => số tiền gốc trả trước trong T1 = 6_666_666.667 / 1.03 
                                          = 6_472_491.909

    Dư nợ còn lại sau tháng 1 = số nợ gốc ban đầu - số tiền gốc đã trả trong T1
    Biết: số tiền gốc đã trả trong T1 = base + số tiền gốc trả trước trong T1 = 83_333_333.33 + 6_472_491.909 = 89_805_825.24

    => Dư nợ còn lại sau tháng 1 = số nợ gốc ban đầu - số tiền gốc đã trả trong T1 = 1 tỷ - 89_805_825.24 = 910_194_174.8




