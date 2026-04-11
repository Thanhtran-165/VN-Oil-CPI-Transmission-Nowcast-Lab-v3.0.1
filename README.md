# VN Oil-CPI Transmission & Nowcast Lab v3.0.1 — Release Note

## Tổng quan

Phiên bản **v3.0.1** đánh dấu việc chỉ báo đã bước vào trạng thái **stable, usable và gần-final** trong phạm vi dữ liệu và năng lực hiện tại của TradingView cho bài toán **Oil → CPI Việt Nam**.

Bản này không còn là một indicator quan sát tương quan đơn giản. Thay vào đó, nó đã phát triển thành một framework nhỏ để:

* nghiên cứu **mối quan hệ lịch sử** giữa dầu và CPI Việt Nam,
* theo dõi **kênh truyền dẫn trực tiếp** qua `VNCPIT`,
* và **nowcast áp lực CPI tháng hiện tại** từ biến động dầu thời gian thực.

---

## Nâng cấp học thuật chính

### 1. Tách hai lớp phân tích riêng biệt

Chỉ báo hiện phân biệt rõ:

* **Direct pass-through:** `UKOIL → VNCPIT`
* **Headline pass-through:** `UKOIL → CPI MoM / CPI YoY`

Điều này giúp tách bạch giữa:

* tác động trực tiếp của dầu lên nhóm vận tải,
* và tác động rộng hơn lên CPI tổng thể.

### 2. Sử dụng nguồn CPI chính thức từ TradingView

Phiên bản này sử dụng trực tiếp:

* `VNIRMM` cho **CPI MoM**
* `VNIRYY` cho **CPI YoY**
* `VNCPIT` cho **CPI Transportation**

Thay vì tự suy luận toàn bộ từ CPI index, cách tiếp cận này giúp indicator sạch hơn và nhất quán hơn với cấu trúc dữ liệu gốc.

### 3. Căn chỉnh đúng mốc thời gian dữ liệu

Indicator xử lý theo logic:

* dữ liệu CPI trên TradingView đang được gắn ở **tháng công bố**
* trong khi nghiên cứu truyền dẫn cần quy về **tháng tham chiếu**

Vì vậy hệ thống sử dụng **reference-month alignment với lag = 1**, giúp tránh sai lệch khi so sánh dầu và CPI.

### 4. Bổ sung lớp nghiên cứu động

Phiên bản này đã triển khai thêm:

* **rolling beta**
* **model comparison giữa lag 0 / lag 1 / lag 2**
* **stability regime**
* **confidence scoring**

Nhờ đó, chỉ báo không chỉ hỏi *“có tương quan hay không”*, mà còn hỏi:

* mô hình hiện có ổn định không,
* độ trễ nào đang trội,
* mức độ tự tin của nowcast là bao nhiêu.

---

## Nâng cấp UI / UX chính

### 1. Dashboard gọn hơn, tập trung hơn

Bản dashboard hiện tại chỉ giữ **2 line chính**:

* **Oil live z-score**
* **Headline pressure**

Điều này giúp giảm cảm giác “lab mode” và đưa indicator gần hơn với trải nghiệm đọc nhanh của người dùng cuối.

### 2. Tách riêng các lớp thông tin quan trọng

Bảng tóm tắt hiện chia rõ các lớp:

* áp lực hiện tại,
* độ tin cậy,
* xác nhận từ kênh trực tiếp,
* cấu trúc lịch sử,
* độ ổn định mô hình,
* và kết luận cuối cùng.

### 3. Bổ sung line labels

Các đường chính hiện đã có **nhãn tên trực tiếp trên chart**, giúp người dùng nhìn nhanh và biết mình đang đọc đường nào mà không phải dò legend.

---

## Ý nghĩa sử dụng

Ở trạng thái hiện tại, chỉ báo có thể được dùng như một công cụ để trả lời nhanh các câu hỏi:

* **Dầu tháng này đang gây áp lực tăng hay giảm lên CPI tháng hiện tại?**
* **Quan hệ lịch sử đó có còn đáng tin không?**
* **Kênh trực tiếp qua vận tải có đang xác nhận tín hiệu headline hay không?**

---

## Trạng thái hiện tại

**v3.0.1** có thể được xem là phiên bản:

* **ổn định**
* **đủ tốt để sử dụng thực tế**
* và **gần chạm trần học thuật của TradingView** cho bài toán Oil → CPI Việt Nam, trong phạm vi dữ liệu kinh tế mà nền tảng hiện hỗ trợ.

---

## Ghi chú

Chỉ báo này là một công cụ **transmission & nowcast** cho **kênh dầu**.

Nó **không phải** mô hình dự báo toàn bộ CPI Việt Nam theo nghĩa đầy đủ, vì CPI thực tế còn chịu ảnh hưởng của nhiều nhóm khác ngoài dầu như thực phẩm, dịch vụ, giá điều hành, mùa vụ và hiệu ứng nền.

Nói cách khác, đây là một công cụ để theo dõi:

> **áp lực CPI từ kênh dầu**,
> không phải toàn bộ cấu trúc lạm phát của nền kinh tế.

---

## Kết luận

Phiên bản **v3.0.1** là bước hoàn thiện quan trọng:

* lõi học thuật đã đủ mạnh,
* cấu trúc truyền dẫn đã rõ hơn,
* dashboard đã gọn hơn,
* và trải nghiệm đọc đã tiến gần tới một sản phẩm hoàn chỉnh.

Đây là nền tảng tốt để tiếp tục tinh chỉnh nhẹ về wording / UI trong các bản tiếp theo mà không cần thay đổi lớn ở lõi mô hình.
