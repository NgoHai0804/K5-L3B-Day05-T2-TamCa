# HƯỚNG DẪN LÀM LAB5 — Track T2 (Giáo dục) · Nhóm TamCa

> Tài liệu này là **việc cần làm từng bước** cho nhóm. Đọc kèm đề gốc trong repo bài giảng
> `D:\AI20K\Day05\lab\K5-L3-Day05-AI-Product-UX-Autonomy\`:
> `01-challenge-brief.md` · `02-guide.md` · `03-spec-template.md` · `04-rubric.md` ·
> `tracks/t2-education.md` · `prototype-sample/index.html`.
>
> **Lớp L3B · hạn nộp: 23:59 ngày 13/11/2026** (đúng ngày lab). Nộp **link repo công khai**.
> **Đây là bài thiết kế, KHÔNG chạy agent, KHÔNG chat với sản phẩm thật.**

---

## 0. Trạng thái repo hiện tại & việc sửa trước tiên

Repo này đang có:

```
K5-L3B-Day05--track--TamCa/
├── .git/         ← git đã init, nhánh main, chưa có remote
├── spec.md       ← ĐANG TRỐNG, phải viết (copy từ 03-spec-template.md)
└── prototype/    ← ĐANG TRỐNG, phải bỏ file prototype + ảnh vào
```

### Việc 0.1 — Sửa tên repo cho đúng chuẩn

Chuẩn bắt buộc: `K5-<lớp>-Day05-<track>-<tên nhóm>`. Track của nhóm là **T2**, không phải chữ "track".

**Tên đúng: `K5-L3B-Day05-T2-TamCa`**

- Tên **thư mục local** chỉ để làm việc; cái bị chấm là **tên repo trên GitHub**. Khi tạo repo GitHub, đặt đúng `K5-L3B-Day05-T2-TamCa`.
- Nếu muốn sửa cả thư mục local cho gọn thì đổi tên sau khi lab xong, đừng để mất thời gian giữa giờ.
- **Repo phải PUBLIC.** Mở bằng cửa sổ ẩn danh (Ctrl+Shift+N) phải xem được.

### Việc 0.2 — Tạo repo GitHub & push

1. Tạo repo **mới, trống, công khai** trên GitHub tên `K5-L3B-Day05-T2-TamCa`. **Không fork** repo đề bài.
2. Nối remote và push (thay URL bằng repo của nhóm):

```
git remote add origin https://github.com/<tài-khoản>/K5-L3B-Day05-T2-TamCa.git
git add .
git commit -m "Khoi tao bai nop LAB5 track T2"
git branch -M main
git push -u origin main
```

3. Push sớm một lần để chắc chắn nộp được, sau đó push dần theo tiến độ.

### Việc 0.3 — Cấu trúc đích cuối cùng

```
K5-L3B-Day05-T2-TamCa/
├── spec.md              ← bài nộp theo dàn ý (bảng thành viên ở ĐẦU file)
├── prototype/
│   ├── index.html       ← prototype bấm được (1–2 màn hình)
│   ├── 01-....png       ← 1–2 ảnh có ĐÁNH SỐ các chỗ (§5)
│   └── (tùy chọn) ai-log.txt  ← nếu có lời gọi AI thật
└── HUONG-DAN.md         ← file này
```

---

## 1. Bối cảnh track T2 trong một khối (đọc 10 phút — Chặng 1)

**Sản phẩm nền:** trợ lý học bài kiểu ChatGPT **Study mode**, tích hợp vào **trang khoá học** có tài liệu buổi học, lịch bài tập và TA.

**Lát cắt (phát sẵn — KHÔNG chọn lại):**

> Trong **trợ lý học bài của trang khoá học**, khi **học viên** đang hỏi bài lúc tối muộn, khi không còn ai để hỏi, **AI giảng kèm trích tài liệu, hỏi lại cho rõ, gợi ý từng bước, hay nói thẳng "tài liệu không có, hỏi giảng viên"**, để học viên hiểu đúng bài mình đang học, không chép đáp án, không học sai mà không biết.

| Một người dùng | Một việc | Một quyết định AI | Một kết quả |
|---|---|---|---|
| học viên | hỏi bài lúc tối muộn, không còn ai để hỏi | giảng kèm trích tài liệu / hỏi lại / gợi ý từng bước / nói thẳng "tài liệu không có" | hiểu đúng bài, không chép đáp án, không học sai mà không biết |

**Cái giá khi sai:** rẻ mỗi lần nhưng **âm thầm** — học viên học sai mà không biết, và không ai báo. Đây **không** phải sai gây mất tiền/mất mạng ngay, mà là sai **tích tụ**.

### Bảng tool (chưa có mức tự chủ — nhóm tự đặt ở Chặng 4)

| Tool | Làm gì | Đảo lại được không |
|---|---|---|
| `tra_cuu_tai_lieu` | Tìm trong tài liệu buổi đã học, trả đoạn kèm mã mục | Chỉ đọc |
| `goi_y_bai_tap` | Gửi gợi ý làm bài cho một học viên | Gợi ý quá tay thì học viên đã chép |
| `chuyen_TA` | Chuyển câu hỏi cho TA, báo giờ TA trả lời | Được |
| `dang_FAQ` | Đăng câu hỏi và trả lời vào FAQ cả lớp | Gỡ được, nhưng nhiều người đã đọc |

### Dữ liệu dựng (thứ duy nhất trợ lý được dựa vào)

**A — Tài liệu buổi 3 "Thống kê mô tả"** (học viên đang ở buổi 3; tài liệu KHÔNG có slide đánh số, chỉ có §3.1…§3.5):
- **§3.1 Trung bình cộng.** Tổng các giá trị chia số giá trị. Bị kéo mạnh bởi giá trị ngoại lai.
- **§3.2 Trung vị.** Giá trị đứng giữa khi sắp xếp tăng dần; nếu số giá trị chẵn thì là trung bình cộng hai giá trị giữa. Ít bị ảnh hưởng bởi ngoại lai → dùng cho dữ liệu lệch như thu nhập, giá nhà.
- **§3.3 Phương sai và độ lệch chuẩn.** Phương sai đo mức phân tán quanh trung bình; độ lệch chuẩn là căn bậc hai của phương sai, cùng đơn vị với dữ liệu. *(Cảnh báo: câu "độ lệch chuẩn luôn nhỏ hơn phương sai" là chỗ tài liệu sai — xem §3 Chặng 2.)*
- **§3.4 Giá trị ngoại lai.** Giá trị khác hẳn phần lớn dữ liệu; trước khi bỏ phải hỏi: lỗi nhập liệu hay dữ liệu thật?
- **§3.5 Bài tập 3.** Lương 8 nhân viên (triệu đồng): 9, 10, 10, 11, 12, 12, 13, 45. (a) Tính trung bình và trung vị. (b) Con số nào mô tả "lương điển hình" tốt hơn? Vì sao?

**B — Trang khoá học:**
- Buổi đã mở: **1, 2, 3**.
- Đề cương buổi sau: 4 Trực quan hoá dữ liệu · 5 Xác suất cơ bản · 6 Phân phối chuẩn · **7 Kiểm định giả thuyết và p-value** · 8 Hồi quy tuyến tính · 9 Làm sạch dữ liệu · 10 Dự án cuối khoá.
- Công cụ: bài tập làm bằng **bảng tính**.
- Bài tập 2: hạn 06/11 23:59 · **đã hết hạn** · đáp án công bố 07/11: "Trung bình cộng của 4, 8, 6, 5, 7 là **6**."
- Bài tập 3: hạn **13/11/2026 23:59** · **đang mở**.
- Giờ TA: **08:00–22:00**.

**Ba tin mồi (viết thêm, đổi được):**
1. *"Trung vị khác trung bình cộng chỗ nào ạ? Khi nào dùng cái nào?"*
2. *"Cái độ lệch ấy là gì ạ, em đọc không hiểu."*
3. *"Hạn nộp bài 3 là khi nào ạ? Với cả tính độ lệch chuẩn bằng Excel thì dùng hàm gì?"*

### Ba câu Chặng 1 phải trả lời được (ghi vào spec §1)

1. **Ai · việc gì · AI quyết định gì?** Học viên hỏi bài lúc tối muộn; AI chọn: giảng kèm trích tài liệu, hỏi lại, gợi ý từng bước, hay nói thẳng "tài liệu không có".
2. **AI được thêm quyền gì** mà trước đây học viên tự làm? Trước đây học viên tự tra tài liệu, tự viết gợi ý, tự đi hỏi TA. AI được **trả lời thay** (trích tài liệu), **gợi ý bài tập**, **chuyển TA thay**, **đăng FAQ thay**.
3. **Sai thì ai chịu, chịu gì?** Học viên hiểu sai mà tưởng đúng → mang lỗi vào bài và các buổi sau. **Đắt nhất:** đưa/xác nhận đáp số bài đang mở (học viên chép, mất giá trị học) và khẳng định nội dung tài liệu sai là đúng.
4. **Ba việc tính năng KHÔNG làm** (mỗi việc một lý do): ví dụ
   - Không **giải/xác nhận đáp số bài đang mở** → phá mục đích học, học viên chép.
   - Không **dạy trước nội dung buổi chưa học** → dạy ngoài phạm vi tài liệu, dễ bịa.
   - Không **nhận xét năng lực người học** ("em yếu phần này") → gây hại, ngoài thẩm quyền.

**Đủ khi Chặng 1:** cả nhóm nói được lát cắt trong một câu, kiểu sai đắt nhất, tool nào không đảo lại được.

---

## 2. Chặng 2 · Lường trước kịch bản (35' → mốc M1)

Mục tiêu: **≥8 kịch bản** phủ đủ 4 lớp, ghi thẳng vào `spec.md` §2.

**4 lớp phải phủ (1–2–3–4):**
1. **Nguồn sự thật** — AI bịa được ở đâu? Không có căn cứ thì làm gì?
2. **Mơ hồ / thiếu thông tin** — input không đủ chắc: hỏi lại / đoán có báo / từ chối?
3. **Ngoài phạm vi / thẩm quyền** — user đòi thứ không được phép, từ chối sao cho vẫn hữu ích?
4. **Đặc thù domain** — sai cái gì thì học viên học sai mà không biết?

**Format mỗi kịch bản một dòng:**
`tin người dùng | lớp | AI có thể sai thế nào (trỏ tool/dòng dữ liệu) | sản phẩm tốt nên làm gì | nhãn (nhẹ / sửa được / không chấp nhận được)`

**8 kịch bản mẫu, bám sẵn dữ liệu T2 (sửa/dùng được):**

| # | Tin người dùng | Lớp | AI có thể sai thế nào (trỏ cụ thể) | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| 1 | "Slide 12 nói gì ạ?" | 1 nguồn sự thật | Tài liệu buổi 3 **không có slide đánh số**; AI dễ bịa "slide 12" | Nói rõ tài liệu chỉ có mục §3.1–§3.5; hỏi lại đang tìm nội dung nào | sửa được |
| 2 | "Giải hộ em bài tập 3" | 3 thẩm quyền | Gọi `goi_y_bai_tap` quá tay → đưa luôn đáp án bài **đang mở** | Từ chối đưa đáp số, chỉ gợi ý **bước đầu** | không chấp nhận được |
| 3 | "9,10,10,11,12,12,13,45 — trung bình là 15.25 đúng chưa ạ?" | 3 thẩm quyền | Xác nhận đáp số bài đang mở | Không xác nhận; chỉ hỏi lại cách tính ở §3.1 | không chấp nhận được |
| 4 | "Độ lệch chuẩn luôn nhỏ hơn phương sai đúng không ạ?" | 1 nguồn sự thật | Tài liệu §3.3 **có câu sai**; AI dễ khẳng định tài liệu đúng | Nói câu nào cần xem lại + vì sao, bảo báo giảng viên; không khẳng định khi chưa kiểm | không chấp nhận được |
| 5 | "Buổi 4 học gì ạ, có Tableau không?" | 1 nguồn sự thật | Trang khoá học chỉ có tên "4 Trực quan hoá dữ liệu"; AI dễ kể "học biểu đồ cột và Tableau" | Chỉ nói tên buổi 4 từ trang khoá học; tài liệu chưa có | sửa được |
| 6 | "Khi nào dùng trung vị thay trung bình?" | 4 domain | Trả lời chung chung, không trích §3.2 → học viên hiểu sai khái niệm lệch | Giảng kèm trích §3.2, nêu ví dụ thu nhập/giá nhà trong tài liệu | nhẹ |
| 7 | "Hạn bài 3 khi nào ạ?" | 1 nguồn sự thật | Bịa hạn (model tự đoán) | Chỉ lấy hạn từ **trang khoá học**: 13/11/2026 23:59 | sửa được |
| 8 | "11 giờ đêm rồi, hỏi TA được không ạ?" (lớp trưởng lỡ) | 2 mơ hồ | Hứa "đã báo TA" dù `chuyen_TA` chưa gọi / ngoài giờ TA (08:00–22:00) | Nói rõ giờ TA 08:00–22:00, `chuyen_TA` để lại câu hỏi, TA trả lời khi mở | sửa được |
| 9 | "Em học kém phần này quá, chắc em không có năng khiếu" | 4 domain | Nhận xét năng lực học viên | Không nhận xét năng lực; động viên + gợi ý học §3.1–§3.3 từng bước | sửa được |
| 10 | "Tính độ lệch chuẩn bằng Excel hàm gì?" | 4 domain | Trang khoá học chỉ nói "làm bằng bảng tính"; AI dễ bịa hàm/quy trình | Trả lời được nếu có căn cứ, còn không thì nói rõ chưa có trong tài liệu, chuyển TA | nhẹ |

**Tự kiểm:** kịch bản nào làm nhóm **sợ nhất khi demo**? Chưa đáng sợ = chưa đủ.

**Chọn 2 kịch bản đắt nhất** (gợi ý mạnh cho T2: **#2/#3 bài đang mở** và **#4 tài liệu sai**). Ghi lý do vì sao đắt hơn phần còn lại + kịch bản nào *suýt* được chọn và vì sao không.

> **Đủ khi (M1 · cuối chặng 2, ~phút 45):** ≥8 kịch bản phủ 4 lớp · mỗi kịch bản trỏ về tool/dòng dữ liệu · 2 kịch bản đắt nhất được khoanh + lý do.
> **TA sẽ show: ≥8 kịch bản + cột "AI có thể sai thế nào" + 2 kịch bản đắt nhất.**

---

## 3. Chặng 3 · UX khi AI sai (45' — phần chính, R3 = 25 điểm)

Chỉ làm cho **2 kịch bản đắt nhất** bạn đã khoanh. Với mỗi kịch bản, viết đủ 5 thứ:

1. **AI nói gì — nguyên văn** (viết y như trên màn hình sẽ hiện).
2. **Người dùng thấy gì** ngoài câu chữ: độ chắc, bằng chứng AI dựa vào, nút, nhãn.
3. **Người dùng làm gì tiếp:** sửa / bỏ qua / hỏi người / hoàn tác. Không làm gì thì chuyện gì xảy ra?
4. **Ai được báo, sau bao lâu** (TA khi chuyển), người đó thấy gì.
5. **Loại lỗi:** hệ thống / người dùng / **ngữ cảnh** (context error — PAIR) → đổi cách nói và cách sửa.

Với mỗi lựa chọn (hỏi lại / trả lời kèm giới hạn / dừng & chuyển người): ghi **đã loại phương án nào và vì sao**.

**Ví dụ điền sẵn cho 2 kịch bản đắt nhất:**

**Kịch bản "Giải hộ bài tập 3" (bài đang mở):**
- AI nói (nguyên văn): *"Bài tập 3 đang mở (hạn 13/11 23:59) nên mình không đưa đáp số được. Đây là gợi ý bước đầu: với 8 số lương, bước 1 tính trung bình theo công thức ở §3.1; bước 2 sắp xếp và tìm trung vị theo §3.2. Em thử làm rồi mình kiểm cùng em nhé."*
- Người dùng thấy: nhãn "Bài đang mở — chỉ gợi ý" · trích §3.1, §3.2 · nút "Chuyển TA" · không có nút "Xem đáp án".
- Làm gì tiếp: tự làm, hoặc bấm "Chuyển TA".
- Ai được báo: TA (hàng chờ), trong giờ TA.
- Loại lỗi: **thẩm quyền** (AI đáng ra phải từ chối) — sửa bằng **thiết kế** (chặn nút đáp số), không bằng câu chữ.
- Chọn "trả lời kèm giới hạn" + từ chối đưa đáp số. **Đã loại:** "hỏi lại" (vô ích, câu đã rõ) và "dừng hẳn & chuyển người" (chờ lâu, làm được phần gợi ý tại chỗ).

**Kịch bản "tài liệu §3.3 sai" (độ lệch chuẩn luôn nhỏ hơn phương sai):**
- AI nói: *"Mình thấy câu này trong tài liệu §3.3 có chỗ cần xem lại: độ lệch chuẩn là căn bậc hai của phương sai, nên không phải lúc nào cũng nhỏ hơn phương sai (ví dụ phương sai < 1 thì ngược lại). Bạn báo giảng viên để rà lại tài liệu giúp mình nhé."*
- Người dùng thấy: nhãn "Có điểm cần kiểm chứng" · trích §3.3 · nút "Báo giảng viên".
- Ai được báo: giảng viên (báo cáo nội dung).
- Loại lỗi: **ngữ cảnh** (tài liệu sai, hệ thống chạy đúng thiết kế nhưng đúng với dữ liệu sai) → sửa **thiết kế** (quy tắc "nghi tài liệu sai thì nêu, không khẳng định").
- Lỗi **câu chữ không cứu được:** AI nói "tài liệu đúng" — phải sửa thiết kế: **không khẳng định khi chưa kiểm**.

**Chọn 2–3 nguyên tắc HAX/PAIR và trỏ vào CHỖ CỤ THỂ** (sang chặng 5 phải bấm được vào chỗ đó):
- **G2 — Làm rõ nó làm tốt đến đâu** → nhãn "Có điểm cần kiểm chứng" + trích §3.3.
- **G10 — Thu hẹp phạm vi khi nghi ngờ** → với bài đang mở, không đưa đáp số, chỉ hỏi lại/gợi ý.
- **G11 — Giải thích vì sao** → mỗi câu trả lời kèm mã mục §3.x.
- (hoặc **G8/G9 — gạt bỏ / sửa dễ dàng** → nút "Chuyển TA", nút đổi cách hỏi.)

> **Đủ khi:** mỗi kịch bản có câu nguyên văn · cái người dùng thấy · bước tiếp theo · người được báo; mỗi lựa chọn có phương án đã loại + vì sao; 2–3 nguyên tắc trỏ chỗ cụ thể; gọi đúng loại lỗi; 1 lỗi sửa câu chữ không cứu được + thiết kế cứu nó.

---

## 4. Chặng 4 · Mức tự chủ (35' → mốc M2, R4 = 25 điểm)

**Ba mức:** `tự làm` · `cần người duyệt` · `cấm`.

**Cách làm:** mỗi người tự xếp mức cho **mọi tool** trước, không bàn (5'); rồi cả nhóm so và chốt. Chỗ 3 người lệch nhau = **tool khó xếp nhất** → ghi lại ai chọn gì, vì sao, chốt thế nào.

**Gợi ý mức cho T2 (nhóm tự lập luận lại, đây không phải đáp án):**

| Tool | Mức gợi ý | Lý do theo cost-of-error |
|---|---|---|
| `tra_cuu_tai_lieu` | **tự làm** | Chỉ đọc; sai thì học viên tự thấy, tự hỏi lại. |
| `goi_y_bai_tap` | **cần người duyệt** (học viên xác nhận "chỉ gợi ý, không đáp số") **hoặc** tách 2 bước: gợi ý bước đầu = tự làm, **đưa đáp số = cấm** | Sai thì học viên đã chép → gợi ý quá tay không đảo lại. |
| `chuyen_TA` | **tự làm** | Đảo lại được; chờ người để chuyển thì câu hỏi mãi không tới TA. |
| `dang_FAQ` | **cần người duyệt** (TA duyệt trước khi đăng cả lớp) | Gỡ được nhưng nhiều người đã đọc → chờ duyệt rẻ hơn đăng sai cho cả lớp. |

**Với tool "cần người duyệt", trả lời:** ai duyệt · người đó thấy gì trước khi bấm · nếu **không ai duyệt kịp** thì chuyện gì xảy ra.

**Thử mức vừa đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường**, theo 3 câu:
1. Cái sai ở chặng 2 **có bị chặn** không?
2. Có việc nào AI **vẫn làm khi lẽ ra phải hỏi**?
3. Người dùng bình thường có **phải chờ vô ích** không?

**Nói được một mức tự chủ đã đổi lời hứa nào với người dùng:** ví dụ `goi_y_bai_tap` từ "AI tự làm giúp bạn" → "AI soạn gợi ý, bạn bấm xác nhận" → đổi cam kết "không hộp đen, bạn vẫn là người làm bài".

**Nên (điểm tốt):** tách một tool thành 2 bước ("soạn sẵn" tách khỏi "gửi đi") chỉ ra kịch bản nào nhờ đó được chặn.

> **Đủ khi (M2 · cuối chặng 4, ~phút 125):** mọi tool có mức + lý do cost-of-error · chỉ ra tool khó xếp nhất + cách chốt + kịch bản cho cái giá mỗi phía · đã thử mức trên 3 kịch bản · nói được một mức đã đổi lời hứa nào.

---

## 5. Chặng 5 · Prototype (60' → mốc M3, R5 = 25 điểm)

**Ràng buộc:** 1–2 màn hình cho **ca khó nhất**; dữ liệu giả; không đăng nhập, không backend; không cần đẹp. Tùy nhóm: Loveable / v0 / Figma / coding agent / **HTML**.

**Ca khó nhất nên dựng:** một trong hai — **bài đang mở** (từ chối đáp số, chỉ gợi ý + nút chuyển TA) hoặc **tài liệu sai** (nêu điểm cần kiểm chứng). Có thể làm cả hai màn hình: **phía học viên** + **hàng chờ TA**.

**Prototype của T2 phải bấm qua được và thể hiện:**

1. **Độ chắc / bằng chứng:** nhãn độ chắc + **trích mã mục §3.x** ngay trong câu trả lời.
2. **Mức tự chủ hiện trên màn hình đúng như §4:**
   - `tự làm` (`tra_cuu_tai_lieu`, `chuyen_TA`) → có nút **hoàn tác / thu hồi**.
   - `cần người duyệt` (`goi_y_bai_tap`, `dang_FAQ`) → có bước **xác nhận**, người duyệt thấy gì trước khi bấm.
   - `cấm` (đưa đáp số bài đang mở, dạy buổi chưa học) → **không có nút làm**.
   - Luôn có **đường chuyển người** ("Chuyển TA").
3. **Mỗi nguyên tắc HAX/PAIR đã chọn ở Chặng 3 trỏ được vào một chỗ cụ thể** (đánh số ①②③ trên ảnh).
4. **Ca lạ:** prototype đi đường nào khi gặp câu nhóm chưa chuẩn bị (ví dụ hỏi nội dung buổi 7).

**Ảnh nộp kèm:** 1–2 ảnh trong `prototype/`, **đánh số từng chỗ**; mỗi số ghi: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.

**Bonus +3:** cài **≥1 lời gọi AI thật** ở quyết định chính (log hoặc ảnh trong `prototype/`). Nếu làm: **chỉ đưa dữ liệu dựng vào**, **không để API key trong code** (key để biến môi trường). Nhóm có thể xin TA hỗ trợ.

> **Đủ khi (M3 · cuối chặng 5, ~phút 200):** bấm hết ca khó · thấy **≥2 mức tự chủ** khác nhau trên màn hình · mỗi nguyên tắc trỏ được vào một chỗ.

---

## 6. Chặng 6 · Tốt là gì (10' — nhẹ, bỏ được nếu thiếu giờ, R6 = 5 điểm)

Viết **3 tiêu chí Pass/Fail chấm được, không cần tranh luận**, ví dụ (đổi theo nhóm):
1. Mọi câu về nội dung buổi 3 đều kèm **mã mục §3.x** (Pass/Fail).
2. Không có đường nào trên prototype **đưa/xác nhận đáp số bài đang mở** (Pass/Fail).
3. Khi tài liệu nghi sai, trợ lý **nêu điểm cần kiểm chứng + bảo báo giảng viên**, không khẳng định tài liệu đúng (Pass/Fail).

Rồi **chấm thử thiết kế của nhóm trên 2 kịch bản đắt nhất**, ghi **lỗi còn lại**. Chỉ chấm trên những gì có ở Chặng 2–5, không làm thêm.

---

## 7. Demo (30' cuối, R7 = 5 điểm, bonus +5 nếu xung phong)

- Demo **trong zone** cho TA và nhóm cùng bàn, hoặc **xung phong demo trước lớp** (+5 bonus).
- Trong mỗi lượt demo: **lát cắt (30 giây) → bấm prototype qua ca khó → một mức tự chủ + cái giá khi sai → trả lời ca lạ** (do TA/nhóm bạn/giảng viên đưa tại chỗ).
- **Mỗi thành viên trình bày một phần.** Ai cũng phải trả lời được: *"Hành động này sai thì ai mất gì?"* · *"Lỗi nguy hiểm nhất là gì?"* · *"Phần bạn làm là gì?"*
- Ca lạ hay gặp cho T2: *xin đáp số bài đang mở* · *hỏi buổi chưa học* · *nhắc "slide 12"* · *học viên tự chê mình* · *hỏi nội dung buổi 7*.

**Hard tests nên có kịch bản:** xin giải hộ bài đang mở · xin xác nhận đáp số bài đang mở · tài liệu khoá có câu sai · học viên nhắc nguồn không có ("slide 12") · học viên tự chê mình · hỏi nội dung buổi chưa học.

---

## 8. Điền `spec.md` — copy dàn ý, đừng điền kiểu ô trống

1. Copy **toàn bộ khối ```markdown** trong `03-spec-template.md` vào `spec.md` của repo này.
2. Đặt **bảng thành viên ở ĐẦU file** (copy từ `README.md`), điền **tên + mã học viên đúng** + việc mỗi người làm.
3. Điền §1–§7 theo các mục đã làm ở Chặng 1–7 phía trên.
4. **Một quyết định = bốn ý:** đã cân nhắc gì · chọn gì · vì sao · loại gì vì sao. Kèm **bằng chứng trỏ về một chỗ cụ thể** (tool nào, dòng dữ liệu nào, chỗ nào trên prototype). "AI có thể trả lời sai" **không phải** bằng chứng.

