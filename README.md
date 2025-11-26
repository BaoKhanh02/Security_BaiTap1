# BÀI TẬP MÔN: An toàn và bảo mật thông tin #

## Sinh viên: Vũ Bảo Khánh. MSSV: K225480106028 ##

## BÀI TẬP 1: ##

### TÌM HIỂU CÁC PHƯƠNG PHÁP MÃ HOÁ CỔ ĐIỂN ###
1. Caesar
2. Affine
3. Hoán vị
4. Vigenère
5. Playfair

**Với mỗi phương pháp, hãy tìm hiểu:**
1. Tên gọi
2. Thuật toán mã hoá, thuật toán giải mã
3. Không gian khóa
4. Cách phá mã (mà không cần khoá)
5. Cài đặt thuật toán mã hoá và giải mã bằng code C++ và bằng html+css+javascript

### Bài làm ###

### 1. Ceasar ###

**Tên gọi**

Caesar cipher (mã Cesar) — dịch vòng dịch chuyển từng ký tự.

**Thuật toán**

Khoá: shift k (0..25).
Mã hoá: C = (P + k) mod 26.
Giải mã: P = (C - k mod 26 + 26) mod 26.

**Không gian khoá**

26 Khả năng (k = 0..25).

**Cách phá (không cần khoá)**

Brute-force thử 26 giá trị — đọc bằng mắt để chọn bản rõ hợp lý.
Phân tích tần suất: so sánh tần suất chữ cái của bản mã với phân bố tiếng Anh/Vietnam (ví dụ E, A, T, O...).
Rõ ràng rất yếu.

**Thuật toán bằng C++**

<img width="243" height="160" alt="image" src="https://github.com/user-attachments/assets/90712c54-a1c6-49be-93c4-5fa7440a5b6a" />

**Thuật toán bằng html+css+javascript**

<img width="366" height="500" alt="image" src="https://github.com/user-attachments/assets/df60b9f8-eb2c-4e46-bd5d-304ba51be6de" />

<img width="348" height="512" alt="image" src="https://github.com/user-attachments/assets/c9925850-355c-419a-89d2-14398e2c6745" />

### 2. Affine ###

**Tên gọi**

Affine cipher — mã affine (mã affine tuyến tính) — là một dạng đơn ký tự (monoalphabetic) dựa trên ánh xạ tuyến tính modulo 26.

**Thuật toán mã hoá và giải mã**

Quy ước: với ký tự chữ cái A..Z tương ứng số 0..25.

**Khoá**

Hai số nguyên (a, b) với điều kiện gcd(a, 26) = 1 (tức a và 26 phải nguyên tố cùng nhau) để a có nghịch đảo modulo 26.

b ∈ {0..25}.

**Mã hoá**

Với ký tự P (số 0..25):
C = (a * P + b) mod 26

**Giải mã**

Tính nghịch đảo modulo của a, gọi là a_inv sao cho a * a_inv ≡ 1 (mod 26).

Với ký tự C:
P = a_inv * (C - b) mod 26

(Lưu ý: thao tác mod nên đảm bảo kết quả không âm.)

**Không gian khoá**

Các giá trị a hợp lệ là các số 0..25 mà gcd(a,26)=1. Những số này:
1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25 → tổng 12 giá trị.

b có 26 giá trị.

Tổng khóa = 12 * 26 = 312 khả năng.

**Cách phá mã (không cần khoá)**

Brute-force: thử tất cả 312 cặp (a,b) — rất nhanh. In ra 312 bản rõ khả dĩ, nhìn chọn kết quả có nghĩa.

Phân tích tần suất: vì là monoalphabetic transform (mỗi chữ được ánh xạ tuyến tính), tần suất chữ cái trong bản mã là permutation của tần suất trong bản rõ, nên có thể map chữ có tần suất cao sang E/A/T... để tìm a,b.

Known-plaintext: nếu biết một hoặc hai cặp (P, C) có thể giải hệ để tìm a,b.

Kết luận: Affine yếu, brute-force đơn giản.

**Thuật toán bằng C++**

<img width="564" height="302" alt="image" src="https://github.com/user-attachments/assets/a23767c4-30d0-43cc-a51d-1c4cf3d8e1e0" />

**Thuật toán bằng html+css+javascript**

<img width="1154" height="525" alt="image" src="https://github.com/user-attachments/assets/3fa279f1-34a9-4c35-abb7-183f976e231d" />

<img width="1146" height="521" alt="image" src="https://github.com/user-attachments/assets/c5510d69-2a35-4f41-8388-b37a934aca6d" />

<img width="1150" height="658" alt="image" src="https://github.com/user-attachments/assets/b008460c-57af-43c0-aa25-018e3abaf010" />

### 3. Hoán vị ###

**Tên gọi**

Permutation cipher (mã hoán vị) — chung chung cho mọi phép hoán vị ký tự.

Trong mật mã cổ điển thường gặp Columnar Transposition (hoán vị theo cột) — thường gọi ngắn là Transposition cipher.

