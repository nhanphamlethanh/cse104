### **EIGROSS**
Tính thuế thu nhập cá nhân (tax) của từng nhân viên.
Biết:
- n: số lượng nhân viên
- n integers: lương sau thuế của n nhân viên => net salary
- tax rate = 10%

Công thức tính thuế:
    tax = gross * 10%
    net = gross - tax => gross = net + tax
=> tax = (net + tax) * 0.1
=> tax = 0.1*net + 0.1*tax
=> 0.9*tax = 0.1*net
=> tax = net/9

gross = net + tax
tax = gross * 10%
=> gross = net + gross*10%
=> net = gross * 90%
=> tax = net / 90 * 10


VD:
- Lương trên hợp đồng:
    Gross salary = 10_000_000
- Tax rate = 10%
=> tax = 1_000_000



### **EIGROSS2**
- Input: N (net salary)
- Output: X (gross salary)

Ý tưởng:

Công thức:
    net = gross - tax
    taxable = gross - 11_000_000

VD:
gross = 15_000_000
Phần lương sẽ bị tính thuế:
taxable = 4_000_000
=> tax = 4_000_000 * 5% = 200_000

=> net = gross - tax = 15_000_000 - 200_000 = 14_800_000

Phần lương đã bị áp thuế
taxed = net - 11_000_000 = 14_800_000 - 11_000_000 = 3_800_000

Từ taxed, tính số thuế phải đóng (tax):
Level 1:
    giới hạn dưới của ngưỡng 1: 
        min = 0
    số thuế tối đa có thể phải đóng ở ngưỡng 1:
        maximum_tax = 5_000_000 * 5% = 250_000
    => giới hạn trên của ngưỡng 1 là: 
        max =  5_000_000 - maximun_tax = 4_750_000
=> Level 1: 0 - 4_750_000

Level 2:
    min = 4_750_000
    MAXIMUM_TAX = 5_000_000*10% = 500_000
    NET THUỘC NGƯỠNG 2: 5_000_000 - 500_000 = 4_500_000
    max = min + NET THUỘC NGƯỠNG 2 = 4_750_000 + 4_500_000 = 9_250_000

0 ---> 5_000_000 ---> 10_000_000

taxed_1 = 4_750_000
taxed_2 = 4_500_000
=> tổng taxed: 9_250_000

Tương tự các level còn lại.



### **EIUMARKUP**
VD: n = 200 (khách hàng mua 200 món)
- 100 món đầu tiên: cost = 200
    => money = 100*200 = 20_000
- 100 món còn lại: cost = 199
    => money = 100*199 = 19_900
=> total = 20_000 + 19_900 = 39_900


Input:
    N: số sản phẩm được mua
Output:
    số tiền phải trả

Ý tưởng: dùng while

long N = sc.nextLong();
long tempN = N;
long cost = 200;
long pay = 0;

while (tempN > 0 && cost >= 180)
    pay += 100 * cost;
    tempN -= 100;
    cost--;

if (tempN > 0)
    pay += tempN * 180;

sysout(pay);

VD: n = 250; => 
tempN = 250
cost = 200
pay = 0
iteration 1: 
    pay = 100 * 200 = 20_000
    tempN = 150
    cost = 199
iteration 2:
    pay = 20_000 + 100 * 199 = 39_900
    tempN = 50
    cost = 198
iteration 3:
    pay = 39_900 + 100 * 198 = 59_700
    tempN = -50
    cost = 197
dừng vòng lặp.

pay = 59_700
=> sai ở iteration 3
=> sửa vòng lặp while:

long N = sc.nextLong();
long tempN = N;
long cost = 200;
long pay = 0;

while (tempN > 0 && cost > 180)
    if (tempN >= 100)
        pay += 100 * cost;
        tempN -= 100;
    else
        pay += tempN * cost;
        tempN = 0;
    cost--;

pay += tempN * 180;
sysout(pay);

VD: n = 250
i1:
    pay = 20_000
    cost = 199
    tempN = 150
i2:
    pay = 39_900
    cost = 198
    tempN = 50
i3:
    pay = 49_800
    cost = 197
    tempN = 0
dừng vòng lặp.
pay = 49_800 
=> đúng

Rút gọn vòng lặp:
while (tempN > 100)
    pay += 100 * cost;
    tempN -= 100;
    if (cost > 180)
        cost--;

pay += tempN * cost;
sysout(pay);

n = 250
i1:
    pay = 20_000
    tempN = 150
    cost = 199
i2:
    pay = 39_900
    tempN = 50
    cost = 198
pay += 50 * cost;

n = 300
i1:
    pay = 
    tempN = 200
    cost = 199
i2:
    pay =
    tempN = 100
    cost = 198
i3:
    pay =
    tempN = 0
    cost = 197
pay += tempN * cost += 0 * cost;

n = 2500