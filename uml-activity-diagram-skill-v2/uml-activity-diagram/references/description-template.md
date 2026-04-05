# Mô tả nghiệp vụ chuẩn BA — Định dạng bảng 4 cột

> **Chuẩn format**: Bảng 4 cột — STT | Bước thực hiện | Người/Hệ thống thực hiện | Mô tả
> Nhánh rẽ dùng bullet points với từ khoá **in đậm** (Duyệt / Từ chối / Hủy / ...)
> Tham chiếu số hình trong diagram dùng ký hiệu (hình x.x)

---

# [TÊN QUY TRÌNH]

## 1. Thông tin chung

| Thuộc tính | Giá trị |
|---|---|
| **Tên quy trình** | [Tên đầy đủ] |
| **Mã quy trình** | QT-[XXX] |
| **Phiên bản** | 1.0 |
| **Ngày tạo** | [YYYY-MM-DD] |
| **Ngày cập nhật** | [YYYY-MM-DD] |
| **Người tạo** | [Tên BA] |
| **Trạng thái** | ☐ Draft  ☐ In Review  ☐ Approved |
| **Hệ thống liên quan** | [Tên các hệ thống] |

---

## 2. Mô tả quy trình

### 2.1. Mục tiêu

[Mô tả ngắn gọn 2-3 câu: Quy trình này làm gì, tại sao cần, ai được lợi]

### 2.2. Mô tả chi tiết

| STT | Bước thực hiện | Người/Hệ thống thực hiện | Mô tả |
|:---:|---|---|---|
| 1 | [Tên bước 1] | [Vai trò], [System A], [System B] | [Người/System] thực hiện [Action 1.1] (hình 1.1) và [Action 1.2] (hình 1.2). Sau khi [action], [System] thực hiện [Action 1.3] (hình 1.3) để [mục đích]. |
| 2 | [Tên bước 2 — gợi ý / đồng bộ] | [System ngoài] | [System] thực hiện [Action] (hình 2) dựa trên [điều kiện/dữ liệu]. Sau khi [hoàn thành], [System] đồng bộ [kết quả] về [System nhận]. |
| 3 | [Tên bước 3 — có rẽ nhánh] | [Vai trò], [System] | [Vai trò] thực hiện [Action chính] (hình 3.1) dựa trên [điều kiện].<br><br>• Nếu chọn **[Nhánh A — ví dụ: Duyệt]**: [Vai trò] thực hiện [Action A] (hình 3.2). [Bên liên quan] sẽ Nhận kết quả [Action A] (hình 3.5).<br><br>• Nếu chọn **[Nhánh B — ví dụ: Từ chối]**: [Vai trò] thực hiện [Action B] (hình 3.3). [Bên liên quan] sẽ Nhận kết quả [Action B] (hình 3.6).<br><br>• Nếu chọn **[Nhánh C — ví dụ: Hủy]**: [Vai trò] thực hiện [Action C] (hình 3.4) và kết thúc tiến trình [tên hồ sơ/đối tượng]. |
| 4 | [Tên bước 4 — tiếp theo] | [Vai trò], [System] | [Mô tả bước tiếp theo. Nếu bước này là kết quả từ bước 3, ghi rõ điều kiện kích hoạt.] |
| 5 | [Tên bước 5 — có rẽ nhánh thứ 2] | [Vai trò], [System] | [Vai trò] thực hiện [Action] (hình 5.1).<br><br>• Nếu chọn **[Nhánh A]**: [Mô tả] (hình 5.2). [Kết quả cho bên liên quan] (hình 5.x).<br><br>• Nếu chọn **[Nhánh B]**: [Mô tả] (hình 5.3).<br><br>• Nếu chọn **[Nhánh C]**: [Mô tả] (hình 5.4) và [kết thúc / tiếp tục]. |

---

## 3. Business Rules

| Mã | Quy tắc nghiệp vụ | Áp dụng tại bước | Hệ quả nếu vi phạm |
|---|---|---|---|
| BR-01 | [Mô tả quy tắc cụ thể] | Bước [X] | [Xử lý thế nào] |
| BR-02 | [Mô tả quy tắc] | Bước [X] | [Xử lý thế nào] |

---

## 4. Pre-conditions & Post-conditions

