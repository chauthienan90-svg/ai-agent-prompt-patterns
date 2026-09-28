# Pattern thiết kế Agent — rút từ Cursor, Claude Code, Devin

**Nguồn:** repo `x1xhlol/system-prompts-and-models-of-ai-tools` (GPL-3.0)
**File đã phân tích:**
- `Cursor Prompts/Agent Prompt 2.0.txt` (~39 KB)
- `Anthropic/Claude Code 2.0.txt` (~57 KB)
- `Devin AI/Prompt.txt` (~35 KB)

**Lưu ý nguồn gốc:** Đây là prompt do cộng đồng trích xuất, không phải tài liệu chính thức, nên có thể đã cũ hoặc không đầy đủ. Mọi nhận định trong file này đều thuộc loại **CLAIM**. File chỉ ghi lại **pattern**, diễn đạt lại bằng lời của mình, không chép nguyên văn.

---

## 1. Bức tranh chung: cả 3 đều có cùng một khung

| Khối | Cursor | Claude Code | Devin |
|---|---|---|---|
| Danh tính và vai trò | Rất ngắn | Ngắn | Dài, nhấn mạnh năng lực |
| Giao tiếp và giọng văn | `<communication>` | Tone & style + nhiều ví dụ | "When to Communicate" |
| Quy tắc gọi tool | `<tool_calling>` gồm 9 luật | Tool usage policy | Command Reference |
| Thu thập ngữ cảnh | `<maximize_context_understanding>` | Doing tasks | Planning mode |
| Quy tắc sửa code | `<making_code_changes>` | Edit tool + Code References | Coding Best Practices |
| Quản lý task | `todo_write` | `TodoWrite` | `suggest_plan` |
| An toàn và bảo mật | Ít | Defensive security | Data Security |
| Định nghĩa tool (schema) | JSON riêng | Trong prompt, rất chi tiết | Dạng XML command |

**Nhận xét:** Phần hành vi (behavior) chỉ chiếm khoảng 20–30% dung lượng. Phần lớn là **định nghĩa tool cùng hướng dẫn dùng từng tool**. Chất lượng của agent nằm ở mô tả tool nhiều hơn ở đoạn "You are...".

---

## 2. Mười pattern đáng học

### P1. Luật tool viết dạng danh sách đánh số và có lý do
Cursor liệt kê 9 luật gọi tool, mỗi luật chỉ xử lý một tình huống: tool không còn tồn tại, sửa file thất bại, không chắc về nội dung file...
→ **Áp dụng:** Tách các rule R01, R06, R11 của bạn theo từng tình huống lỗi cụ thể, tránh viết rule chung chung.

### P2. Tự tìm trước, chỉ hỏi khi thật sự cần
Cả 3 đều ưu tiên dùng tool để tự lấy thông tin hơn là hỏi người dùng. Chỉ hỏi khi thiếu thông tin không thể tự tìm, cần quyền hoặc key, hoặc có nhiều phương án cần người chọn.
→ **Áp dụng:** Khớp với nguyên tắc "Action over discussion" của bạn. Nên đưa thành rule trong Router.

### P3. Lập kế hoạch xong thì làm luôn
Cursor: khi đã có plan thì thực hiện ngay, không chờ xác nhận. Ngoại lệ là thiếu thông tin hoặc cần người chọn phương án.
Claude Code thận trọng hơn: nếu người dùng hỏi "nên làm thế nào" thì trả lời trước, chưa hành động.
→ **Áp dụng:** Phân biệt rõ **câu hỏi** (trả lời) và **yêu cầu** (làm). Đây là một nhánh quyết định cho Router.

### P4. Hai chế độ: Planning và Standard (Devin)
- **Planning:** chỉ thu thập thông tin, xác định mọi vị trí cần sửa, rồi đề xuất plan.
- **Standard:** thực thi theo plan đã duyệt.
→ **Áp dụng:** Tương ứng với Bước 1–3 và Bước 4 trong Operating Model của bạn. Có thể biến thành trạng thái `mode` trong Master State.

### P5. Bắt buộc suy nghĩ tại các điểm quyết định (Devin)
Devin buộc phải dùng `<think>` ở 3 thời điểm: trước quyết định quan trọng về git, khi chuyển từ tìm hiểu sang sửa code, và **trước khi báo hoàn thành**.
→ **Áp dụng:** Đây chính là **Verification Gate**. Thêm checkpoint "tự kiểm trước khi báo DONE" vào quy trình Evidence/DoD.

### P6. Giới hạn số vòng tự sửa lỗi
Cursor: sửa lỗi linter trên cùng một file tối đa 3 lần. Đến lần thứ 3 thì dừng và hỏi người dùng.
→ **Áp dụng:** Self-Repair Loop của Autonomous AI Brain cần một `max_retries` rõ ràng, sau đó chuyển trạng thái BLOCKED rồi mới hỏi người.

