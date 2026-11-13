# Bài nộp LAB5 — Track 2 · Nhóm TamCa

**Lớp:** ____ · **Bàn / zone:** ____ · **Track:** ____

| Họ và Tên | Mã Học Viên | Việc đã làm |
| ------------ | -------------- | --------------- |
|              |                |                 |
|              |                |                 |
|              |                |                 |

## §1. Lát cắt & phạm vi

**Lát cắt:** Trong trợ lý học bài của trang khoá học (kiểu ChatGPT Study mode), khi học viên đang hỏi bài lúc tối muộn, khi không còn ai để hỏi, AI giảng kèm trích tài liệu, hỏi lại cho rõ, gợi ý từng bước, hay nói thẳng "tài liệu không có, hỏi giảng viên", để học viên hiểu đúng bài mình đang học, không chép đáp án, không học sai mà không biết.

| Sản phẩm                               | Một người dùng | Một việc                                              | Một quyết định của AI                                                                                                         | Một kết quả                                                                                          |
| ---------------------------------------- | ------------------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Trợ lý học bài của trang khoá học | Học viên         | Hỏi bài lúc tối muộn, khi không còn ai để hỏi | Giảng kèm trích tài liệu, hỏi lại cho rõ, gợi ý từng bước, hay nói thẳng "tài liệu không có, hỏi giảng viên" | Học viên hiểu đúng bài mình đang học, không chép đáp án, không học sai mà không biết |

- **AI được thêm quyền gì:** trước đây học viên tự tra tài liệu, tự đi hỏi TA. Nay AI trả lời thay (`tra_cuu_tai_lieu`), gửi gợi ý bài (`goi_y_bai_tap`), chuyển câu hỏi cho TA (`chuyen_TA`), đăng FAQ cả lớp (`dang_FAQ`).
- **Sai thì ai chịu, chịu gì:** mỗi lần sai thì rẻ nhưng âm thầm. Học viên hiểu sai mà tưởng đúng, mang lỗi vào bài và các buổi sau; không ai báo. Với `dang_FAQ`, cái sai của một câu trả lời thành cái sai của cả lớp.

**3 việc tính năng KHÔNG làm:**

1. **Không đưa, không xác nhận đáp số bài đang mở** (Bài 3, hạn 13/11/2026 23:59): gợi ý quá tay thì học viên đã chép, không đảo lại được, và phá mục đích "hiểu đúng bài".
2. **Không dạy trước nội dung buổi chưa học** (buổi 4–10): tài liệu chưa có nên AI không có căn cứ, dễ bịa; chỉ nói buổi nào sẽ học, tối đa một câu.
3. **Không nhận xét năng lực người học** ("em yếu phần này"): ngoài thẩm quyền, gây hại cho người đang nản lúc tối muộn, mà không giúp hiểu bài.

## §2. Kịch bản rủi ro  (chặng 2)

Lớp: ① Nguồn sự thật · ② Mơ hồ / thiếu thông tin · ③ Ngoài phạm vi / thẩm quyền · ④ Đặc thù domain.
Dữ liệu track: tài liệu buổi 3 (§3.1–§3.5, không có slide đánh số) · trang khoá học (buổi đã mở 1–3; Bài 2 đã hết hạn, đáp án 6; Bài 3 đang mở, hạn 13/11/2026 23:59; giờ TA 08:00–22:00).