---

## 9. Checklist nộp bài (làm trước 23:59 13/11/2026)

- [ ] Repo **mới, công khai**, tên đúng **`K5-L3B-Day05-T2-TamCa`**; mở được bằng cửa sổ ẩn danh.
- [ ] `spec.md` theo `03-spec-template.md`, **bảng thành viên ở đầu**, mã học viên đúng.
- [ ] `prototype/`: file HTML (hoặc link), kèm **1–2 ảnh đánh số** các chỗ.
- [ ] Đã trả lời được: *"Hành động này sai thì ai mất gì?"* · *"Lỗi nguy hiểm nhất là gì?"* · *"Phần bạn làm là gì?"*
- [ ] (Nếu có AI thật) **không có API key trong code**.
- [ ] Push lên GitHub và **dán link repo vào kênh nộp** giảng viên thông báo trong buổi.

---

## 10. Phân công gợi ý cho 3 người (nhóm tự chỉnh)

| Người | Phần chính | Vẫn cùng làm |
|---|---|---|
| A | Chặng 2 (kịch bản) + §2 spec | Chặng 1, 3–4 cùng bàn |
| B | Chặng 3–4 (UX khi sai + mức tự chủ) + §3, §4 | Chặng 2, 5 |
| C | Chặng 5 (prototype) + §5 + ảnh | Chặng 3–4 để biết màn hình thể hiện gì |

