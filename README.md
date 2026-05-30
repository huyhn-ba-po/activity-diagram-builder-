# Activity Diagram Builder

Skill cho AI agent hỗ trợ kỹ thuật **Process Modelling** trong BABOK v3 (§10.35):
sinh process model dạng Activity Diagram hoặc User Flow (`.drawio`) thể hiện cách
công việc được thực hiện — participants, trigger, activities, decision points,
flows, result.

Tài liệu viết bằng tiếng Việt, giữ nguyên thuật ngữ BABOK tiếng Anh (process
model, activity, decision point, flow, participant, as-is/to-be, scope…).

## Purpose

Theo BABOK §10.35.1, process modelling là **mô hình đồ hoạ chuẩn hoá thể hiện cách
công việc được thực hiện**, làm nền tảng cho process analysis. Skill tự động hoá
việc dựng model đó từ mô tả luồng nghiệp vụ, thay vì vẽ tay trên draw.io.

## Cách dùng

```text
Bạn: Vẽ activity diagram cho luồng thanh toán đơn hàng có 2 phương thức
     Thẻ và Ví điện tử; phần cổng thanh toán xử lý riêng.
AI:  [xác định participants/trigger/activities/decision → sinh .drawio + legend]
```

Các cụm từ kích hoạt: "vẽ activity diagram", "vẽ sơ đồ hoạt động / process
model", "vẽ user flow", "vẽ luồng nghiệp vụ", "vẽ flow có rẽ nhánh", "xuất drawio".

## Cấu trúc

```text
activity-diagram-builder/
├── SKILL.md     ← kỹ thuật (Purpose / Description / Elements /
│                  Usage Considerations) + quy trình tạo + spec .drawio
└── README.md
```

`SKILL.md` được nạp vào context của agent.

## Cài đặt

Skill agent-agnostic (Claude, Antigravity/Gemini, Codex CLI, Cursor…). Clone repo
về đường dẫn skill của tool, hoặc cho agent đọc `SKILL.md` như context document:

```bash
git clone https://github.com/huyhn-ba-po/activity-diagram-builder-.git
```

## Phạm vi (theo Usage Considerations của BABOK)

Process model thể hiện **sequential flow of work** — phù hợp khi mô tả how work
occurs (as-is/to-be), xử lý nhiều scenario và nhánh song song, làm nổi bật pain
points. BABOK lưu ý: **tách business rules/decisions ra khỏi process** để model
không bị rối, và model high-level không phải lúc nào cũng đủ để thấy hết vấn đề.
Để thể hiện tương tác giữa các object theo thời gian, dùng Sequence Diagrams
(mermaid-sequence-diagram); để đặc tả giao diện, dùng screen-description-writer.