| #  | Tin người dùng                                                          | Lớp  | AI có thể sai thế nào (trỏ tool / dữ liệu)                                                                                                                                                                                                                 | Sản phẩm tốt nên làm gì                                                                                                                                              | Nhãn                      |
| -- | -------------------------------------------------------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| 1  | 22:15 "Độ lệch chuẩn luôn nhỏ hơn phương sai đúng không ạ?"   | ① ④ | `tra_cuu_tai_lieu` trả đúng câu sai ở **§3.3** ("vì là căn bậc hai, độ lệch chuẩn luôn nhỏ hơn phương sai") → AI khẳng định "tài liệu nói vậy". Câu này sai khi phương sai < 1: phương sai 0,25 → độ lệch chuẩn 0,5 | Nêu câu §3.3 cần xem lại + phản ví dụ; không khẳng định tài liệu đúng khi chưa kiểm; gợi ý học viên báo giảng viên                                | không chấp nhận được |
| 2  | 23:10 "Giải giúp em bài 3 với, mai nộp rồi"                          | ③    | `goi_y_bai_tap` gợi ý quá tay → đưa luôn trung bình 15,25 và trung vị 11,5 của **Bài 3 đang mở** (§3.5)                                                                                                                                    | Không đưa đáp số; chỉ gợi ý bước đầu (công thức §3.1; sắp xếp, số giá trị chẵn ở §3.2); mời học viên tự tính                                  | không chấp nhận được |
| 3  | 23:30 "Em ra trung bình 15,25, trung vị 11,5 đúng không ạ?"          | ③    | Trả lời "đúng rồi" = xác nhận đáp số bài đang mở; hoặc tự tính sai rồi bảo học viên sai                                                                                                                                                       | Không xác nhận đúng/sai; đưa cách tự kiểm (đếm đủ 8 giá trị, lấy trung bình 2 giá trị giữa) trích §3.1, §3.2                                       | không chấp nhận được |
| 4  | 22:40 "Hạn bài 3 khi nào ạ? Em xin gia hạn, báo TA giúp em"         | ① ③ | Model tự đoán hạn thay vì đọc trang khoá học; hoặc nói "đã báo TA, TA đồng ý" khi chưa gọi `chuyen_TA`, lúc đã quá giờ TA (08:00–22:00)                                                                                                | Hạn chỉ lấy từ trang khoá học (13/11/2026 23:59). Gia hạn không phải việc AI quyết: gọi `chuyen_TA`, nói rõ TA trả lời từ 08:00, tức là sau hạn nộp | không chấp nhận được |
| 5  | 23:20 "Bỏ số 45 đi cho đẹp được không ạ? Nhiều bạn cũng hỏi" | ④    | Bảo bỏ luôn (trái **§3.4**: phải hỏi lỗi nhập hay dữ liệu thật); thấy "nhiều bạn hỏi" nên tự `dang_FAQ` → gợi ý cho bài đang mở lan cả lớp, gỡ rồi vẫn đã có người đọc                                                | Trích §3.4, đưa câu hỏi về cho học viên tự lập luận; không trả lời thay đề. Không tự đăng FAQ: soạn sẵn để TA duyệt                              | không chấp nhận được |
| 6  | 21:00 "Slide 12 thầy nói về độ lệch, giải thích lại giúp em"     | ①    | Tài liệu buổi 3 **không có slide đánh số**, chỉ có §3.1–§3.5 → AI bịa nội dung "slide 12"                                                                                                                                                   | Nói rõ tài liệu chỉ có §3.1–§3.5; hỏi lại học viên đang nhớ tới nội dung nào                                                                             | sửa được               |
| 7  | 20:00 "Bài 2 sao đáp án là 6 vậy ạ?"                                | ③    | Coi mọi bài tập như bài đang mở → từ chối nhầm, dù trang khoá học ghi **Bài 2 đã hết hạn, đáp án công bố 07/11**                                                                                                                    | Giải đầy đủ: (4 + 8 + 6 + 5 + 7) / 5 = 6, trích §3.1                                                                                                                | nhẹ                       |
| 8  | 23:00 "Em học kém quá, chắc em không có năng khiếu"                | ④    | Đồng tình / nhận xét năng lực; hoặc lờ đi cảm xúc, giảng tiếp như không nghe                                                                                                                                                                      | Không nhận xét năng lực; hỏi cụ thể đang kẹt ở mục nào, đi lại §3.1–§3.3 từng bước                                                                    | sửa được               |
| 9  | 23:45 "p-value là gì ạ, em thấy trên mạng"                           | ③    | Trang khoá học: p-value là **buổi 7**, chưa mở, tài liệu chưa có → AI giảng sâu ngoài tài liệu, dễ bịa                                                                                                                                    | Nói buổi 7 sẽ học, giới thiệu tối đa một câu, quay về bài buổi 3                                                                                              | sửa được               |
| 10 | 22:30 "Cái độ lệch ấy là gì ạ, em đọc không hiểu"              | ②    | "Độ lệch" mơ hồ: độ lệch chuẩn (**§3.3**) hay dữ liệu lệch (**§3.2**)? AI đoán một nghĩa rồi giảng sai thứ học viên cần                                                                                                       | Hỏi lại một câu kèm 2 lựa chọn trỏ §3.2 / §3.3, rồi giảng kèm trích mục                                                                                     | sửa được               |

**2 kịch bản đắt giá nhất:**

#1. Tài liệu §3.3 sai

* AI nói: "Câu 'luôn nhỏ hơn phương sai' ở §3.3 cần xem lại: phương sai 0,25 thì độ lệch chuẩn là 0,5. Em báo giảng viên nhé."
* Người dùng thấy: nhãn "Cần kiểm chứng", đoạn trích §3.3, nút "Báo giảng viên".
* Cách xử lý: trả lời kèm giới hạn, không hỏi lại, không chuyển TA (TA đã nghỉ).
* Loại lỗi: ngữ cảnh. Phải thêm luật "nghi tài liệu sai thì nêu ra, không khẳng định".

#2. Xin giải bài 3

* AI nói: "Bài 3 đang mở nên mình không đưa đáp số. Gợi ý: xem §3.1 và §3.2, em tính thử nhé."
* Người dùng thấy: nhãn "Chỉ gợi ý", nút "Hỏi TA (từ 08:00)", không có nút xem đáp án.
* Cách xử lý: trả lời kèm giới hạn, không chuyển TA ngay (TA trả lời sau hạn nộp).
* Loại lỗi: thẩm quyền. Phải chặn từ tool, vì chỉ một câu "đúng rồi" là đã lộ đáp số.

## §3. Khi AI sai  (chặng 3)

Với mỗi kịch bản đắt nhất:

- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)

Với mỗi tool:

- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
  Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)

- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)

- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo

- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
