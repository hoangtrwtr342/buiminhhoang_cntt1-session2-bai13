# (Bài Tập Tổng Hợp) Tech Lead của Cyber Arena


## Phần 1 – Lĩnh vực CNTT và đơn vị lưu trữ

### 1. Lựa chọn nhân sự kỹ thuật
* **Lựa chọn:** Ứng viên B (lĩnh vực Mạng máy tính / Quản trị hệ thống).
* **Giải thích:** Nhu cầu cốt lõi của một Cyber Arena là máy tính vận hành ổn định và hệ thống mạng mượt mà, độ trễ thấp để phục vụ khách thuê và đội tuyển tập luyện. Ứng viên B có khả năng lắp ráp, xử lý sự cố phần cứng tức thì và cấu hình hạ tầng mạng tối ưu. Về phần mềm đặt lịch thuê máy, trung tâm hoàn toàn có thể sử dụng các giải pháp phần mềm quản lý phòng máy đóng gói sẵn trên thị trường.

### 2. Sắp xếp đơn vị lưu trữ
Thứ tự tăng dần về dung lượng:
$$\text{Byte} \rightarrow \text{KB} \rightarrow \text{MB} \rightarrow \text{GB} \rightarrow \text{TB}$$

---

## Phần 2 – Mô hình IPO và lĩnh vực CNTT

### 1. Mô hình IPO trong hệ thống quay và xem lại trận đấu

| Thành phần | Vai trò trong hệ thống quay/xem lại trận đấu |
| :--- | :--- |
| **Input** | Nhận tín hiệu video hiển thị từ màn hình máy tính và âm thanh từ mic/tai nghe của tuyển thủ. |
| **Process** | Phần mềm (OBS/Streamlabs) xử lý mã hóa (encode), giải mã và nén luồng video/âm thanh. |
| **Output** | Xuất file video hoàn chỉnh ra màn hình phân tích hoặc phát trực tiếp (livestream) lên YouTube. |
| **Storage** | Ổ cứng SSD dùng để ghi và lưu trữ lâu dài các file video trận đấu (.mp4, .mkv). |

### 2. Các lĩnh vực CNTT liên quan
* **Mạng máy tính & Truyền thông:** Đảm bảo đường truyền dữ liệu băng thông cao, ổn định và không ngắt quãng khi phát sóng trực tiếp luồng video trận đấu lên nền tảng YouTube.
* **Công nghệ Đa phương tiện (Multimedia):** Đảm nhận việc ghi nhận tín hiệu hình ảnh/âm thanh, áp dụng các chuẩn nén kỹ thuật số và phát lại video phục vụ công tác phân tích chiến thuật.

---

## Phần 3 – Tính toán dung lượng và tốc độ mạng

### 1. Tính toán dung lượng lưu trữ
* **Tổng dung lượng 20 trận (MB):**
  $$20 \times 500\text{ MB} = 10.000\text{ MB}$$
* **Quy đổi kết quả sang GB:**
  $$10.000 \div 1024 \approx 9,77\text{ GB}$$
* **Khả năng lưu trữ của ổ cứng SSD 512 GB:**
  * Ổ SSD 512 GB hoàn toàn đủ chỗ lưu trữ vì $9,77\text{ GB} < 512\text{ GB}$.
  * Dung lượng còn trống sau 1 tháng đầu tiên:
    $$512 - 9,77 = 502,23\text{ GB}$$

### 2. Tính toán tốc độ mạng
* **Tốc độ truyền tải tối đa quy đổi ra MB/s:**
  $$100\text{ Mbps} \div 8 = 12,5\text{ MB/s}$$
* **Thời gian tối thiểu tải lên đoạn video 200 MB:**
  $$\text{Thời gian} = \frac{200\text{ MB}}{12,5\text{ MB/s}} = 16\text{ giây}$$
* **Lý do thời gian thực tế thường lâu hơn:**
  Băng thông mạng trên thực tế bị hao hụt bởi tiêu đề gói tin (network overhead), độ trễ kết nối (ping/jitter), hoặc do băng thông đường truyền bị chia sẻ với các máy trạm khác đang truy cập trong quán.

---

## Phần 4 – Phần cứng và mô hình DIKW

### 1. Quyết định nâng cấp linh kiện
* **Lựa chọn:** Nâng cấp **CPU**.
* **Giải thích:** Bộ nhớ 16 GB RAM hiện tại đã đủ đáp ứng cho hệ điều hành, game Liên Minh Huyền Thoại và ứng dụng nền. Hiện tượng giật khung hình khi vừa chơi game vừa stream/quay hình xuất phát từ việc vi xử lý bị quá tải (100% load) do phải gánh thêm tác vụ mã hóa (encode) luồng video thời gian thực; nâng cấp CPU nhiều nhân/luồng và xung nhịp mạnh hơn sẽ giải quyết triệt để vấn đề này.

### 2. Áp dụng mô hình DIKW vào tình huống thực tế

| Tầng | Nội dung trong tình huống | Vì sao thuộc tầng này? |
| :--- | :--- | :--- |
| **Data** | Các mốc thời gian chết của tuyển thủ, video ghi lại trận đấu, chỉ số cắm mắt. | Là dữ liệu thô, các số liệu và ghi nhận ban đầu chưa qua xử lý hay phân tích ngữ cảnh. |
| **Information** | Tuyển thủ thường xuyên bị hạ gục trong khoảng thời gian từ phút 15 đến 20. | Dữ liệu thô đã được tổng hợp để chỉ ra một quy luật/hiện tượng cụ thể. |
| **Knowledge** | Nguyên nhân dẫn đến việc bị hạ gục là do thiếu tầm nhìn trên bản đồ. | Phân tích sâu để nắm bắt bản chất vấn đề và mối quan hệ nhân - quả đằng sau thông tin. |
| **Wisdom** | Quyết định yêu cầu tuyển thủ mua thêm mắt (Ward) để kiểm soát tầm nhìn ở các trận sau. | Vận dụng hiểu biết để đưa ra giải pháp/chiến lược tối ưu cải thiện kết quả tương lai. |
