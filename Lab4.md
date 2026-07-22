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