**Thuật toán mã hoá và giải mã**
Ý tưởng chung

Không thay thế ký tự — chỉ thay đổi vị trí các ký tự bằng một hoán vị. Với Columnar Transposition ta viết bản rõ theo hàng vào một ma trận có n cột (n = chiều key), rồi đọc ra theo thứ tự cột được chỉ định bởi hoán vị (hoặc thứ tự chữ cái của keyword).

**Các cách biểu diễn khoá**

Permutation numeric: một hoán vị trực tiếp, ví dụ order = [2,0,3,1] (đọc cột 2 trước, rồi 0, rồi 3, rồi 1).

Keyword (từ khoá): dùng 1 từ (ví dụ ZEBRA) — ta sắp chữ cái theo thứ tự chữ cái để suy thứ tự cột. Ví dụ Z E B R A → khi sắp theo alphabet A B E R Z tương ứng cột thứ: 4,2,1,3,0 → dùng thứ tự đó để đọc.

**Mã hoá (Columnar transposition, kiểu thường dùng)**

Chuẩn hoá plaintext: thường chuyển thành chữ hoa A–Z và loại bỏ ký tự lạ (hoặc giữ nguyên nếu muốn). Ở ví dụ code bên dưới mình chuẩn hoá A–Z, bỏ ký tự khác để dễ xử lý.

Chọn n (số cột) — hoặc keyword.

Viết plaintext theo hàng vào ma trận có n cột; nếu thiếu ô thì padding bằng ký tự filler (thường 'X').

Đọc các cột theo thứ tự hoán vị → nối thành ciphertext.

Ví dụ:

Plain: WEAREDISCOVERED (15 chữ) với n=4, rows=4 (4x4=16) pad 'X'

W E A R
E D I S
C O V E
R E D X


Nếu order = [1,3,0,2] → đọc cột 1,3,0,2 → kết quả.

**Giải mã**

Biết n và order: tính số hàng rows = ceil(len(ct)/n).

Tạo ma trận rows×n.

Điền từng cột theo order bằng các ký tự ciphertext theo thứ tự (lưu ý: nếu padding không đều thì phải xử lý special case — code dưới đây giả định padding đầy đủ vì ta dùng rows*n = pad length).

Đọc ma trận theo hàng để thu plaintext, loại bỏ padding cuối cùng nếu cần.

(Nếu ciphertext không chia hết cho n, ta phải tính cột ngắn hơn — có thể thêm logic nhưng code mình đưa sẽ dùng padding để đảm bảo đầy đủ.)

**Không gian khoá**

Nếu dùng hoán vị trực tiếp với n cột: số khoá = n! (giai thừa). Rất lớn khi n tăng.

Nếu dùng keyword độ dài n, thực chất là 1 hoán vị của n phần tử → vẫn n! về mặt thông lượng.

Với n nhỏ (5..8) có thể brute-force; với n lớn, tìm bằng heuristic.

**Cách phá mã (không cần khoá)**

Brute-force small n: thử tất cả hoán vị nếu n! nhỏ (ví dụ n ≤ 8).

Thử các độ dài cột n hợp lý: thường thử n trong range 2..max (ví dụ 2..12) — với mỗi n thử hoán vị (hoặc heuristic).

Fitness scoring / language model: với mỗi candidate giải mã, đánh giá bằng score dựa trên unigram/bigram/ngram để chọn bản rõ có nghĩa cao nhất.

Index of Coincidence (IC): khác substitution; dùng IC để ước tính có phải là transposition — IC không thay đổi (vì không đổi tần suất chữ) nên transposition giữ IC giống như plaintext. Vì thế IC ít giúp chọn n, nhưng bigram/trigram scoring hữu ích (bởi vì transposition phá cấu trúc bigram).

Hoán vị cột bằng hill-climbing / simulated annealing / genetic: thường dùng để tối ưu sắp xếp cột theo fitness (log-probability theo n-gram).

Known-plaintext / crib: nếu biết một phần plaintext (từ, cụm từ), có thể dùng để đặt hàng cột và suy hoán vị.

Chiến lược phân tích: cố tách các cột bằng quan sát các cặp ký tự/n-gram xuất hiện — ví dụ truy tìm các bigram phổ biến 'TH', 'HE' có thể cho manh mối về cột gần nhau.

Tóm lại: transposition khá mạnh chống brute-force đơn giản nếu n lớn, nhưng với heuristic + scoring có thể phá.

**Thuật toán bằng C++**

<img width="450" height="378" alt="image" src="https://github.com/user-attachments/assets/69efc50f-d42e-4773-ad0e-d526009a1673" />

**Thuật toán bằng html+css+javascript**

<img width="1168" height="630" alt="image" src="https://github.com/user-attachments/assets/b33854d9-d4ee-4441-b0ee-42b95ffbd840" />

<img width="1153" height="604" alt="image" src="https://github.com/user-attachments/assets/cc4f2191-9478-42db-99e0-db1b2afa287a" />

