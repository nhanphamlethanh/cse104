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