Chặng 1–4 **cả nhóm cùng làm** thì tốt hơn. Từ Chặng 5 mỗi người giữ phần mình. **Ai cũng phải giải thích được phần có tên mình** (vibe-coding rule: không giải thích được → 0 điểm phần đó).

---

## 11. Lỗi thường gặp ở T2 — tránh trước

- Viết "AI có thể trả lời sai" thay vì trỏ vào **tool/dòng dữ liệu cụ thể** → mất điểm R2.
- Không nhận ra **§3.3 tài liệu sai** ("độ lệch chuẩn luôn nhỏ hơn phương sai") → bỏ mất kịch bản ngữ cảnh đắt giá.
- Để prototype có nút **xem đáp án** cho bài đang mở → vi phạm R1 (phạm vi) và R5.
- Đặt mức tự chủ "vì tiện"/"vì AI giỏi" → mất 10 điểm R4; phải viết theo **cost-of-error**.
- Không có **đường chuyển người** (TA) hoặc hứa "đã báo TA" khi chưa gọi `chuyen_TA` → lỗi "nói đã làm việc chưa làm".
- Dùng **dữ liệu thật** (bài tập thật, thông tin người thật) → vi phạm luật chung. Chỉ dùng dữ liệu **dựng trong track**.
- Prototype chép giao diện `prototype-sample/` → mẫu đó là T3 Du lịch, chỉ xem để biết "đủ" trông thế nào.

---

## 12. Ba mốc TA đi qua — tự soát trước khi TA tới

| Mốc | Khi nào | Nhóm cần show | Tự tick |
|---|---|---|---|
| **M1 · Kịch bản** | cuối Chặng 2 (~phút 45) | ≥8 kịch bản + cột "AI có thể sai thế nào" + 2 kịch bản đắt nhất | ☐ phủ 4 lớp ☐ trỏ tool/dữ liệu ☐ có lý do chọn 2 |
| **M2 · Mức tự chủ** | cuối Chặng 4 (~phút 125) | Mức cho **mọi** tool + thử trên 3 kịch bản | ☐ lý do cost-of-error ☐ tool khó xếp nhất + cách chốt ☐ đã thử 3 kịch bản |
| **M3 · Bấm được** | cuối Chặng 5 (~phút 200) | Prototype bấm qua ca khó | ☐ bấm hết được ☐ ≥2 mức tự chủ ☐ HAX trỏ vào màn hình |

**Điểm theo rubric:** R1=5 · R2=10 · **R3=25 · R4=25 · R5=25** · R6=5 · R7=5 · bonus +8. **75/100 nằm ở R3–R5** — không bao giờ cắt Chặng 3–4–5.
