# 🚀 HƯỚNG DẪN SỬ DỤNG — UML Activity Diagram Skill

> Dành cho Business Analyst | Phiên bản 1.0

---

## Tổng quan nhanh

Skill này giúp bạn tạo UML Activity Diagram chuẩn UML 2.x + mô tả nghiệp vụ
đầy đủ theo 3 bước rõ ràng, đảm bảo **output đúng ngay lần đầu**.

```
Bước 1 (INPUT)     →    Bước 2 (CONFIRM)    →    Bước 3 (OUTPUT)
──────────────          ─────────────────         ───────────────
Cung cấp thông tin      AI phân tích &            PlantUML code
(template hoặc          trả bảng phân tích        + Mô tả BA chuẩn
 tài liệu sẵn có)       BA reply "OK"
```

---

## 🟦 TRƯỜNG HỢP 1: Chưa có tài liệu nào

### Bước 1: Copy template, điền thông tin

Mở file `templates/INPUT_TEMPLATE.md`, điền vào các trường, paste vào Claude.

**Prompt mẫu:**
```
Tôi cần tạo UML Activity Diagram. Đây là thông tin quy trình:

[PROCESS_NAME]
Tên quy trình: Quy trình duyệt đơn nghỉ phép

[ACTORS]
Người dùng: Nhân viên, Quản lý trực tiếp
Hệ thống: HR System, Email Service

[HAPPY_PATH]
1. Nhân viên tạo đơn nghỉ phép
2. Hệ thống gửi thông báo cho quản lý
3. Quản lý xem xét và phê duyệt
4. Hệ thống cập nhật lịch và thông báo kết quả

[EXCEPTIONS]
- Quản lý từ chối: gửi lý do về nhân viên
- Quản lý vắng: auto escalate lên HR sau 24h

[BUSINESS_RULES]
BR-01: Đơn phải nộp trước 3 ngày làm việc
BR-02: Không được nghỉ quá 5 ngày liên tiếp không có lý do đặc biệt
```

### Bước 2: AI trả bảng phân tích → BA review

AI sẽ trả về bảng gồm: Actors, Flow steps, Gaps cần confirm, Assumptions.
Bạn chỉ cần reply:
- **"OK"** — nếu mọi thứ đúng → AI generate ngay
- **Sửa trực tiếp** vào bảng rồi gửi lại → AI cập nhật và generate
- **Trả lời gaps**: "GAP-01: Quản lý vắng thì escalate HR sau 24h"

### Bước 3: Nhận output

AI trả về:
1. PlantUML code (paste vào plantuml.com để xem diagram)
2. Mô tả nghiệp vụ đầy đủ theo chuẩn BA
3. Lưu ý & khuyến nghị

---

## 🟩 TRƯỜNG HỢP 2: Đã có tài liệu sẵn

### Bước 1: Upload / paste tài liệu

Bạn có thể cung cấp bất kỳ loại tài liệu nào:

| Loại tài liệu | Cách cung cấp |
|---|---|
| BRD / FRD / SRS | Paste nội dung hoặc upload file |
| Source code | Paste đoạn code liên quan |
| User Story / Jira | Paste nội dung ticket |
| Email mô tả nghiệp vụ | Paste nội dung email |
| Diagram cũ (text) | Paste mô tả hoặc code cũ |
| Transcript cuộc họp | Paste nội dung transcript |

**Prompt mẫu — có tài liệu:**
```
Đây là BRD quy trình thanh toán của chúng tôi.
Hãy đọc và tạo UML Activity Diagram chuẩn cho tôi.

[Paste nội dung BRD vào đây]
```

**Prompt mẫu — có source code:**
```
Đây là source code của service xử lý đơn hàng.
Hãy đọc code và tạo Activity Diagram mô tả luồng xử lý thực tế.

[Paste code vào đây]
```

### Bước 2: AI hỏi level (nếu có nhiều sub-process)

