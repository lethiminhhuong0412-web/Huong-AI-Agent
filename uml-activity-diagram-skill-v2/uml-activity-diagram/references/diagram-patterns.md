# Diagram Patterns — Các mẫu quy trình phổ biến

> Đây là bộ pattern sẵn có. Khi gặp quy trình tương tự, lấy pattern này làm
> skeleton và điều chỉnh theo thực tế. Tiết kiệm ~60% thời gian so với viết từ đầu.

---

## PATTERN 01 — Approval Workflow (Duyệt đa cấp)

**Dùng khi**: Quy trình phê duyệt hợp đồng, đơn nghỉ phép, chi phí, yêu cầu mua sắm

```plantuml
@startuml Approval_Workflow

skinparam defaultFontName Arial
skinparam ActivityBorderColor #2C3E50
skinparam ActivityDiamondBackgroundColor #FFF9C4
skinparam PartitionBorderColor #AEB6BF

title <b>Quy Trình Phê Duyệt [Tên đối tượng]</b>

|#E8F4FD| Người nộp |
start
:Tạo [tên đối tượng] mới;
:Điền thông tin và đính kèm tài liệu;
:Nộp yêu cầu phê duyệt;

|#FFF3E0| Hệ thống |
:Validate dữ liệu đầu vào;
if (Dữ liệu hợp lệ?) then ([Hợp lệ])
  :Gán cho cấp phê duyệt 1;
  :Gửi thông báo email cho người phê duyệt;
else ([Thiếu / Sai thông tin])
  #FFE4E4:Trả về lỗi cho người nộp;
  |#E8F4FD| Người nộp |
  :Xem thông báo lỗi và chỉnh sửa;
  stop
endif

|#F0FFF0| Cấp phê duyệt 1 (Trực tiếp) |
:Xem xét yêu cầu;
if (Quyết định cấp 1?) then ([Phê duyệt])
  :Xác nhận và chuyển cấp 2;
elseif ([Từ chối])
  :Nhập lý do từ chối;
  |#FFF3E0| Hệ thống |
  :Cập nhật trạng thái REJECTED;
  :Gửi thông báo kết quả cho người nộp;
  |#E8F4FD| Người nộp |
  :Nhận thông báo từ chối;
  stop
else ([Yêu cầu bổ sung])
  :Ghi chú thông tin cần bổ sung;
  |#E8F4FD| Người nộp |
  :Nhận yêu cầu bổ sung;
  :Bổ sung tài liệu / thông tin;
  :Nộp lại;
  |#F0FFF0| Cấp phê duyệt 1 (Trực tiếp) |
  :Xem xét lại;
endif

|#F5F0FF| Cấp phê duyệt 2 (Ban Giám đốc) |
:Xem xét và ra quyết định cuối;
if (Phê duyệt cuối?) then ([Phê duyệt])
  :Ký duyệt;
else ([Từ chối])
  :Ghi lý do từ chối;
  |#FFF3E0| Hệ thống |
  #FFE4E4:Cập nhật trạng thái FINAL_REJECTED;
  :Gửi thông báo;
  stop
endif

|#FFF3E0| Hệ thống |
#E8F8E8:Cập nhật trạng thái APPROVED;
:Thực thi hành động tiếp theo (tạo PO, ghi sổ sách...);
:Gửi email xác nhận cho tất cả bên liên quan;
:Lưu hồ sơ vào kho lưu trữ;
stop

@enduml
```

---

## PATTERN 02 — User Registration / Onboarding

**Dùng khi**: Đăng ký tài khoản, onboarding khách hàng mới, KYC

```plantuml
@startuml User_Registration

title <b>Quy Trình Đăng Ký Tài Khoản</b>

|#E8F4FD| Người dùng |
start
:Truy cập trang đăng ký;
:Điền thông tin cá nhân (Họ tên, Email, SĐT, Mật khẩu);

|#FFF3E0| Hệ thống |
:Kiểm tra định dạng dữ liệu;
if (Dữ liệu hợp lệ?) then ([Hợp lệ])
  :Kiểm tra email/SĐT đã tồn tại chưa;
  if (Đã tồn tại?) then ([Đã có tài khoản])
    #FFE4E4:Thông báo tài khoản đã tồn tại;
    :Gợi ý đăng nhập hoặc quên mật khẩu;
    stop
  else ([Chưa có])
    :Tạo tài khoản với trạng thái PENDING;
    :Gửi email xác thực (OTP/Link);
  endif
else ([Không hợp lệ])
  #FFE4E4:Hiển thị lỗi validate cho từng field;
  |#E8F4FD| Người dùng |
  :Xem lỗi và sửa thông tin;
  stop
endif

|#E8F4FD| Người dùng |
:Nhận email xác thực;
if (Xác thực trong 24h?) then ([Đúng hạn])
  :Nhấn link / nhập OTP xác thực;
else ([Quá hạn])
  :Yêu cầu gửi lại email xác thực;
  |#FFF3E0| Hệ thống |
  :Gửi lại email mới;
  |#E8F4FD| Người dùng |
  :Xác thực bằng email mới;
endif

|#FFF3E0| Hệ thống |
:Cập nhật trạng thái tài khoản → ACTIVE;
:Tạo hồ sơ người dùng mặc định;
:Gửi email chào mừng;

|#E8F4FD| Người dùng |
#E8F8E8:Đăng nhập vào hệ thống thành công;
stop

@enduml
```

