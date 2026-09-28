# AI Agent Prompt Patterns (Tiếng Việt)

[English](README.md) · Bản đầy đủ và cập nhật nhất là bản tiếng Anh.

12 pattern thiết kế system prompt cho coding agent, rút ra từ việc đọc đối chiếu prompt của
Cursor, Claude Code và Devin, kèm một template để tự viết prompt.

## Đây là gì
Mỗi pattern gồm: mô tả ngắn, **bằng chứng** (vị trí dòng trong prompt nguồn), lý do nó hiệu quả,
cách áp dụng, và một **anti-pattern** nên tránh.

## Đây không phải là
- **Không phải bản chép prompt.** Tất cả được viết lại bằng lời của mình.
- **Không phải tài liệu chính thức.** Prompt nguồn do cộng đồng trích xuất, nhà sản xuất chưa xác nhận.
- **Chưa đo lường.** Phần "lý do hiệu quả" là lập luận, không phải kết quả benchmark.

## Danh sách pattern
| # | Pattern | Nhóm |
|---|---|---|
| 01 | [Luật tool theo từng tình huống](patterns/01-situational-tool-rules.md) | Dùng tool |
| 02 | [Ghi rõ khi nào KHÔNG dùng tool](patterns/02-when-not-to-use.md) | Dùng tool |
| 03 | [Gộp các lệnh độc lập](patterns/03-parallel-independent-calls.md) | Dùng tool |
| 04 | [Tự tìm trước khi hỏi](patterns/04-search-before-asking.md) | Ngữ cảnh & kế hoạch |
| 05 | [Phân biệt câu hỏi và yêu cầu](patterns/05-questions-vs-requests.md) | Ngữ cảnh & kế hoạch |
| 06 | [Tách chế độ lập kế hoạch và thực thi](patterns/06-planning-and-execution-modes.md) | Ngữ cảnh & kế hoạch |
| 07 | [Kiểm tra trạng thái trước khi làm](patterns/07-verify-state-before-acting.md) | Ngữ cảnh & kế hoạch |
| 08 | [Bắt buộc suy nghĩ tại điểm quyết định](patterns/08-think-at-decision-points.md) | Kiểm chứng & sửa lỗi |
| 09 | [Giới hạn số lần tự sửa lỗi](patterns/09-bounded-self-repair.md) | Kiểm chứng & sửa lỗi |
| 10 | [Không sửa test để test pass](patterns/10-never-edit-tests-to-pass.md) | Kiểm chứng & sửa lỗi |
| 11 | [Chính xác hơn chiều lòng](patterns/11-accuracy-over-agreement.md) | Hành vi |
| 12 | [Dạy hành vi bằng ví dụ](patterns/12-teach-by-example.md) | Hành vi |

Xem thêm: [so sánh 3 agent](docs/comparison.md) · [template prompt 10 phần](templates/prompt-framework.md)

## Nguồn & giới hạn
Nguồn: repo cộng đồng [`x1xhlol/system-prompts-and-models-of-ai-tools`](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)
(GPL-3.0), snapshot commit `1e4203a` ngày 2026-08-11. Mọi pattern có trạng thái `OBSERVED`: hành vi
có xuất hiện trong văn bản prompt trích xuất, nhưng chưa được kiểm chứng trên sản phẩm thật.

## Giấy phép
[MIT](LICENSE) cho phần phân tích và template. Prompt gốc thuộc về chủ sở hữu tương ứng và không có trong repo này.
