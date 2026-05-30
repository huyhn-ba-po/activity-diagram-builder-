---
name: activity-diagram-builder
description: |
  Hiện thực kỹ thuật Process Modelling (BABOK v3 §10.35): sinh process model dạng
  Activity Diagram hoặc User Flow (.drawio) thể hiện flow tuần tự của công việc —
  participants, trigger event, activities, decision points, flows, result — phân
  ranh giới hệ thống bằng scope container, xuất file chỉnh sửa được. Dùng khi user
  nói "vẽ activity diagram", "vẽ sơ đồ hoạt động", "vẽ process model", "vẽ user
  flow", "vẽ luồng nghiệp vụ", "vẽ flow có rẽ nhánh", "vẽ sơ đồ cho Confluence",
  "xuất drawio", kể cả nói tắt "vẽ activity đi", "làm cái flow đi".
  KHÔNG dùng cho: sequence diagram (dùng mermaid-sequence-diagram), ERD, class
  diagram, gantt chart, mô tả màn hình UI (dùng screen-description-writer).
---

# Activity Diagram Builder

Skill này hiện thực kỹ thuật **Process Modelling** trong BABOK v3 (§10.35). Các
element, level và phạm vi áp dụng bám theo định nghĩa của kỹ thuật. Thuật ngữ kỹ
thuật giữ nguyên tiếng Anh theo BABOK.

## Purpose (Mục đích)

> *"Process modelling is a standardized graphical model used to show how work is
> carried out and is a foundation for process analysis."* — BABOK v3, §10.35.1

Skill sinh một **process model** (dạng activity diagram / user flow, định dạng
`.drawio`) thể hiện cách công việc được thực hiện, làm nền tảng cho process
analysis.

## Description (Mô tả)

Theo BABOK §10.35.2:

- Process model mô tả **sequential flow of work/activities**. Một *business
  process model* mô tả luồng công việc qua các task/activity trong (một phần)
  doanh nghiệp.
- Model có thể dựng ở nhiều **level**: context/enterprise (tổng quan, quan hệ với
  process khác) → operational (chi tiết activity, exception, alternative path) →
  system (làm cơ sở mô phỏng/thực thi).
- Phân biệt **as-is** (current state — điều gì đang xảy ra) và **to-be** (future
  state — điều mong muốn xảy ra).
- Một process model nói chung gồm: **participants**, **business event** kích hoạt
  process, các **steps/activities** (cả manual và automated), các **paths
  (flows)** và **decision points** nối các activity, và **results** của process.
- Process model cơ bản nhất gồm: *trigger event + sequence of activities +
  result*. Model đầy đủ hơn có thể thêm data/materials, inputs/outputs và
  call-out descriptions.

Skill hỗ trợ 2 dạng output của process model:

| Dạng | Mô tả | Khi nào dùng |
|---|---|---|
| **Activity Diagram** | Process model nghiệp vụ end-to-end, nhiều participant/hệ thống, có scope container | Mô tả how work occurs cho BA/PO/stakeholder |
| **User Flow** | Process model ở mức màn hình, tập trung điều end-user thấy | Hành trình người dùng qua từng màn hình, nhánh lỗi gọn |

## Elements (Các thành phần)

### Notation (BABOK §10.35.3 .1)

BABOK liệt kê nhiều notation: Flowcharts & Value Stream Mapping (business);
Data Flow & UML activity diagram (IT); **BPMN** (cả hai domain, industry
standard); IDEF/IGOE (scope); SIPOC. Skill xuất `.drawio` dạng activity
flowchart có màu (BPMN-lite) — đủ trực quan cho stakeholder nghiệp vụ.

### Ánh xạ element của process model → shape .drawio

| Element (BABOK) | Ý nghĩa | Shape .drawio |
|---|---|---|
| **Participant / Role** | Bên thực hiện activity (người/hệ thống) | Scope container (nét đứt) + màu |
| **Trigger** (business event) | Sự kiện khởi đầu process | Start node (`ellipse fill #333`) |
| **Activity / Step** | Bước công việc (manual hoặc automated) | Rounded rectangle |
| **Flow (path)** | Đường nối thể hiện thứ tự | Orthogonal edge |
| **Decision point** | Điểm rẽ nhánh theo điều kiện | Diamond (`rhombus`), edge có label điều kiện |
| **Merge** | Hội tụ các nhánh | Diamond nhỏ đặc |
| **Result / End** | Kết quả của process | End node (2 ellipse lồng nhau) |
| **Call-out / data** | Bổ sung text/dữ liệu | Label / Legend |

