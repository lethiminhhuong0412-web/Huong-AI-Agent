# 📋 INPUT TEMPLATE — UML Activity Diagram
> **Hướng dẫn**: Copy toàn bộ file này, điền vào các chỗ trống, paste lại cho AI.
> Không cần điền 100% — phần nào chưa rõ cứ để trống, AI sẽ xử lý ở bước tiếp theo.

---

## [PROCESS_NAME]
Tên quy trình: _______________________________________________
Mã quy trình (nếu có): QT-___________
Phiên bản: 1.0
Ngày tạo: ____________________________________________________
Tên BA phụ trách: ____________________________________________
Phòng ban / Team: ____________________________________________

---

## [SCOPE] — Phạm vi quy trình
Bắt đầu khi (trigger):
> _______________________________________________________________

Kết thúc khi (end condition):
> _______________________________________________________________

Không áp dụng cho (exclusions):
> _______________________________________________________________

---

## [ACTORS] — Tác nhân tham gia

### Người dùng / Vai trò con người
| Tên vai trò | Mô tả ngắn |
|---|---|
| | |
| | |

### Hệ thống nội bộ
| Tên hệ thống / Service | Chức năng chính |
|---|---|
| | |
| | |

### Bên ngoài (External systems, 3rd party)
| Tên | Loại tích hợp |
|---|---|
| | |

---

## [HAPPY_PATH] — Luồng chính (khi mọi thứ OK)
> Mô tả các bước theo thứ tự. Ghi rõ AI/Hệ thống hay Con người thực hiện.

1. [Actor]: ___________________________________________________
2. [Actor]: ___________________________________________________
3. [Actor]: ___________________________________________________
4. [Actor]: ___________________________________________________
5. [Actor]: ___________________________________________________
6. [Actor]: ___________________________________________________
(thêm dòng nếu cần)

---

## [ALTERNATE_FLOWS] — Luồng thay thế
> Điều gì xảy ra khi có điều kiện rẽ nhánh (không phải lỗi, chỉ là lựa chọn khác)?

- Nếu [điều kiện A]: → ________________________________________
- Nếu [điều kiện B]: → ________________________________________
- Nếu [điều kiện C]: → ________________________________________

---

## [EXCEPTION_FLOWS] — Luồng ngoại lệ / Lỗi
> Điều gì xảy ra khi có sự cố, timeout, lỗi hệ thống?

- Khi [sự cố 1]: → ____________________________________________
  Xử lý: _____________________________________________________
- Khi [sự cố 2]: → ____________________________________________
  Xử lý: _____________________________________________________
- Khi [sự cố 3]: → ____________________________________________
  Xử lý: _____________________________________________________

---

## [BUSINESS_RULES] — Quy tắc nghiệp vụ
> Các ràng buộc, điều kiện đặc biệt, giới hạn cần tuân theo.

- BR-01: _____________________________________________________
- BR-02: _____________________________________________________
- BR-03: _____________________________________________________

---

## [SLA_TIMING] — Thời gian & SLA
> Giới hạn thời gian, timeout, SLA cho từng bước hoặc toàn quy trình.

- Tổng thời gian xử lý tối đa: ________________________________
- Timeout cho bước [tên bước]: ________________________________
- SLA phản hồi cho người dùng: ________________________________

---

## [DATA_OBJECTS] — Dữ liệu / Artifact truyền qua quy trình
> Các form, document, dữ liệu quan trọng được tạo ra hoặc sử dụng.

- Đầu vào (Input): ___________________________________________
- Đầu ra (Output): ___________________________________________
- Lưu trữ (Storage): _________________________________________

---

## [OUTPUT_LEVEL] — Mức độ chi tiết mong muốn
> Đánh dấu [x] vào ô phù hợp.

- [ ] **Tổng quan** — Main flow, không drill-down sub-process
- [ ] **Chi tiết** — Có exception, alternate flow đầy đủ
- [ ] **Cả hai** — Tổng quan + drill-down từng sub-process

---

## [NOTES] — Ghi chú thêm
> Bất kỳ thông tin nào bạn muốn AI biết thêm.

_______________________________________________________________
_______________________________________________________________

---

> ✅ **Sau khi điền xong**, paste toàn bộ nội dung này vào chat và gõ thêm:
> *"Hãy phân tích và tạo UML Activity Diagram cho tôi."*
