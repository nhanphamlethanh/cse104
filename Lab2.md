### **EIUMADIS**
- Cho mảng có n số nguyên.
- Yêu cầu: Tìm giá trị tối đa của A[j] - A[i]
với 0 <= i <= j < n
=> i và j nằm trong khoảng [0, n-1]
và: j >= i
khi j = i: A[j] - A[i] = 0

VD:
n = 5
A = {2 4 1 5 3}
index: 0 1 2 3 4
value: 2 4 1 5 3

Xét trường hợp j > i:
Duyệt vòng lặp for để xét các cặp phần tử.
=> Duyệt như nào?

- Với mỗi j bất kỳ:
VD: j = 3 => A[j] = 5
=> Để A[j] - A[i] là lớn nhất, thì cần lấy A[j] trừ với A[i] nhỏ nhất có thể.
- Gọi min là phần tử nhỏ nhất có thể trong mảng:
    long min = A[0];
- Gọi maxDiff là giá trị lớn nhất của A[j] - A[i] cần tìm:
    long maxDiff = 0;
- Duyệt vòng lặp for với j chạy từ 1 tới n-1:
    for (long j = 1; j < n; j++)
        - Tính khoảng cách của A[j] hiện tại với giá trị min:
            long diff = A[j] - min;
        - So sánh diff với maxDiff và cập nhật maxDiff nếu diff lớn hơn maxDiff:
            if (diff > maxDiff)
                maxDiff = diff;
        - So sánh A[j] với min và cập nhật min nếu A[j] nhỏ hơn min:
            if (A[j] < min)
                min = A[j];
    Kết thúc vòng lặp.

VD:
A = {2 4 1 5 3}
index: 0 1 2 3 4
value: 2 4 1 5 3

min = A[0] = 2
maxDiff = 0
Duyệt vòng lặp for j:
j = 1: A[j] = 4
    - tính diff = A[j] - min = 4 - 2 = 2
    - so sánh: diff = 2 > maxDiff = 0
        => cập nhật: maxDiff = diff = 2
    - so sánh: A[j] = 4 > min = 2
        => bỏ qua
j = 2: A[j] = 1
    - tính diff = A[j] - min = 1 - 2 = -1
    - so sánh: diff = -1 < maxDiff = 2
        => bỏ qua
    - so sánh: A[j] = 1 < min = 2
        => cập nhật: min = A[j] = 1
j = 3: A[j] = 5
    - tính diff = A[j] - min = 5 - 1 = 4
    - so sánh: diff = 4 > maxDiff = 2
        => cập nhật: maxDiff = diff = 4
    - so sánh: A[j] = 5 > min = 1
        => bỏ qua
j = 4: A[j] = 3
    - tính diff = A[j] - min = 3 - 1 = 2
    - so sánh: diff = 2 < maxDiff = 4
        => bỏ qua
    - so sánh: A[j] = 3 > min = 1
        => bỏ qua


### **EIUBIRTH**