---

## PATTERN 03 — API Call với Retry & Timeout

**Dùng khi**: Tích hợp payment gateway, gọi external API, xử lý message queue

```plantuml
@startuml API_Retry_Pattern

title <b>Quy Trình Gọi External Service với Retry</b>

|#E8F4FD| Application Service |
start
:Chuẩn bị request payload;
:Khởi tạo retry_count = 0;

|#FFF3E0| Integration Layer |
repeat
  :Gọi External API;
  note right
    Timeout: 30 giây
    Max retry: 3 lần
    Backoff: 2^n giây
  end note
  
  if (Response nhận được?) then ([Có response])
    if (HTTP Status?) then ([2xx - Thành công])
      :Parse response body;
      #E8F8E8:Xử lý kết quả thành công;
      kill
    elseif ([4xx - Client Error])
      #FFE4E4:Ghi log lỗi client (không retry);
      :Trả về lỗi nghiệp vụ cho caller;
      kill
    else ([5xx - Server Error])
      #FFF9C4:Ghi log lỗi server;
      :Tăng retry_count;
      :Chờ backoff (2^retry_count giây);
    endif
  else ([Timeout / Network Error])
    #FFF9C4:Ghi log timeout;
    :Tăng retry_count;
    :Chờ backoff;
  endif
  
repeat while (retry_count < 3?) is ([Còn retry])
-> [Hết retry];

#FFE4E4:Ghi log "Max retry exceeded";
:Gửi alert cho Ops team;

|#E8F4FD| Application Service |
:Xử lý fallback (cache / default value / queue);
:Thông báo lỗi cho end user;
stop

@enduml
```

---

## PATTERN 04 — Order Processing (E-Commerce)

**Dùng khi**: Đặt hàng, thanh toán, fulfillment

```plantuml
@startuml Order_Processing

title <b>Quy Trình Xử Lý Đơn Hàng</b>

|#E8F4FD| Khách hàng |
start
:Chọn sản phẩm và thêm vào giỏ hàng;
:Xác nhận đơn hàng và chọn phương thức thanh toán;

|#FFF3E0| Order Service |
:Tạo đơn hàng với trạng thái PENDING;
:Kiểm tra tồn kho cho từng sản phẩm;

if (Đủ hàng?) then ([Tất cả còn hàng])
  :Tạm giữ (reserve) số lượng tồn kho;
else ([Có sản phẩm hết hàng])
  #FFE4E4:Thông báo sản phẩm hết hàng;
  :Đề xuất sản phẩm thay thế hoặc pre-order;
  stop
endif

|#F0FFF0| Payment Service |
:Thực hiện giao dịch thanh toán;
if (Thanh toán thành công?) then ([Thành công])
  :Xác nhận transaction_id;
else ([Thất bại / Từ chối])
  #FFE4E4:Ghi nhận lỗi thanh toán;
  |#FFF3E0| Order Service |
  :Giải phóng tồn kho đã reserve;
  :Cập nhật đơn hàng → PAYMENT_FAILED;
  |#E8F4FD| Khách hàng |
  :Thông báo thanh toán thất bại;
  stop
endif

|#FFF3E0| Order Service |
:Cập nhật đơn hàng → PAID;
:Gửi xác nhận đơn hàng qua email/SMS;

fork
  |#F5F0FF| Warehouse Service |
  :Nhận lệnh xuất kho;
  :Đóng gói và chuẩn bị hàng;
  :In phiếu giao hàng;
fork again
  |#FFF3E0| Order Service |
  :Tạo shipment record;
  :Gán mã vận đơn;
end fork

|#F5F0FF| Warehouse Service |
:Bàn giao hàng cho đơn vị vận chuyển;
:Cập nhật trạng thái → SHIPPED;

|#E8F4FD| Khách hàng |
:Nhận thông báo và tracking number;
:Nhận hàng;
:Xác nhận đã nhận hàng;

|#FFF3E0| Order Service |
#E8F8E8:Cập nhật đơn hàng → COMPLETED;
:Kích hoạt quy trình review & loyalty points;
stop

@enduml
```