**Pre-conditions (Điều kiện tiên quyết):**
- [ ] [Điều kiện 1 phải đúng trước khi bắt đầu quy trình]
- [ ] [Điều kiện 2]

**Post-conditions (Hậu điều kiện):**
- [ ] [Trạng thái hệ thống sau khi quy trình hoàn thành thành công]
- [ ] [Thông báo/artifact đã được tạo ra]

---

## Ví dụ tham chiếu — Quy trình bảo lãnh viện phí BVCare

*(Đây là ví dụ điền sẵn để AI hiểu đúng format mong muốn)*

### 1.1.2. Mô tả quy trình

| STT | Bước thực hiện | Người/Hệ thống thực hiện | Mô tả |
|:---:|---|---|---|
| 1 | Tạo mới và Gửi Đề nghị bảo lãnh | Cán bộ bệnh viện, App Bệnh viện, BVCare Gateway | Cán bộ bệnh viện (tại App Bệnh viện) thực hiện Tạo Đề nghị bảo lãnh (hình 1.1) và Gửi Đề nghị bảo lãnh (hình 1.2). Sau khi gửi, hệ thống BVCare Gateway thực hiện Gửi Đề nghị bảo lãnh (hình 1.3) để chuyển dữ liệu sang hệ thống BVCare xử lý Ghi dữ liệu Đề nghị bảo lãnh (hình 1.4). |
| 2 | Gợi ý thông tin duyệt Đề nghị bảo lãnh | DMN | Hệ thống DMN thực hiện Gợi ý thông tin duyệt Đề nghị bảo lãnh (hình 2) dựa trên dữ liệu đã ghi nhận. Sau khi gợi ý xong, DMN đồng bộ thông tin gợi ý về BVCare. |
| 3 | Trả lời Đề nghị bảo lãnh | Cán bộ Bảo lãnh, BVCare | Cán bộ bảo lãnh (tại BVCare) thực hiện Trả lời Đề nghị bảo lãnh (hình 3.1) dựa trên thông tin duyệt đã gợi ý.<br><br>• Nếu chọn **Duyệt**: Cán bộ bảo lãnh thực hiện Duyệt Đề nghị bảo lãnh (hình 3.2). Cán bộ bệnh viện sẽ Nhận kết quả Duyệt Đề nghị bảo lãnh (hình 3.5).<br><br>• Nếu chọn **Từ chối**: Cán bộ bảo lãnh thực hiện Từ chối Đề nghị bảo lãnh (hình 3.3). Cán bộ bệnh viện sẽ Nhận kết quả Từ chối Đề nghị bảo lãnh (hình 3.6).<br><br>• Nếu chọn **Hủy**: Cán bộ bảo lãnh thực hiện Hủy hồ sơ (hình 3.4) và kết thúc tiến trình hồ sơ đó. |
| 4 | Yêu cầu bổ thường | Cán bộ bệnh viện, App Bệnh viện, BVCare Gateway | Cán bộ bệnh viện (tại App Bệnh viện) thực hiện Tạo Yêu cầu bổ thường (hình 5.1), Điền Yêu cầu bổ thường (hình 5.2) và Gửi Yêu cầu bổ thường (hình 5.3). Sau khi gửi, BVCare Gateway thực hiện Gửi Yêu cầu bổ thường (hình 5.3) để chuyển dữ liệu sang BVCare Ghi dữ liệu Yêu cầu bổ thường (hình 5.4). |
| 5 | Trả lời Yêu cầu bổ thường | Cán bộ Bảo lãnh, BVCare | Cán bộ bảo lãnh (tại BVCare) thực hiện Trả lời Yêu cầu bổ thường (hình 7.1) dựa trên thông tin đã gợi ý.<br><br>• Nếu chọn **Duyệt**: Cán bộ bảo lãnh thực hiện Duyệt Yêu cầu bổ thường (hình 7.2). Bản lãnh tại VCBT sẽ được thông báo.<br><br>• Nếu chọn **Từ chối**: Cán bộ bảo lãnh thực hiện Từ chối Yêu cầu bổ thường (hình 7.3).<br><br>• Nếu chọn **Hủy duyệt**: Cán bộ bảo lãnh thực hiện Hủy duyệt Yêu cầu bổ thường (hình 7.6). |
