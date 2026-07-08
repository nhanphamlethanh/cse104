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
Mua quà. Có 2 loại quà:
- Màu xanh: giá X
- Màu đỏ: giá Y
- Phí đổi: Z
Tính minCost.

VD:
Cần mua:
    5 xanh
    7 đỏ
Giá:
    X = 2
    Y = 6
    Z = 3

Xét màu xanh:
    Giá: X = 2
    - Nếu mua 5 xanh, cần: 5*2 = 10 đồng
    - Nếu mua 5 đỏ và đổi thành xanh, cần:
        5*6 + 5*3 = 45
Xét màu đỏ:
    Giá: Y = 6
    - Nếu mua 7 đỏ, cần: 7*6 = 42 đồng
    - Nếu mua 7 xanh, và đổi qua đỏ:
        7*2 + 7*3 = 35 đồng < 42 đồng
    => Nếu cần mua 7 đỏ, nên mua 7 xanh và đổi thành 7 đỏ => tốn ít tiền hơn.

Ý tưởng:
- Với mỗi loại quà (xanh hoặc đỏ):
    - So sánh giá tiền 2 trường hợp:
        1. Mua trực tiếp loại quà màu đó
        2. Mua loại quà màu còn lại và đổi lại
    => Phương án nào tốn ít tiền hơn thì chọn phương án đó.
    => Dùng if/else hoặc Math.min()

Hướng dẫn:
- Input:
    B: xanh
    R: đỏ
    X
    Y
    Z
- Tính toán:
    1. Tính giá tiền tối ưu để 1 món quà màu xanh:
        - TH1: X
        - TH2: (Y+Z) => tốn Y để mua 1 món đỏ, và tốn thêm Z để đổi từ đỏ thành xanh.
        => công thức:
        costB = Math.min(X, Y+Z);
    2. Tương tự, tính cho màu đỏ.
        costR
    3. Tính tổng tiền:
        totalCost = B*costB + R*costR;

### **EIUCUBES**
Xây kim tự tháp.
Input:
    - n: Số lượng viên gạch
Output:
    - Tính số lớp xây được

Số gạch cần để xây mỗi lớp:
- Layer 1: 1
- Layer 2: 1 + 2 = số gạch cần để xây layer 1 + số layer
- Layer 3: 1 + 2 + 3 = số gạch cần để xây layer 2 + số layer
- Layer 4: 1 + 2 + 3 + 4 = số gạch cần để xây layer 3 + số layer
- ...

Biết: 1 <= n <= 10,000
=> n luôn >= 1 => luôn có đủ gạch để xây lớp đầu tiên

VD: n = 25
- Ban đầu, có n = 25 viên gạch.
- Xét Layer 1:
    + Số gạch cần:
        needed_bricks = 1
    + Kiểm tra số gạch còn lại có đủ để xây layer 1:
        (left_bricks = 25) > (needed_bricks = 1)
    => đủ: cập nhật số layer xây được:
        built_layers++;
        left_bricks -= needed_bricks;
- Xét layer 2:
    + Số gạch cần:
        needed_bricks = 1 + 2 = needed_bricks + layer
    + Kiểm tra số gạch còn lại có đủ để xây layer 1:
        (left_bricks = 24) > (needed_bricks = 3)
    => đủ: cập nhật số layer xây được:
        built_layers++;
        left_bricks -= needed_bricks; (left_bricks = 24 - 3 = 21)
- Xét tương tự cho các layer còn lại.

=> tổng quát hóa:
int left_bricks = n;
int built_layers = 0;
int layer = 1;
int needed_bricks = 1;

while (left_bricks >= needed_bricks)
    built_layers++;
    left_bricks -= needed_bricks;

    //cập nhật layer tiếp theo
    layer++; 
    //tính số gạch cần cho layer tiếp theo
    needed_bricks += layer; 









