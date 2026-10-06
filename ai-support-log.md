# AI Support Log

Họ tên: Trần Thị Thu Trang
Mã học viên: 2A202602581
Dự án: BookingBot AI Agent — tìm và đặt lịch xem bất động sản Vinhomes

| Mục | Công cụ AI | Mục đích sử dụng | Mức độ dùng lại gợi ý |
|---|---|---|---|
| 00 — Dự án, persona, core job | ChatGPT | Hỗ trợ mô tả BookingBot, xác định persona Buyer, vấn đề, giá trị cốt lõi và phân biệt Core Job với tính năng. | Giữ phần lớn, sau đó người dùng kiểm tra và chỉnh theo MVP thực tế. |
| 01 — Core Action Card | ChatGPT | Phân tích Core Job và đề xuất Core Action; so sánh “hoàn tất xem nhà” với “tạo Viewing Request”; xác định Actor, Intent, Trigger, Object, Completion Rule và Value. | Sửa đáng kể. Chọn “Buyer giao mục tiêu cho AI để AI tạo Viewing Request cho căn phù hợp”; “hoàn tất xem nhà” được giữ làm Core Value Event. |
| 02 — Action Nature Card + cadence | ChatGPT | Phân tích nature của Core Action và xác định cadence dựa trên hành vi thực tế. | Giữ và tinh chỉnh. Chọn project-based; Weekly chỉ là nhịp báo cáo, không phải cadence tự nhiên. |
| 03 — Metric System + Retention | ChatGPT | Xây Activation, Engagement, North Star, Leading Indicators và Counter-metrics. | Giữ có chọn lọc. Giữ viewing_request_created, Precision@5, Owner Confirmation Rate và counter-metrics; bỏ các metric chỉ đo activity. |
| 04 — Retention Definition | ChatGPT | Xây retention theo 6 thành phần và đối chiếu với nature project-based. | Sửa đáng kể. Không dùng máy móc D7/D30; giữ project-based retention. |
| 05 — Product Loop | ChatGPT | Suy ra loop từ Core Action và metric; xác định Natural Trigger → Core Action → Immediate Value → Saved State → Next Trigger. | Giữ và tinh chỉnh. Chọn Project Loop, không dùng streak/badge/notification để ép quay lại. |
| 06 — Tracking | ChatGPT | Xác định core events, thời điểm ghi nhận, metric tương ứng và acceptance criteria chống event giả/trùng. | Giữ phần lớn, kiểm tra lại với backend. Giữ search_project_started, viewing_request_created, owner_confirmation_received, viewing_completed; team kỹ thuật cần xác nhận khả năng tracking. |