### 4. Vigenère ###

**Tên gọi**

Vigenère Cipher (Mật mã Vigenère)

Đặt theo tên Blaise de Vigenère (thế kỷ 16).

**Thuật toán mã hoá**

Giả sử:

<img width="398" height="77" alt="image" src="https://github.com/user-attachments/assets/180bbe2f-a76e-4cba-8eb7-5784fb1f689e" />

Mã hoá:

<img width="987" height="52" alt="image" src="https://github.com/user-attachments/assets/7cfd7c20-0608-4c38-9dd4-46dc2eedc996" />

Giải mã:

<img width="974" height="52" alt="image" src="https://github.com/user-attachments/assets/c028f57e-0d3c-41f5-b79c-41992aeb9c57" />
Không gian khóa

+ Nếu độ dài khóa là 𝑚, thì số khóa có thể:<img width="49" height="24" alt="image" src="https://github.com/user-attachments/assets/7e6b8844-4689-4d83-8a4a-0ca0b30170cc" />

+ Lớn hơn nhiều so với Caesar và Affine.

**Cách phá mã (không có khoá)**

+ Kasiski examination: Tìm khoảng cách lặp của chuỗi để đoán độ dài khóa.

+ Friedman test (Index of Coincidence): Ước lượng độ dài khóa.

+ Sau đó dùng phân tích tần suất với từng cột (giống Caesar).

**Thuật toán bằng C++**

<img width="249" height="159" alt="image" src="https://github.com/user-attachments/assets/372a9e50-16bd-4c7c-a60b-b6d65fbd69d6" />

**Thuật toán bằng html+css+javascript**

<img width="284" height="286" alt="image" src="https://github.com/user-attachments/assets/e7188fbe-aff5-484e-999e-e073375ab71a" />

<img width="260" height="269" alt="image" src="https://github.com/user-attachments/assets/f8a8dc6f-c9ba-498f-b975-da1578f5ee9f" />

### 5. Playfair ###

**Tên gọi**

Playfair cipher — Mã Playfair, là một bộ mã cổ điển thay thế cặp ký tự (digraph) theo một bảng 5×5; thường gộp I và J.

**Thuật toán mã hoá và giải mã**

**Xây bảng 5×5 từ khóa:**

+ Chuẩn hoá khóa: viết hoa, loại bỏ ký tự không phải chữ, thay J thành I, loại bỏ ký tự trùng lặp theo thứ tự xuất hiện.

+ Ghi tiếp các chữ cái còn lại từ A đến Z (bỏ J) để điền đủ 25 ô.

**Tiền xử lý bản rõ:**

+ Chuyển sang chữ in hoa, thay J -> I, loại bỏ ký tự không phải chữ (tùy chọn).

+ Tách thành các digraph (cặp): nếu hai ký tự liên tiếp giống nhau thì chèn X sau ký tự đầu; nếu còn ký tự lẻ cuối cùng thì thêm X.

**Mã hoá mỗi cặp (A, B):**

+ Tìm vị trí A = (r1,c1), B = (r2,c2).

+ Nếu cùng hàng: thay mỗi chữ bằng chữ bên phải (vòng).

+ Nếu cùng cột: thay bằng chữ bên dưới (vòng).

+ Nếu tạo thành chữ nhật: thay A bằng chữ ở (r1, c2), B bằng chữ ở (r2, c1).

**Giải mã:** làm ngược lại (bên trái/bên trên/và cùng quy tắc chữ nhật).

Lưu ý: do có chèn X, kết quả giải mã thường cần hậu xử lý (loại bỏ X chèn thêm) theo quy tắc heuristics.

**Không gian khóa**

Lý thuyết: mọi hoán vị của 25 ký tự → 25! rất lớn. Thực tế người dùng thường nhập keyphrase nên không gian khả dĩ nhỏ hơn, nhưng vẫn rộng.

**Cách phá mã (không cần khoá)**

+ Phân tích tần suất digraph (bigram) để so sánh với bảng tần suất ngôn ngữ.

+ Thuật toán tối ưu hoán vị (hill-climbing, simulated annealing, genetic) dùng hàm fitness dựa trên log-probability n-gram (bigram/trigram) để tìm bảng 5×5 tốt nhất.

+ Nếu có known-plaintext (crib), có thể gán một số chữ vào bảng và rút gọn không gian.

**Thuật toán bằng C++**

<img width="381" height="410" alt="image" src="https://github.com/user-attachments/assets/3b0cfa27-3b94-4947-8534-bf532ae6bee5" />

**Thuật toán bằng html+css+javascript**

<img width="1145" height="746" alt="image" src="https://github.com/user-attachments/assets/cd891f89-2525-4bcd-af8f-9f729ace9e8e" />

<img width="1134" height="723" alt="image" src="https://github.com/user-attachments/assets/18d550f9-c5d2-4e17-811d-8e4b69f247de" />