---

## PATTERN 05 — Incident Management (IT/Support)

**Dùng khi**: Xử lý sự cố, ticket support, escalation

```plantuml
@startuml Incident_Management

title <b>Quy Trình Xử Lý Sự Cố</b>

|#E8F4FD| Người dùng / Monitor |
start
:Phát hiện sự cố / Nhận cảnh báo;
:Tạo ticket sự cố (mô tả, mức độ ưu tiên, ảnh chụp màn hình);

|#FFF3E0| Hệ thống ITSM |
:Tự động phân loại và gán mức độ ưu tiên;
:Gán ticket cho L1 Support;
:Bắt đầu đếm SLA timer;

|#F0FFF0| L1 Support |
:Tiếp nhận và xem xét ticket;
if (Giải quyết được?) then ([Có thể xử lý L1])
  :Áp dụng giải pháp từ knowledge base;
  :Xác nhận với người dùng;
  if (Người dùng xác nhận OK?) then ([Đã giải quyết])
    :Đóng ticket;
    #E8F8E8:Ghi nhận solution vào KB;
    stop
  else ([Chưa giải quyết])
    :Mở lại ticket;
  endif
else ([Vượt quá scope L1])
  :Escalate lên L2;
endif

|#F5F0FF| L2 Support / Engineering |
:Nhận ticket escalate;
:Phân tích root cause;
note right
  SLA escalation:
  P1: trong 1 giờ
  P2: trong 4 giờ
  P3: trong 24 giờ
end note

if (Tìm ra nguyên nhân?) then ([Xác định được])
  :Implement fix hoặc workaround;
  :Test trên môi trường staging;
  if (Test passed?) then ([OK])
    :Deploy fix lên production;
    :Xác nhận với người dùng;
  else ([Test failed])
    :Tìm giải pháp khác;
  endif
else ([Chưa tìm ra])
  :Escalate lên L3 / Vendor;
  ' Tiếp tục xử lý...
endif

|#FFF3E0| Hệ thống ITSM |
:Ghi nhận thời gian giải quyết;
:Cập nhật ticket → RESOLVED;
:Gửi survey đánh giá cho người dùng;

|#E8F4FD| Người dùng / Monitor |
#E8F8E8:Xác nhận sự cố đã được giải quyết;
stop

@enduml
```

---

## PATTERN 06 — Data Processing Pipeline (ETL/Batch)

**Dùng khi**: Xử lý file import, ETL, batch job, data migration

```plantuml
@startuml Data_Pipeline

title <b>Quy Trình Xử Lý Dữ Liệu Hàng Loạt</b>

|#E8F4FD| Scheduler / Trigger |
start
:Kích hoạt batch job (scheduled / manual);
:Ghi log bắt đầu với timestamp và job_id;

|#FFF3E0| Data Ingestion |
:Đọc dữ liệu từ nguồn (file / DB / API);
if (Dữ liệu nguồn accessible?) then ([Có thể đọc])
  :Load dữ liệu vào staging area;
else ([Lỗi kết nối / File không tồn tại])
  #FFE4E4:Ghi log lỗi ingestion;
  :Gửi alert qua email / Slack;
  stop
endif

|#F0FFF0| Data Validation |
:Kiểm tra schema và data types;
:Kiểm tra business rules (duplicates, ranges, FK...);
:Tạo báo cáo validation (valid_count, error_count);

if (Error rate <= threshold?) then ([Chấp nhận được])
  :Đánh dấu records lỗi, giữ lại records hợp lệ;
else ([Quá nhiều lỗi])
  #FFE4E4:Dừng pipeline — dữ liệu không đáng tin cậy;
  :Ghi log chi tiết lỗi;
  :Gửi báo cáo cho data owner;
  stop
endif

|#F5F0FF| Data Transformation |
fork
  :Transform dimension data;
fork again
  :Transform fact data;
fork again
  :Tính toán các aggregated metrics;
end fork
:Join và merge các dataset đã transform;

|#FFF3E0| Data Loading |
:Load vào destination (DWH / DB / File);
if (Load thành công?) then ([Thành công])
  :Cập nhật data lineage và metadata;
  :Commit transaction;
else ([Lỗi khi load])
  #FFE4E4:Rollback toàn bộ transaction;
  :Ghi log lỗi load;
  stop
endif

|#E8F4FD| Reporting |
:Tạo job execution report;
:Lưu trữ log và metrics;
#E8F8E8:Gửi báo cáo hoàn thành;
stop

@enduml
```
