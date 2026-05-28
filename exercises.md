# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature tăng từ 0.0 lên 1.5, các phản hồi chuyển từ tính xác định và có cấu trúc chặt chẽ (0.0 và 0.5) sang tính sáng tạo, đa dạng từ ngữ hơn (1.0), và cuối cùng là mất kiểm soát, lặp từ hoặc phi logic (1.5). Ở mức 0.0, câu trả lời luôn cố định và dễ đoán, trong khi mức 1.5 tạo ra văn bản rời rạc và lỗi cú pháp do mô hình chọn các token có xác suất rất thấp.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature từ 0.0 đến 0.2. Trong hỗ trợ khách hàng, sự chính xác, nhất quán và độ tin cậy của thông tin là quan trọng nhất; đặt mức thấp giúp giảm thiểu tối đa hiện tượng "ảo tưởng" (hallucination) và đảm bảo chatbot luôn đưa ra câu trả lời chuẩn xác dựa trên tài liệu nghiệp vụ.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Dựa trên bảng giá PRICING_1M_TOKENS: GPT-4o có giá đầu vào là $5.00/1M tokens và đầu ra là $20.00/1M tokens, trong khi GPT-4o-mini là $0.150/1M tokens đầu vào và $0.600/1M tokens đầu ra. Tỉ lệ chênh lệch giá cho cả đầu vào và đầu ra đều là đúng 33.33 lần (5.00 / 0.150 = 33.33 và 20.00 / 0.600 = 33.33). Do đó, GPT-4o đắt hơn GPT-4o-mini đúng **33.33 lần** cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> - **GPT-4o xứng đáng**: Khi cần giải quyết các bài toán yêu cầu khả năng lập luận phức tạp (complex reasoning), phân tích tài chính/pháp lý chuyên sâu, hoặc sinh mã nguồn phức tạp nơi độ chính xác cực cao là bắt buộc và sai lệch nhỏ có thể gây thiệt hại lớn.
> - **GPT-4o-mini tốt hơn**: Khi xây dựng các tính năng xử lý số lượng lớn tác vụ đơn giản (high volume, low complexity) như phân loại ý định (intent routing), trích xuất thông tin có cấu trúc (entity extraction), hoặc chatbot đàm thoại cơ bản để tối ưu hóa chi phí vận hành.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming cực kỳ quan trọng đối với các ứng dụng trò chuyện trực tiếp (chatbot, trợ lý ảo) có phản hồi dài, giúp hiển thị kết quả ngay lập tức dưới dạng ký tự chạy để giảm "thời gian chờ đợi cảm nhận" (perceived latency) của người dùng. Ngược lại, non-streaming phù hợp hơn cho các tác vụ xử lý ngầm (background jobs), các cuộc gọi API từ hệ thống đến hệ thống (backend-to-backend integrations), các yêu cầu trích xuất dữ liệu có cấu trúc chặt chẽ (như JSON) cần được xác thực đầy đủ trước khi xử lý tiếp, hoặc khi nội dung cần phải qua một bộ lọc kiểm duyệt (moderation filter) trước khi hiển thị cho người dùng.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
