# Thin SPEC – Day 05

## 1. Track, Product/App và User

**Track:** Learning OS

**Product/App thật:** V-App – V-AI

**User cụ thể:** Người dùng sử dụng V-AI để hỗ trợ học tập, lập trình và tạo nội dung.

**Nhóm có phải user thật không?**

Có.

Nhóm đã trực tiếp sử dụng V-AI để thực hiện các tác vụ như tạo website đơn giản, bổ sung tính năng cho website và xin lời khuyên trong các tình huống thực tế.

---

# 2. Evidence Summary

| Evidence                                                                | Nguồn               | User/Pain nói lên điều gì?                                              | SPEC phải đổi gì?                               |
| ----------------------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------- | ----------------------------------------------- |
| User yêu cầu: "Tạo cho tôi một trang web đặt xe đơn giản"               | Observation từ V-AI | AI có khả năng sinh code và hoàn thành task cơ bản                      | Không cần thay đổi                              |
| User yêu cầu: "Thêm cho tôi vài chức năng đi"                           | Observation từ V-AI | User đưa ra yêu cầu mơ hồ nhưng AI vẫn tự quyết định chức năng cần thêm | Cần bổ sung Low-Confidence Path                 |
| AI tự sinh chức năng kiểm tra dữ liệu, chọn loại xe, thông báo xác nhận | Observation từ V-AI | AI suy diễn intent thay vì xác nhận lại nhu cầu                         | Cần thêm bước làm rõ intent trước khi sinh code |
| User phải tự đánh giá kết quả có đúng nhu cầu hay không                 | Observation từ V-AI | Không có cơ chế xác nhận intent hoặc correction rõ ràng                 | Bổ sung UX Recovery và Correction Path          |

---

# 3. Pain Statement

User sử dụng V-AI để hỗ trợ lập trình đang gặp khó khăn ở bước mở rộng yêu cầu sau khi đã có kết quả ban đầu,

vì AI không nhận diện được khi yêu cầu còn mơ hồ và tự suy diễn nhu cầu của người dùng,

dẫn tới việc sinh ra kết quả không đúng mong muốn thực tế và làm tăng số lần chỉnh sửa.

Bằng chứng chính là khi người dùng yêu cầu:

> "Thêm cho tôi vài chức năng đi"

AI đã tự động lựa chọn và sinh các chức năng mà không hỏi lại người dùng muốn chức năng nào.

---

# 4. Build Slice

Cho người dùng đang sử dụng AI hỗ trợ lập trình,

prototype sẽ dùng AI để **augment** quá trình làm rõ yêu cầu trước khi sinh code,

tạo ra danh sách các lựa chọn chức năng phù hợp,

và xử lý failure mode "intent mơ hồ" bằng cách yêu cầu người dùng xác nhận nhu cầu trước khi sinh mã nguồn.

---

# 5. Auto/Aug Decision

## Chọn:

✅ Augmentation

AI gợi ý các lựa chọn chức năng.

Người dùng quyết định chức năng nào sẽ được triển khai.

### Lý do chọn

Yêu cầu lập trình thường có nhiều cách diễn giải khác nhau.

Nếu AI tự động quyết định sẽ dễ sinh ra kết quả không đúng nhu cầu.

Cho người dùng xác nhận trước giúp giảm rủi ro hiểu sai intent.

### Human Role

**Decider**

Người dùng là người quyết định cuối cùng về chức năng cần triển khai.

---

# 6. Four Paths

| Path           | Prototype phải thể hiện gì?                                        |
| -------------- | ------------------------------------------------------------------ |
| Happy          | User chọn chức năng cụ thể, AI sinh code đúng yêu cầu              |
| Low-Confidence | User đưa yêu cầu mơ hồ, AI hiển thị danh sách lựa chọn để xác nhận |
| Failure        | AI sinh chức năng không đúng nhu cầu của user                      |
| Correction     | User thay đổi lựa chọn, AI sinh lại kết quả phù hợp                |

---

# 7. Failure Mode Nguy Hiểm Nhất

Nếu user nhập:

> "Thêm cho tôi vài chức năng đi"

AI có thể:

Tự suy diễn intent và sinh các chức năng không đúng nhu cầu thực tế.

Hậu quả là:

- Tăng số lần chỉnh sửa.
- Giảm hiệu quả làm việc.
- Người dùng mất niềm tin vào AI.

Prototype sẽ xử lý bằng:

- Ask Again
- Show Options

Ví dụ:

"Bạn muốn thêm chức năng nào?"

- Đăng nhập
- Thanh toán
- Định vị GPS
- Theo dõi tài xế
- Đặt lịch trước

**Owner kiểm thử path này:** Nguyễn Hoàng Thanh Tùng

---

# 8. Owner Plan Cho Sáng Day 06

| Thành viên              | Việc phụ trách      | Bằng chứng cần có trong repo                |
| ----------------------- | ------------------- | ------------------------------------------- |
| Nguyễn Hoàng Thanh Tùng | Research / Evidence | Screenshot V-AI, query test, finding note   |
| Nguyễn Hoàng Thanh Tùng | SPEC                | Thin SPEC hoàn chỉnh                        |
| Nguyễn Hoàng Thanh Tùng | Prototype           | Flow demo bằng HTML/Figma hoặc web đơn giản |
| Nguyễn Hoàng Thanh Tùng | Test / Failure Path | Happy path và Low-Confidence path           |
| Nguyễn Hoàng Thanh Tùng | Demo Script / Repo  | Demo narrative, README, repo structure      |

---

# Product Decision

Khi người dùng đưa ra yêu cầu có nhiều cách diễn giải khác nhau, hệ thống không được sinh code ngay.

Hệ thống phải kích hoạt Low-Confidence Path, hiển thị các lựa chọn phù hợp và yêu cầu người dùng xác nhận intent trước khi thực hiện.

Mục tiêu là giảm lỗi hiểu sai nhu cầu và tăng chất lượng kết quả đầu ra.
