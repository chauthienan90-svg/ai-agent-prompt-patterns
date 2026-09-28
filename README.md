# AI Agent Prompt Patterns

Tổng hợp **pattern thiết kế agent** rút từ 3 họ prompt coding-agent: Cursor Agent Prompt 2.0, Claude Code 2.0, Devin.

Repo này **không chép nguyên văn** prompt gốc — chỉ diễn đạt lại pattern thành khung thiết kế dùng được.

## Phát hiện chính
1. Phần hành vi chỉ ~20–30% prompt; phần lớn là mô tả tool và luật dùng tool.
2. Mô tả tool phải có cả "khi dùng" và **"khi KHÔNG dùng"**.
3. Cần verification gate: tự kiểm trước khi báo hoàn thành.
4. Vòng tự sửa lỗi phải có giới hạn số lần.
5. Tách chế độ planning và execute giúp agent ổn định hơn.
6. Guardrail an toàn là bắt buộc.

## Nội dung
- `agent-prompt-patterns.md` — 10 pattern + so sánh 3 agent + khung prompt 10 phần
- `prompt-framework-template.md` — template điền sẵn để viết prompt/skill mới

## Nguồn & giấy phép
Nguồn tham khảo: repo cộng đồng `x1xhlol/system-prompts-and-models-of-ai-tools` (GPL-3.0), gồm prompt do cộng đồng trích xuất, **không phải tài liệu chính thức**. Repo này chỉ chứa phân tích viết lại, dùng cho mục đích học tập và tham khảo thiết kế.
