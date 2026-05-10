# Service Boundary của nhóm

## 1. Thông tin nhóm

- Tên nhóm: Nhóm 15
- Lớp: FIT17-09
- Thành viên:
  - Trịnh Minh Quân
  - Nguyễn Nhật Quang
  - Lê Cao Tất Thành
  - Phùng Thế Ânh

- Service nhóm phụ trách:
  - Dịch vụ AI phân tích hình ảnh

- Sản phẩm tổng thể của lớp:
  - Hệ thống phân tích và xử lý hình ảnh ứng dụng AI

---

# 2. Actor

Các đối tượng tương tác với hệ thống:

- Người dùng cuối (User)
  - Upload ảnh để hệ thống phân tích
  - Xem kết quả nhận diện hình ảnh

- Quản trị viên (Admin)
  - Quản lý hệ thống
  - Kiểm tra log và trạng thái service

- Service khác trong hệ thống
  - Gửi ảnh đến AI service để xử lý
  - Nhận kết quả phân tích từ AI service

---

# 3. System Boundary

## Phần nhóm kiểm soát

Nhóm phụ trách xây dựng:

- AI Image Analysis Service
- API nhận ảnh từ người dùng
- Xử lý ảnh bằng mô hình AI
- Trả kết quả nhận diện
- Quản lý log xử lý ảnh
- Docker container cho service AI

## Phần nhóm chỉ tích hợp

- Authentication Service
- Frontend giao diện người dùng
- Database tổng của hệ thống
- API Gateway
- Notification Service

---

# 4. Service Boundary

## Service của nhóm có trách nhiệm

- Nhận ảnh từ client hoặc service khác
- Kiểm tra định dạng ảnh
- Phân tích ảnh bằng mô hình AI
- Nhận diện đối tượng trong ảnh
- Trả kết quả JSON cho hệ thống
- Ghi log xử lý ảnh
- Kiểm tra trạng thái service qua endpoint healthcheck

## Service KHÔNG làm gì

- Không quản lý đăng nhập người dùng
- Không quản lý giao diện frontend
- Không gửi email hoặc thông báo
- Không lưu trữ lâu dài dữ liệu người dùng
- Không xử lý thanh toán hoặc phân quyền

---

# 5. Input / Output

## Input

- Ảnh upload từ người dùng
- Request từ service khác
- Thông tin metadata ảnh

Ví dụ:

- JPG
- PNG
- JPEG

## Output

- Kết quả nhận diện ảnh
- Danh sách object phát hiện được
- Độ chính xác của AI
- Log xử lý


# 6. API dự kiến

| Method | Endpoint | Mục đích |
|---|---|---|
| GET | /health | Kiểm tra trạng thái hoạt động của service |
| POST | /analyze | Upload ảnh và thực hiện phân tích bằng AI |
| GET | /result/{id} | Lấy kết quả phân tích theo ID |
| GET | /logs | Xem log xử lý ảnh của hệ thống |
| DELETE | /result/{id} | Xóa kết quả phân tích ảnh |
| POST | /detect-object | Nhận diện đối tượng trong ảnh |
| POST | /classify-image | Phân loại hình ảnh bằng AI |
| GET | /model/info | Xem thông tin model AI đang sử dụng |

# 8. Sơ đồ minh họa

Người dùng sẽ gửi ảnh từ giao diện frontend đến API Gateway.  
API Gateway chuyển request đến AI Image Analysis Service của nhóm để xử lý.  

Service AI sẽ:
- nhận ảnh,
- kiểm tra dữ liệu đầu vào,
- gửi ảnh đến mô hình AI để phân tích,
- lưu kết quả vào database hoặc storage nếu cần,
- trả kết quả nhận diện về frontend cho người dùng.

Quản trị viên có thể truy cập service để kiểm tra log, trạng thái hoạt động và theo dõi quá trình xử lý ảnh.

Service của nhóm có thể kết nối với:
- Database Service để lưu dữ liệu,
- Storage Service để lưu ảnh,
- Authentication Service để xác thực người dùng.
# 9. Công nghệ dự kiến sử dụng
Docker
Python 3.11
FastAPI hoặc Flask
YOLO / Ultralytics AI Model
PostgreSQL
REST API
GitHub
# 10. Kết quả mong muốn
Service AI hoạt động độc lập bằng Docker
Phân tích được ảnh cơ bản
Trả kết quả nhanh qua API
Dễ dàng tích hợp với các service khác
Có thể mở rộng thêm model AI trong tương lai