### P7. Không sửa test để cho test pass (Devin)
Khi test fail, giả định lỗi nằm ở code chứ không phải ở test. Chỉ sửa test khi nhiệm vụ yêu cầu.
→ **Áp dụng:** Thành một rule cho Verification: không được thay đổi tiêu chí kiểm tra để "đạt".

### P8. Đọc lại trước khi sửa, và không giả định thư viện có sẵn
- Sửa file thất bại thì phải đọc lại file, vì có thể người dùng vừa sửa (Cursor).
- Không tự cho rằng một thư viện đã có sẵn. Phải kiểm tra file dependency trước (Devin).
→ **Áp dụng:** Đây là FACT-check ở tầng Tool: xác minh trạng thái trước khi hành động.

### P9. Khách quan hơn chiều lòng (Claude Code)
Ưu tiên độ chính xác kỹ thuật hơn việc đồng ý với người dùng. Khi chưa chắc, phải điều tra trước rồi mới xác nhận.
→ **Áp dụng:** Khớp với cách phân loại FACT/ASSUMPTION của bạn. Nên có trong phần "Nguyên tắc" của mọi skill.

### P10. Chạy song song các lệnh độc lập
Cả Claude Code và Devin đều yêu cầu gộp các lệnh không phụ thuộc nhau vào cùng một lượt để tiết kiệm thời gian.
→ **Áp dụng:** Workflow engine nên đánh dấu các bước `independent` để chạy song song.

---

## 3. Khác biệt đáng chú ý

| Chủ đề | Cursor | Claude Code | Devin |
|---|---|---|---|
| Mức chủ động | Rất cao: làm luôn | Cân bằng: không gây bất ngờ | Theo mode |
| Độ dài câu trả lời | Bình thường | **Rất ngắn** (giao diện CLI) | Chỉ báo khi cần |
| Commit git | Không nói rõ | **Chỉ commit khi được yêu cầu** | Theo plan |
| Lộ prompt | Không nói rõ | Không nói rõ | Có câu trả lời cố định khi bị hỏi |
| Cách dùng ví dụ | Ít | **Rất nhiều `<example>`** | Ít |

**Bài học:** Claude Code dạy hành vi chủ yếu bằng **ví dụ** chứ không chỉ bằng luật. Với những hành vi khó mô tả, như độ dài hay giọng văn, 2–3 ví dụ hiệu quả hơn 10 dòng luật.

---

## 4. Khung prompt tổng hợp (áp dụng cho skill của bạn)

```
[1] VAI TRÒ — 1–2 câu: là ai, làm việc gì, cho ai
[2] GIAO TIẾP — ngôn ngữ, độ dài, định dạng, khi nào báo cho người dùng
[3] CHẾ ĐỘ — planning | execute; điều kiện chuyển chế độ
[4] LUẬT TOOL — danh sách đánh số, mỗi luật một tình huống
[5] THU THẬP NGỮ CẢNH — tự tìm trước; khi nào mới được hỏi
[6] THỰC THI — quy tắc sửa/tạo; giới hạn số lần retry
[7] VERIFICATION GATE — tự kiểm trước khi báo DONE; không sửa tiêu chí kiểm tra
[8] AN TOÀN — dữ liệu nhạy cảm, secret, hành động không thể hoàn tác cần xác nhận
[9] VÍ DỤ — 2–3 cặp input → output mẫu cho hành vi khó mô tả
[10] TOOL SCHEMA — tên, mục đích, khi dùng / khi KHÔNG dùng, tham số
```

**Điểm then chốt:** Ở mục [10], mỗi tool nên có cả dòng **"khi KHÔNG dùng"**. Cả Claude Code và Devin đều làm vậy, ví dụ: không dùng shell để đọc hay sửa file mà phải dùng tool chuyên dụng.

---

## 5. Việc tiếp theo có thể làm

| Việc | Ưu tiên | Đầu ra |
|---|---|---|
| Đối chiếu khung ở mục 4 với prompt-execution-system hiện tại | P0 | Danh sách phần còn thiếu |
| Thêm P5 (gate trước khi DONE) và P6 (max_retries) vào Autonomous AI Brain | P1 | Rule mới |
| Phân tích thêm Windsurf và Kiro (có spec-driven workflow) | P2 | Mở rộng file này |
| Góc nội dung: "3 AI coding agent được lập trình thế nào" | P2 | Kịch bản video 7 phần |

---

**English vocab:**
- Tool schema = Mô tả cấu trúc tham số của công cụ
- Scratchpad = Vùng nháp để suy nghĩ
- Checkpoint = Điểm kiểm tra
- Retry limit = Giới hạn số lần thử lại
- Proactiveness = Mức độ chủ động
- Idiomatic = Đúng phong cách, thông lệ của ngôn ngữ hoặc dự án
