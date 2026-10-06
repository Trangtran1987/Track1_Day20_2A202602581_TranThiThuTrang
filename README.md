# Track1_Day20_2A202602581_TranThiThuTrang
Họ tên: Trần Thị Thu Trang
Mã học viên: 2A202602581

# 00—Phạm_vi
1. Dự án: BookingBot AI Agent giành cho khách hàng có nhu cầu tìm và xem bất động sản Vinhomes.
2. Persona: Người có ý định mua bất động sản về Vinhomes đã xác định rõ một số tiêu chí trong mua nhà của mình như tài chính, số phòng ngủ, vị trí...
3. Core job: Giúp tôi nhanh chóng tìm được căn Vinhomes phù hợp và sắp xếp được lịch xem nhà thuận tiện mà không phải mất nhiều thời gian tìm kiếm, trao đổi qua nhiều bên trung gian.
# 01—Core_action
Target user: Buyer BĐS Vinhomes  
Core job: Tìm được căn phù hợp và nhanh chóng sắp xếp lịch xem nhà.  
Core action: Giao mục tiêu cho AI để AI tạo yêu cầu xem nhà cho căn phù hợp.  
Object: Viewing Request.  
Preconditions: Có nhu cầu đủ rõ, căn/Owner đã xác thực, có slot phù hợp.  
Completion rule: Viewing Request được backend ghi nhận thành công ở trạng thái REQUESTED và gửi tới Owner.  
Core value: Tiết kiệm thời gian tìm kiếm và điều phối lịch xem, giảm phụ thuộc vào trung gian.  
Evidence of value: Buyer nhận được request/booking ID và khung giờ cụ thể; Owner nhận được yêu cầu xác nhận.
# 02 — Nature & cadence
1. Action Nature Card
Thành phần |	Câu trả lời cho BookingBot
Actor      |    Buyer / người mua BĐS là người khởi tạo hành vi; AI Agent thực hiện chuỗi tác vụ để tạo Viewing Request.
Intent     |    Buyer muốn tìm và xem một căn Vinhomes phù hợp mà không phải tự tìm kiếm, kiểm tra lịch và liên hệ nhiều bên.
Trigger    |	Chủ yếu do Buyer chủ động khi phát sinh nhu cầu tìm/xem nhà; ngoài ra có thể xuất hiện lại khi yêu cầu trước bị từ chối, không có slot phù hợp hoặc có nhu cầu xem thêm căn khác.
Effort     |	Effort ban đầu thấp đến trung bình: Buyer chỉ cần mô tả mục tiêu bằng ngôn ngữ tự nhiên. Phần tìm căn, matching, kiểm tra lịch và tạo request được AI thực hiện.
Value timing|	Trễ và phụ thuộc người khác: sau khi AI tạo request, Buyer chưa nhận được toàn bộ value; cần Owner xác nhận và cuối cùng Buyer thực sự xem nhà.
State       |	Hệ thống lưu Buyer profile/nhu cầu, Property được chọn, Viewing Request, thời gian yêu cầu, Booking ID và trạng thái như REQUESTED → CONFIRMED → VIEWED/COMPLETED.
Dependency  |	Phụ thuộc nguồn cung căn phù hợp, Availability của căn, Owner xác nhận và thời gian xem nhà.
Repeat condition|	Action xuất hiện lại khi Buyer muốn xem căn khác, muốn xem thêm căn để so sánh, yêu cầu trước không thành công, Owner không phản hồi/từ chối hoặc Buyer tiếp tục tìm nhà trong cùng quá trình mua.
2. Kết luận cadence
Nature: Hành vi theo dự án (project-based).  
Cadence: Theo dự án tìm nhà; báo cáo theo tuần.  
Lý do: Buyer chỉ thực hiện Core Action khi đang có nhu cầu tìm mua/xem nhà. Trong một quá trình tìm nhà, action có thể lặp lại nhiều lần nhưng không có frequency cố định và nhiều hơn không đồng nghĩa với nhiều value hơn.
Đối với Buyer đang trong quá trình tìm mua BĐS Vinhomes, core action "giao mục tiêu cho AI để tạo yêu cầu xem nhà cho căn phù hợp" thường xuất hiện nhiều lần trong một quá trình tìm nhà, vì Buyer có thể cần xem và so sánh nhiều căn trước khi tìm được căn phù hợp, đồng thời action phụ thuộc vào nguồn cung và phản hồi của Owner. Do đó, đây là hành vi theo dự án (project-based), và nhịp đo phù hợp là theo dự án ở cấp Buyer; có thể tổng hợp theo tuần để theo dõi.
# 03 — Metric System + Retention
1. Activation metric
- Start event:	Buyer gửi mục tiêu tìm/xem nhà lần đầu cho AI Agent, ví dụ: "Cuối tuần này tìm giúp tôi căn 2PN Ocean Park dưới 5 tỷ và đặt lịch xem."
- Activation event:	viewing_request_created — AI đã tìm được căn phù hợp, kiểm tra availability và tạo thành công yêu cầu xem nhà cho Buyer.
- Time window:	Trong cùng phiên tìm nhà / tối đa 24 giờ từ Start event.
2. Engagement metric
- Do BookingBot là sản phẩm project-based, không nên dùng "số lần mở app/ngày".
Mình chọn Frequency + Depth.
① Frequency: Số Viewing Request được tạo thành công trên mỗi Buyer trong một search project.