### Bảng màu theo ý nghĩa (giúp "process visualization" — highlight pain points)

| Mục đích | Fill | Stroke |
|---|---|---|
| Bước chung / neutral | #f5f5f5 | #999999 |
| Decision | #fff2cc | #d6b656 |
| Nhánh 1 (chính) | #d5e8d4 | #82b366 |
| Nhánh 2 (phụ) | #FAECE7 | #D85A30 |
| Hệ thống kiểm tra / server | #E8E6FC | #7F77DD |
| App xử lý | #E1F5EE | #1D9E75 |
| Hệ thống ngoài (3rd party) | #dae8fc | #6c8ebf |
| Lỗi / thông báo lỗi | #f8cecc | #b85450 |

## Quy trình tạo

1. **Chọn dạng & state** — Activity Diagram hay User Flow; as-is hay to-be (hỏi
   nếu chưa rõ; nếu user đã nói rõ thì làm luôn).
2. **Thu thập element** (theo "process models generally include"): participants,
   trigger event, activities (manual/automated), decision points + điều kiện,
   flows, result, và ranh giới hệ thống cần khoanh vùng (scope).
3. **Thiết kế layout** — trục dọc là chính (top → bottom); rẽ nhánh trải ngang từ
   decision; merge trước khi vào phần chung; scope container (`dashed`) bao nhóm
   activity thuộc cùng một participant/hệ thống.
4. **Sinh `.drawio`** — shapes + màu theo ý nghĩa; tất cả edge `orthogonal`; mỗi
   shape có `vertex="1" parent="1"`, edge có `edge="1" parent="1"`, dùng `html=1`.
5. **Legend** — luôn thêm chú thích màu ở cuối.
6. **Xuất file** tại `/mnt/user-data/outputs/<tên-process>-activity.drawio` (hoặc
   `-user-flow`), import được vào draw.io / Confluence.

### Khung XML .drawio

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="app.diagrams.net">
  <diagram id="[id]" name="[Tên process]">
    <mxGraphModel dx="1422" dy="[height]" grid="1" gridSize="10"
      page="1" pageScale="1" pageWidth="[width]" pageHeight="[height]">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>
        <!-- shapes + edges -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Usage Considerations

Theo BABOK §10.35.4:

### Strengths
- Phù hợp với hiểu biết tự nhiên của con người về **sequential activities**; đa
  số stakeholder thoải mái với khái niệm và element của process model.
- Dùng nhiều **level** để đáp ứng các perspective khác nhau của các nhóm stakeholder.
- Hiệu quả khi thể hiện nhiều scenario và **parallel branches**.
- Giúp phát hiện stakeholder group bị bỏ sót.
- Hỗ trợ nhận diện cơ hội cải tiến bằng cách làm nổi bật **"pain points"**
  (process visualization).
- Có giá trị tự thân: tài liệu cho compliance, training; baseline cho cải tiến
  liên tục; nhất quán nhãn; minh bạch trách nhiệm, thứ tự, hand-over.

### Limitations
- Với nhiều người trong IT, process model formal bị xem là cách tiếp cận
  **document-heavy** kiểu cũ → dễ không được cấp thời gian.
- Có thể trở nên **phức tạp/rối** nếu không cấu trúc cẩn thận — đặc biệt khi
  **business rules và decisions không được tách riêng khỏi process**.
- Process phức tạp nhiều activity/role → gần như không thể để một cá nhân hiểu
  hết và "sign off".
- Vấn đề trong process không phải lúc nào cũng thấy ở model high-level → cần
  model chi tiết hơn kèm metadata (tần suất, chi phí, thời gian).
- Môi trường biến động nhanh → model dễ **lỗi thời**; khó maintain nếu chỉ đóng
  vai trò tài liệu.

## Ràng buộc khi sinh diagram

- **Tách business rules khỏi flow** (theo limitation của BABOK): trong activity
  chỉ ghi bước/decision; điều kiện chi tiết tham chiếu rule ID, không nhồi vào ô.
- Tất cả edge dùng `edgeStyle=orthogonalEdgeStyle`; luôn có Legend.
- ≤ 15 activity trên một nhánh; vượt thì tách diagram hoặc gộp bước nhỏ.
- 2 nhánh cách nhau ≥ 100px; >2 nhánh thì mở rộng pageWidth (~300px/nhánh).
- Không trộn Activity Diagram và User Flow trong cùng một file.
