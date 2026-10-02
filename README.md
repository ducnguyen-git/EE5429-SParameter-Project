# Đồ án: Kỹ thuật vi hệ thống siêu cao tần (EE5429)
**Nhóm 01**

Dự án này là mã nguồn phục vụ đồ án môn học **Kỹ thuật vi hệ thống siêu cao tần (EE5429)**. Mục tiêu của dự án là xây dựng một công cụ bằng Python (S-Parameter Project) nhằm phân tích, xử lý, và tính toán dữ liệu tham số S (S-parameters).

## Các tính năng chính (Main Features)

- **Đọc và ghi file Touchstone:** Xử lý dữ liệu S-parameter định dạng `.s2p` (và các chuẩn Touchstone khác).
- **Chuyển đổi tham số mạng (Network Conversion):** Chuyển đổi qua lại giữa các tham số mạng (S, Z, Y, ABCD).
- **Khử nhiễu hệ thống đo (De-embedding):** Loại bỏ ảnh hưởng của fixture (bên trái và bên phải) ra khỏi kết quả đo của thiết bị cần kiểm tra (DUT).
- **Nội suy (Interpolation):** Xử lý và nội suy dữ liệu miền tần số.
- **Phân tích miền thời gian (Time Domain):** Chuyển đổi dữ liệu từ miền tần số sang miền thời gian (sử dụng IFFT).
- **Xác định điểm gián đoạn (Discontinuity Localization):** Xác định và định vị các điểm gián đoạn trên đường truyền tín hiệu siêu cao tần.
- **Vẽ đồ thị (Plotting):** Trực quan hóa dữ liệu mô phỏng và đo đạc.

## Cấu trúc thư mục (Folder Structure)

Dự án được tổ chức theo kiến trúc như sau:

```text
sparameter-project/
├── README.md                           # Tài liệu hướng dẫn dự án
├── requirements.txt                    # Các thư viện Python cần thiết
├── main.py                             # Script chính để chạy ứng dụng
├── src/                                # Thư mục chứa mã nguồn chính
│   ├── touchstone_io.py                # Xử lý đọc/ghi file Touchstone (.s2p, .sNp)
│   ├── network_conversion.py           # Chuyển đổi S, Z, Y, ABCD parameters
│   ├── deembedding.py                  # Thuật toán de-embedding khử fixture
│   ├── interpolation.py                # Các hàm nội suy tần số
│   ├── time_domain.py                  # Phân tích miền thời gian (TDR/TDT)
│   ├── discontinuity.py                # Xác định các điểm gián đoạn
│   ├── validation.py                   # Kiểm tra tính hợp lệ của dữ liệu (Passivity, Causality)
│   └── plotting.py                     # Vẽ đồ thị kết quả
├── examples/                           # Thư mục chứa dữ liệu mẫu và file cấu hình
│   ├── measured.s2p                    # File S-parameter đo lường tổng thể
│   ├── fixture_left.s2p                # File S-parameter của fixture trái
│   ├── fixture_right.s2p               # File S-parameter của fixture phải
│   └── config.json                     # Cấu hình các tham số đầu vào cho hệ thống
├── results/                            # Thư mục lưu kết quả xuất ra
│   ├── dut_deembedded.s2p              # File S-parameter của riêng DUT sau khi de-embed
│   ├── comparison.csv                  # Bảng so sánh kết quả
│   └── discontinuities.csv             # Danh sách vị trí các điểm gián đoạn
├── tests/                              # Unit tests đảm bảo độ chính xác
│   ├── test_touchstone.py
│   ├── test_conversion.py
│   ├── test_deembedding.py
│   └── test_localization.py
└── reference/                          # So sánh kết quả thuật toán với các thư viện/công cụ chuẩn
    └── compare_with_library.py
```

## Hướng dẫn sử dụng (Usage)

1. Cài đặt các thư viện yêu cầu:
   ```bash
   pip install -r requirements.txt
   ```
2. Chạy chương trình chính (chỉnh sửa `config.json` nếu cần):
   ```bash
   python main.py
   ```
3. Xem kết quả dữ liệu xuất ra tại thư mục `results/`.

## Phân công nhóm (T7-2 Plan)
*(Chi tiết công việc tham khảo sơ đồ phân công T7-2 trên Miro board của nhóm)*