Ví dụ:
Buyer	Search project	Viewing Request
A	Tìm căn Ocean Park	     3
B	Tìm căn Smart City	     1
C	Tìm căn Ocean Park	     4

Vì sao quan trọng?
Buyer có thể cần xem nhiều căn trước khi tìm được căn phù hợp. Số request phản ánh mức độ Buyer sử dụng BookingBot để tiến hành quá trình tìm nhà.
Nhưng: nhiều hơn không mặc định là tốt hơn. Nếu Buyer phải tạo 10 request vì AI matching kém thì đó là tín hiệu xấu.
② Depth
Tỷ lệ Viewing Request dẫn tới Owner Confirmation và hoàn tất Viewing.

Ví dụ:
10 Viewing Requests
        ↓
8 Owner Confirm
        ↓
6 Buyer thực sự đi xem

→ Depth của engagement không chỉ là "đã tạo request", mà là request có tạo ra tiến triển thực tế hay không.
Ưu tiên metric này hơn "số phút chat với AI", vì chat càng lâu không có nghĩa sản phẩm càng tốt.

3. Retention Definition — đủ 6 thành phần

Retention Card
Thành phần	|   Định nghĩa cho BookingBot
Unit        |	Buyer / người mua có một search project
Cohort entry|	Buyer tạo Viewing Request đầu tiên thành công (viewing_request_created)
Return event|	Buyer tiếp tục tạo một Viewing Request mới trong cùng search project
Window   	|   Project-based / custom bracket, theo thời gian của một hành trình tìm nhà; có thể phân tích các mốc 7/14/30 ngày nhưng không coi đó là cadence tự nhiên
Threshold   |	Ít nhất 1 core action lặp lại trong cùng search project
Segment     |	Activated Buyer đang trong quá trình tìm mua BĐS Vinhomes

Định nghĩa đầy đủ
Retention của BookingBot là tỷ lệ Buyer đã tạo Viewing Request đầu tiên và tiếp tục tạo ít nhất một Viewing Request khác trong cùng search project trong khoảng thời gian project đó còn diễn ra.


# 04 — North Star + leading + counter
1. North Star Metric theo công thức:Số lượt Buyer hoàn tất xem một căn phù hợp, đã được Owner xác nhận / số search project đang hoạt động
2. Leading indicators : 
Leading 1	Agentic Booking Completion Rate	Agent tự xử lý được chuỗi tìm → matching → availability → request
Leading 2	Precision@5	Chất lượng Top 5 căn đề xuất
Leading 3	Owner Confirmation Rate	Khả năng biến request thành lịch thực tế
3. Counter-metric 
2 counter-metric.
🛑 Counter 1 — No-show Rate
Số lịch đã được xác nhận nhưng Buyer không đến xem / tổng số lịch đã xác nhận.
Bởi vì nếu team tối ưu để tăng Successful Viewing bằng cách tạo thật nhiều booking, nhưng Buyer không thực sự đi xem thì chất lượng sản phẩm đang xấu đi.
🛑 Counter 2 — AI Cost per Successful Viewing
Tổng chi phí AI/API / số lượt xem nhà thành công.
Bởi vì BookingBot càng Agentic thì càng có thể:
LLM → Search → Ranking → Availability → Booking → Notification
Nếu Agent làm nhiều việc hơn nhưng chi phí cho mỗi lượt xem thành công tăng quá cao, product không bền vững.

