# Bài 5: Áp dụng AI Policy & Nguyên tắc Human-in-the-loop trong Đánh giá Nhân sự

## Phần giải thích kiến thức

**Human-in-the-loop (HITL)** là nguyên tắc: trong mọi quy trình có AI tham gia, **con người phải nằm trong vòng lặp**, tức là kiểm tra, thẩm định và chịu trách nhiệm cuối cùng cho quyết định, nhất là quyết định ảnh hưởng trực tiếp đến quyền lợi của con người (sa thải, tuyển dụng, vay vốn, y tế...).

**Decision Support (hỗ trợ ra quyết định):** AI chỉ là *trợ lý đề xuất*. Nó phân tích dữ liệu và gợi ý, còn **quyết định thuộc về con người**.

| | AI | Con người |
|---|---|---|
| Vai trò | Trợ lý phân tích, đề xuất | Người thẩm định và ra quyết định |
| Tư cách pháp lý | Không có | Có, chịu trách nhiệm giải trình |
| Hiểu bối cảnh thực tế | Hạn chế (chỉ thấy dữ liệu được đưa vào) | Có thể xác minh, đối thoại, cân nhắc hoàn cảnh |

**Rủi ro khi tự động hóa quyết định nhân sự:**

- **Định kiến (Bias):** AI học từ dữ liệu, nếu dữ liệu lệch hoặc thiếu bối cảnh thì kết quả cũng lệch.
- **Thiếu bối cảnh:** KPI và chấm công không phản ánh hết lý do (ốm đau, nghỉ thai sản, đổi vị trí, vai trò hỗ trợ khó đo bằng số...).
- **Ảo giác / sai sót:** AI có thể xử lý sai số liệu mà vẫn trình bày rất tự tin.
- **Trách nhiệm pháp lý:** quyết định sa thải phải đúng căn cứ và đúng quy trình theo quy định pháp luật lao động; AI không thể đứng ra chịu trách nhiệm.

---

## Phần 1: Phân tích 2 vi phạm nghiêm trọng của Trưởng phòng Nhân sự

### Vi phạm 1: Vi phạm nguyên tắc Human-in-the-loop (giao quyết định cho AI, không thẩm định)

- **Hành động sai:** Trưởng phòng yêu cầu AI "lập danh sách 3 nhân viên kém nhất để sa thải *ngay lập tức*", nhận 3 cái tên rồi **ký quyết định ngay mà không kiểm tra lại**.
- **Vì sao vi phạm:** AI chỉ là công cụ **Decision Support**, không có thẩm quyền pháp lý hay tư cách chủ thể để quyết định sa thải. Việc ký thẳng kết quả AI nghĩa là con người đã **bị loại khỏi vòng lặp**, biến AI thành người ra quyết định thật sự.
- **Hậu quả:** quyết định có thể dựa trên dữ liệu thiếu, sai hoặc lệch; không có bước xác minh, không có đối thoại với nhân viên, không đúng quy trình.

### Vi phạm 2: Đổ trách nhiệm cho AI và ngụy biện "AI khách quan nên công bằng"

- **Hành động sai:** Khi bị khiếu nại, Trưởng phòng nói *"Do AI phân tích khách quan từ số liệu, tôi không can thiệp nên hoàn toàn công bằng!"*
- **Vì sao vi phạm đạo đức nghề nghiệp:**
  1. **AI không mặc định khách quan.** Nó có thể mang **Bias** từ dữ liệu: KPI và chấm công không phản ánh các yếu tố như nghỉ ốm hợp lệ, nghỉ thai sản, vị trí khó đo KPI, hoàn cảnh đặc biệt. Kết quả "dựa trên số liệu" vẫn có thể bất công.
  2. **Không can thiệp không đồng nghĩa với công bằng.** Việc "không can thiệp" chính là vi phạm: người ra quyết định có nghĩa vụ kiểm chứng.
  3. **Trách nhiệm giải trình thuộc về con người.** AI không thể bị khiếu nại hay chịu trách nhiệm pháp lý, nên Trưởng phòng là người chịu trách nhiệm cuối cùng, không thể đổ cho AI.

### Lưu ý bổ sung (điểm cộng)

- **Câu lệnh (prompt) mang tính áp đặt kết quả:** "sa thải ngay lập tức" ép AI trả về đúng 3 tên bất kể dữ liệu có đủ căn cứ hay không.
- **Dữ liệu nhân sự là dữ liệu nhạy cảm:** cần tuân thủ chính sách bảo mật của công ty khi đưa vào công cụ AI (ẩn danh hóa, dùng công cụ nội bộ được phê duyệt).

---

## Phần 2: Sơ đồ quy trình phối hợp Human-in-the-loop cho MartX

### Sơ đồ luồng

