# Đồ án: Kỹ thuật vi hệ thống siêu cao tần (EE5429)

**Nhóm 01**

**Tên đề tài:** Khử ảnh hưởng bộ chuyển kết nối và định vị gián đoạn từ tham số S (De-embedding and Discontinuity Localization from S-parameters).

---
**[Project Plan - Dự án Kế hoạch](https://docs.google.com/spreadsheets/d/1WzEuhW8v6pte6aKQZzRB8YIo7CVdOmkQIDitc5sCpwo/edit?usp=sharing)*
---

## 1. Mục tiêu đề tài
Xây dựng một chương trình (phần mềm) có khả năng:
1. Đọc dữ liệu tham số S từ file Touchstone `.s2p`.
2. Khử ảnh hưởng của hai bộ chuyển kết nối hoặc test fixture (De-embedding).
3. Chuyển đổi giữa ma trận $S$ và ma trận truyền $T$.
4. Khôi phục tham số $S$ của thiết bị cần đo (DUT).
5. Chuyển $S_{11}(f)$ sang miền thời gian bằng IFFT.
6. Phát hiện và ước lượng vị trí các điểm gián đoạn trở kháng (Discontinuity Localization).
7. So sánh kết quả tự viết với thư viện hoặc phần mềm tham chiếu chuẩn.

## 2. Cơ sở lý thuyết cơ bản
* **Phương pháp de-embedding (khử fixture):**
  Hai cổng có thể thực hiện bằng công thức ma trận truyền:
  $[T_{do}] = [T_L][T_{DUT}][T_R]$
  $\Rightarrow [T_{DUT}] = [T_L]^{-1}[T_{do}][T_R]^{-1}$
* **Định vị gián đoạn (Time-Domain Reflectometry - TDR):**
  Thực hiện bằng cách biến đổi dữ liệu phản xạ từ miền tần số sang miền thời gian dựa trên biến đổi IFFT, từ đó tính toán khoảng cách dựa trên trễ thời gian và vận tốc lan truyền.

## 3. Công nghệ và Yêu cầu kỹ thuật
* **Ngôn ngữ lập trình:** Python.
* **Thư viện hỗ trợ:** 
  * `numpy`: Xử lý số phức, ma trận, FFT/IFFT.
  * `matplotlib`: Vẽ đồ thị trực quan hóa.
  * `csv`: Xuất/nhập kết quả.
  * `tkinter` hoặc `streamlit`: Xây dựng giao diện (nếu còn thời gian).
  * `scikit-rf`: **Chỉ dùng để đối chiếu kết quả**, không dùng làm thuật toán chính.
* **Yêu cầu tự xây dựng (Cốt lõi):** Nhóm phải tự viết bộ đọc file Touchstone, các hàm chuyển đổi (RI, MA, DB sang số phức), chuyển đổi $S \leftrightarrow T$, thuật toán de-embedding, nội suy lưới tần số, cửa sổ tín hiệu (Windowing), IFFT, chuyển trễ thời gian sang khoảng cách và tìm đỉnh.

## 4. Phân công nhiệm vụ

* **Thành viên 1: Lý thuyết và thuật toán de-embedding**
  * Tổng hợp lý thuyết tham số S.
  * Viết hàm chuyển đổi $S \leftrightarrow T$.
  * Viết thuật toán khử fixture trái và phải.
  * Xử lý nội suy và sai lệch lưới tần số.
  * Viết phần lý thuyết trong báo cáo.
* **Thành viên 2: Miền thời gian và định vị gián đoạn**
  * Chuẩn hóa dữ liệu tần số trước IFFT.
  * Viết các cửa sổ (Hann, Hamming, Kaiser, v.v.).
  * Biến đổi $S_{11}(f)$ sang miền thời gian.
  * Viết thuật toán tìm đỉnh phản xạ và quy đổi thời gian thành khoảng cách.
  * Đánh giá sai số định vị.
* **Thành viên 3: Dữ liệu, kiểm thử và tích hợp**
  * Viết bộ đọc và ghi file Touchstone.
  * Tạo dữ liệu mô phỏng kiểm thử.
  * Tích hợp các mô-đun thành chương trình hoàn chỉnh.
  * Vẽ đồ thị và xây dựng ví dụ chạy lại.
  * Đối chiếu kết quả với thư viện có sẵn (`scikit-rf`).
  * Tổng hợp báo cáo, slide và hướng dẫn sử dụng.
* **Công việc chung:** Kiểm tra công thức, review mã nguồn chéo, viết báo cáo tiến độ, chuẩn bị slide, chạy thử toàn bộ chương trình trước khi nộp.

## 5. Lộ trình thực hiện (Timeline)

| Giai đoạn | Tuần | Nhiệm vụ trọng tâm |
| :--- | :---: | :--- |
| **Khởi động** | 1 - 3 | Thành lập nhóm, khảo sát tài liệu (de-embedding, TDR, Touchstone), chốt đề tài và lập đặc tả (sơ đồ khối). |
| **Xây dựng nền tảng** | 4 - 5 | Viết bộ đọc file Touchstone, xây dựng các hàm chuyển đổi ma trận $S \leftrightarrow T$. |
| **Thuật toán cốt lõi** | 6 - 7 | Xây dựng thuật toán de-embedding, xử lý lưới tần số và độ ổn định ma trận. |
| **Miền thời gian** | 8 - 9 | Chuyển tham số S sang miền thời gian (áp dụng Windowing, IFFT), thuật toán định vị gián đoạn. |
| **Kiểm chứng & Mở rộng** | 10 - 12 | Tạo dữ liệu kiểm chứng, đối chiếu sai số với thư viện chuẩn (MathWorks/scikit-rf), mở rộng tính năng. |
| **Hoàn thiện** | 13 - 15 | Hoàn thiện chương trình (Release Candidate), viết báo cáo (cấu trúc 9 phần, ~25 trang), chuẩn bị kịch bản thuyết trình/demo và bảo vệ. |

## 6. Cấu trúc thư mục (Folder Structure)

```text
sparameter-project/
├── README.md                           # Tài liệu hướng dẫn dự án
├── requirements.txt                    # Các thư viện Python cần thiết (numpy, matplotlib, ...)
├── main.py                             # Script chính để chạy ứng dụng
├── src/                                # Thư mục chứa mã nguồn chính
│   ├── touchstone_io.py                # Xử lý đọc/ghi file Touchstone (.s2p)
│   ├── network_conversion.py           # Chuyển đổi ma trận S <-> T
│   ├── deembedding.py                  # Thuật toán de-embedding khử fixture
│   ├── interpolation.py                # Xử lý đồng bộ lưới tần số
│   ├── time_domain.py                  # Phân tích IFFT, Windowing (TDR)
│   ├── discontinuity.py                # Thuật toán tìm đỉnh và tính khoảng cách
│   ├── validation.py                   # Kiểm tra tính hợp lệ dữ liệu
│   └── plotting.py                     # Vẽ đồ thị tần số / thời gian
├── examples/                           # Dữ liệu mẫu & cấu hình
│   ├── measured.s2p                    
│   ├── fixture_left.s2p                
│   ├── fixture_right.s2p               
│   └── config.json                     
├── results/                            # Kết quả đầu ra
│   ├── dut_deembedded.s2p              
│   ├── comparison.csv                  
│   └── discontinuities.csv             
├── tests/                              # Unit tests (đảm bảo độ chính xác thuật toán)
│   ├── test_touchstone.py
│   ├── test_conversion.py
│   ├── test_deembedding.py
│   └── test_localization.py
└── reference/                          # Script dùng thư viện chuẩn để đối chiếu
    └── compare_with_library.py
```

## 7. Hướng dẫn sử dụng (Usage)

1. Cài đặt các thư viện yêu cầu:
   ```bash
   pip install -r requirements.txt
   ```
2. Cấu hình đường dẫn file đầu vào trong `examples/config.json`.
3. Chạy chương trình chính:
   ```bash
   python main.py
   ```
4. Kiểm tra kết quả trực quan trên giao diện (đồ thị) và file xuất ra tại thư mục `results/`.