Nếu tài liệu lớn, AI sẽ hỏi:
- **A** — Tổng quan (1 diagram lớn)
- **B** — Chi tiết từng phần (nhiều diagram nhỏ)
- **C** — Cả hai
- **D** — Chỉ làm phần cụ thể

### Bước 3: Xác nhận bảng phân tích → Nhận output

Tương tự Trường hợp 1.

---

## 💡 TIPS để ra kết quả tốt nhất

### ✅ Nên làm

```
✅ Cung cấp tên quy trình cụ thể
✅ Liệt kê actors rõ ràng (người + hệ thống)
✅ Mô tả happy path theo thứ tự bước
✅ Ghi rõ các business rules quan trọng
✅ Nêu rõ exception nào cần xử lý
✅ Cho biết mức độ chi tiết mong muốn (overview / detail)
```

### ❌ Tránh làm

```
❌ Prompt quá ngắn: "Vẽ diagram đăng nhập"
   → Thiếu context, AI phải đoán nhiều, sẽ sai

❌ Trộn nhiều quy trình không liên quan vào 1 prompt
   → Tách ra, làm từng quy trình riêng

❌ Không review bảng phân tích Phase 2
   → Bỏ qua bước này dễ dẫn đến diagram sai về nghiệp vụ
```

### 📊 So sánh prompt tốt vs tệ

| | Prompt tệ | Prompt tốt |
|---|---|---|
| **Nội dung** | "Vẽ diagram đăng ký" | Điền đầy đủ template với actors, steps, exceptions |
| **Kết quả** | AI đoán mò, thiếu swimlane, thiếu exception | Diagram đúng ngay lần đầu |
| **Số lần sửa** | 3-5 lần | 0-1 lần |
| **Thời gian** | 30-60 phút | 10-15 phút |

---

## 📁 Cấu trúc file trong bộ skill

```
uml-activity-diagram/
│
├── SKILL.md                        ← Hướng dẫn chính cho AI (đừng sửa)
│
├── templates/
│   └── INPUT_TEMPLATE.md           ← Template BA điền vào (Trường hợp 1)
│
├── references/
│   ├── uml-notation-guide.md       ← Bảng ký hiệu UML 2.x đầy đủ
│   ├── diagram-patterns.md         ← 6 pattern sẵn có cho quy trình phổ biến
│   └── description-template.md    ← Template mô tả nghiệp vụ chuẩn BA
│
└── HUONG_DAN_SU_DUNG.md           ← File này
```

---

## 🔗 Công cụ render diagram

Sau khi có PlantUML code, dùng một trong các tool sau để xem diagram:

| Tool | Link | Đặc điểm |
|---|---|---|
| PlantUML Online | https://www.plantuml.com/plantuml/uml/ | Miễn phí, nhanh |
| Kroki.io | https://kroki.io | Hỗ trợ nhiều format |
| VS Code Extension | PlantUML extension | Xem trực tiếp trong IDE |
| IntelliJ Plugin | PlantUML Integration | Tích hợp IDE |
| draw.io | Import PlantUML | Export sang PNG/SVG/PDF |

---

## ❓ FAQ

**Q: AI có thể đọc file PDF / Word không?**
A: Upload file trực tiếp vào chat, AI có thể đọc và extract thông tin tự động.

**Q: Tôi có thể yêu cầu vẽ lại diagram với thay đổi nhỏ không?**
A: Có. Sau khi nhận output, gõ: "Sửa bước 3: thêm exception timeout 30 giây"

**Q: Diagram có thể export sang PNG/SVG không?**
A: PlantUML online cho phép export PNG, SVG, PDF trực tiếp.

**Q: Tôi muốn thêm màu sắc theo style công ty?**
A: Cung cấp mã màu HEX của công ty, AI sẽ áp dụng vào skinparam.

**Q: Có thể tạo nhiều diagram cho 1 tài liệu BRD lớn không?**
A: Có. Chọn option B hoặc C khi AI hỏi level, AI sẽ tạo từng diagram riêng.

---

*UML Activity Diagram Skill v1.0 — Được tối ưu cho Business Analyst*