# 05 — Product Loop
1. Product Loop
┌─────────────────────────────────────────┐
│ Natural trigger                         │
│ Buyer cần tìm/xem BĐS Vinhomes          │
└────────────────┬────────────────────────┘
                 ↓
┌─────────────────────────────────────────┐
│ Core Action                             │
│ Giao mục tiêu cho AI                    │
└────────────────┬────────────────────────┘
                 ↓
┌─────────────────────────────────────────┐
│ Immediate Value                         │
│ AI tìm căn + matching + availability    │
│ + tạo Viewing Request                   │
└────────────────┬────────────────────────┘
                 ↓
┌─────────────────────────────────────────┐
│ Saved State / Investment                │
│ Profile + preference + lịch sử +       │
│ booking/viewing status                  │
└────────────────┬────────────────────────┘
                 ↓
       Buyer vẫn chưa tìm được
       căn phù hợp / muốn xem thêm
                 ↓
        Natural trigger mới
                 ↓
           Core Action
                 ↓
             Repeat...
2. Loại loop
Project Loop – vòng lặp theo dự án tìm mua nhà
3. Metric Hypothesis
Nếu loop Project này hoạt động, metric Viewing Request → Completed Viewing Rate sẽ tăng theo hướng tích cực trong mỗi search project trong vòng 7–30 ngày, vì Buyer có thể tiếp tục giao mục tiêu cho AI dựa trên preference và trạng thái đã được lưu thay vì phải bắt đầu lại từ đầu.

# 06 — Tracking nhanh
7 core events:
Tên event	           |Ý nghĩa  |	Thời điểm ghi nhận	|Metric sử dụng
search_project_started | Buyer thực sự bắt đầu một hành trình tìm nhà mới|Khi Buyer gửi mục tiêu tìm/xem nhà đầu tiên và hệ thống tạo search project thành công|	Activation Rate
viewing_request_created|Viewing Request đã thực sự được tạo thành công| Sau khi backend ghi request thành công với trạng thái REQUESTED|	Activation Rate; Core Action; Engagement
owner_confirmation_received|	Owner thực sự xác nhận yêu cầu xem nhà|	Khi backend nhận và ghi thành công trạng thái CONFIRMED từ Owner|	Owner Confirmation Rate
viewing_hold_created|	Hệ thống thực sự tạo Viewing Hold cho booking đã được xác nhận|	Sau khi hold được ghi thành công và không có conflict|	Booking/Viewing funnel; Operational monitoring
viewing_completed|	Buyer thực sự hoàn tất buổi xem nhà|	Khi booking/viewing chuyển sang trạng thái COMPLETED/VIEWED theo business rule|	North Star / Successful Viewing
viewing_no_show|	Booking đã xác nhận nhưng Buyer không thực hiện buổi xem|	Khi hệ thống xác định booking đã qua thời gian xem mà không có trạng thái completed|	No-show Rate
search_project_completed|	Search project kết thúc theo business rule|	Khi Buyer đạt trạng thái kết thúc project, ví dụ đã hoàn thành mục tiêu hoặc chủ động kết thúc|	Project-level analysis; Retention


1. Event quan trọng nhất: viewing_request_created
Đây là Core Action Event.

2. viewing_completed
Đây là event quan trọng nhất đối với North Star.

Acceptance criteria:
1. Event chỉ được ghi khi hành vi/trạng thái thực sự hoàn tất, không ghi khi user mới click hoặc có ý định.
2. Reload, retry, double-click hoặc autosave không tạo event trùng cho cùng một lần chuyển trạng thái.
Logic cuối cùng
Natural trigger → Agentic Core Action → Viewing Request → Owner confirmation → Viewing → Value → Saved state → Next need → Repeat.
Điểm hay của loop này là không cần tạo artificial habit. BookingBot không cần tìm cách khiến Buyer "quay lại mỗi ngày"; nó cần giúp Buyer hoàn thành project tìm nhà càng hiệu quả càng tốt.