```
┌───────────────────────────────┐
│ BƯỚC 1: NHẬP DỮ LIỆU          │  (Con người)
│ - Thu thập KPI, chấm công     │
│ - Làm sạch, ẩn danh hóa       │
│ - Bổ sung bối cảnh (nghỉ phép,│
│   thai sản, đổi vị trí...)    │
│ - Prompt trung lập            │
└──────────────┬────────────────┘
               ▼
┌───────────────────────────────┐
│ BƯỚC 2: AI ĐỀ XUẤT            │  (AI - Decision Support)
│ - Phân tích dữ liệu           │
│ - Đưa ra danh sách cần xem xét│
│   kèm lý do, số liệu dẫn chứng│
│ - KHÔNG đưa quyết định cuối   │
└──────────────┬────────────────┘
               ▼
┌───────────────────────────────┐
│ BƯỚC 3: HUMAN-IN-THE-LOOP     │  (Con người)
│        THẨM ĐỊNH              │
│ - Đối chiếu số liệu gốc       │
│ - Xem xét bối cảnh, kiểm tra  │
│   Bias                        │
│ - Trao đổi với quản lý trực   │
│   tiếp, lắng nghe nhân viên   │
│ - Đối chiếu quy chế, pháp luật│
└──────────────┬────────────────┘
               ▼
        ┌──────────────┐
        │ Đủ căn cứ ?  │
        └───┬──────┬───┘
         Không    Có
            │      │
   Quay về  │      ▼
   Bước 1   │  ┌───────────────────────────────┐
  (bổ sung  │  │ KÝ QUYẾT ĐỊNH                 │  (Người có thẩm quyền)
   dữ liệu) │  │ - Con người chịu trách nhiệm  │
            │  │ - Lưu hồ sơ căn cứ, lý do     │
            │  │ - Thông báo, cho quyền phản hồi│
            └──┴───────────────────────────────┘
```

### Bảng mô tả chi tiết từng bước

| Bước | Tên bước | Ai thực hiện | Nội dung chính | Đầu ra |
|---|---|---|---|---|
| 1 | Nhập dữ liệu | Con người (HR) | Thu thập KPI, chấm công; làm sạch dữ liệu; ẩn danh hóa; ghi chú bối cảnh (nghỉ hợp lệ, vị trí đặc thù); viết prompt trung lập | Bộ dữ liệu sạch và đủ bối cảnh |
| 2 | AI đề xuất | AI | Phân tích, xếp hạng, nêu lý do và số liệu dẫn chứng; chỉ gợi ý "cần xem xét" | Bản đề xuất tham khảo |
| 3 | Human-in-the-loop thẩm định | Con người (HR + quản lý trực tiếp) | Đối chiếu dữ liệu gốc, kiểm tra Bias, xem xét bối cảnh, trao đổi với nhân viên, đối chiếu quy chế | Kết luận đủ hay chưa đủ căn cứ |
| 4 | Ký quyết định | Người có thẩm quyền | Ra quyết định, lưu hồ sơ căn cứ, thông báo và cho quyền phản hồi | Quyết định có người chịu trách nhiệm |

### Prompt chuẩn thay cho câu lệnh sai

```
Dựa trên dữ liệu KPI và chấm công (đã ẩn danh) của 50 nhân viên dưới đây,
hãy phân tích và nêu các trường hợp có hiệu suất thấp cần được xem xét.
Với mỗi trường hợp, nêu rõ số liệu dẫn chứng và những yếu tố bối cảnh
có thể làm sai lệch kết quả (nghỉ phép, vị trí khó đo KPI, thiếu dữ liệu).
Đây chỉ là đề xuất tham khảo để con người thẩm định, không phải kết luận
cuối cùng, và không đưa ra quyết định sa thải.
```

### Quy tắc an toàn cho MartX (AI Policy rút gọn)

1. AI **chỉ đề xuất**, không ra quyết định về con người.
2. Mọi quyết định nhân sự phải qua **thẩm định của con người** và có **người ký chịu trách nhiệm**.
3. Dữ liệu đưa vào AI phải được **ẩn danh hóa** và dùng công cụ được công ty phê duyệt.
4. Kết quả AI phải **kiểm chứng với số liệu gốc**, kiểm tra Bias trước khi dùng.
5. Nhân viên có **quyền được giải trình và phản hồi** trước khi quyết định có hiệu lực.
6. **Lưu vết** toàn bộ quy trình (dữ liệu, đề xuất AI, kết quả thẩm định) để phục vụ giải trình khi khiếu nại.

---

## Tóm tắt nộp bài

- **Phần 1:** Trưởng phòng vi phạm (1) nguyên tắc **Human-in-the-loop**: ký quyết định sa thải theo AI mà không thẩm định; (2) đạo đức nghề nghiệp: **đổ trách nhiệm cho AI** và ngụy biện "AI khách quan nên công bằng", bỏ qua **Bias** và nghĩa vụ giải trình.
- **Phần 2:** Quy trình **Nhập dữ liệu → AI đề xuất → Human-in-the-loop thẩm định → Ký quyết định**, trong đó AI chỉ đóng vai trò **Decision Support**, con người thẩm định và chịu trách nhiệm cuối cùng.
