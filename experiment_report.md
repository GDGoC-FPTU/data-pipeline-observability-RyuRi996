# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600421  
**Name:** Phan Anh Ly Ly  
**Date:** 2026-04-15

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Dữ liệu đã được làm sạch, chỉ còn các sản phẩm hợp lệ. Trong nhóm Electronics, Laptop là mặt hàng có giá cao nhất nên câu trả lời hợp lý. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Bộ dữ liệu rác chứa outlier phi thực tế, dữ liệu sai kiểu và bản ghi lỗi, nên logic chọn giá cao nhất bị dẫn đến kết quả vô nghĩa. |

## 2. Phân tích và nhận xét (Phan tich va nhan xet)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (Tai sao Agent tra loi sai khi dung Garbage Data?)

Agent này có logic rất đơn giản: nó tìm các dòng có `category = electronics`, sau đó lấy sản phẩm có `price` lớn nhất. Vì vậy, chất lượng dữ liệu ảnh hưởng trực tiếp đến câu trả lời. Trong bộ `garbage_data.csv`, có nhiều vấn đề cùng lúc xuất hiện. Đầu tiên, có duplicate ID làm giảm độ tin cậy của tập dữ liệu và cho thấy quy trình quản lý bản ghi không chặt. Thứ hai, có giá trị sai kiểu như `ten dollars`, điều này có thể gây lỗi hoặc làm hỏng quá trình tính toán trong những pipeline phức tạp hơn. Thứ ba, có outlier rất lớn là `Nuclear Reactor` giá `999999`, và chính bản ghi này đánh lừa logic chọn sản phẩm "tốt nhất". Ngoài ra còn có dòng bị thiếu ID, category rỗng, và giá bằng 0, cho thấy dữ liệu chưa được validate. Prompt dù có viết tốt đến đâu cũng không thể sửa được một nguồn dữ liệu bị nhiễm bẩn. Nếu agent lấy dữ liệu sai làm căn cứ, nó vẫn sẽ sinh ra câu trả lời sai một cách rất tự tin.

## 3. Kết luận

**Quality Data > Quality Prompt?** Mình đồng ý trong bài lab này. Prompt tốt có thể giúp agent diễn đạt rõ hơn, nhưng nếu dữ liệu đầu vào sai, thiếu, hoặc bị nhiễu outlier, thì agent vẫn đưa ra kết quả sai. Dữ liệu sạch là nền tảng để prompt phát huy tác dụng. Nói cách khác, prompt có thể cải thiện cách trả lời, nhưng data quality mới quyết định agent đang trả lời dựa trên sự thật hay rác.
