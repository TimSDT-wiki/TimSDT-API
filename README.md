# Hướng Dẫn Sử Dụng API Của Timsdt.wiki

API của Timsdt.wiki cung cấp các dịch vụ truy vấn thông tin và tương tác với cơ sở dữ liệu của website, cho phép người dùng lấy thông tin về số điện thoại và gửi bình luận liên quan. Dưới đây là hướng dẫn chi tiết về cách sử dụng API này.

## 1. Thông Tin Cơ Bản

- **Base URL:** `https://timsdt.wiki/api/v1/`
- **Authentication:** API sử dụng phương thức xác thực bằng `API Key`. Bạn cần thêm `API Key` vào phần header của mỗi yêu cầu với định dạng sau:
  - `Authorization: Bearer your_api_key_here`

## 2. Các API Endpoint

### 2.1. Truy Vấn Thông Tin Số Điện Thoại

- **Endpoint:** `/phone-info`
- **Phương Thức:** `GET`
- **Mô Tả:** Lấy thông tin chi tiết về một số điện thoại bao gồm nhà mạng, số lượt xem, đánh giá tích cực, tiêu cực, và ngày cập nhật.
- **Tham Số Yêu Cầu:**
  - `phone`: Số điện thoại cần tra cứu (bắt buộc).
- **Ví Dụ Yêu Cầu:**

    ```http
    GET /api/v1/phone-info?phone=0912345678
    Authorization: Bearer your_api_key_here
    ```

- **Ví Dụ Phản Hồi:**

    ```json
    {
      "phone_number": "0912345678",
      "provider": "Viettel",
      "views": 123,
      "positive_reviews": 45,
      "negative_reviews": 10,
      "unsure_reviews": 5,
      "created_at": "2024-07-01"
    }
    ```

### 2.2. Gửi Bình Luận Cho Số Điện Thoại

- **Endpoint:** `/submit-comment`
- **Phương Thức:** `POST`
- **Mô Tả:** Gửi bình luận và đánh giá cho một số điện thoại.
- **Tham Số Yêu Cầu:**
  - `phone_id`: ID của số điện thoại (bắt buộc).
  - `comment`: Nội dung bình luận (bắt buộc).
  - `review_type`: Loại đánh giá, giá trị có thể là `positive`, `negative`, hoặc `unsure` (bắt buộc).
- **Ví Dụ Yêu Cầu:**

    ```http
    POST /api/v1/submit-comment
    Authorization: Bearer your_api_key_here
    Content-Type: application/json

    {
      "phone_id": 123,
      "comment": "Số điện thoại này đã gọi điện làm phiền tôi.",
      "review_type": "negative"
    }
    ```

- **Ví Dụ Phản Hồi:**

    ```json
    {
      "status": "success",
      "message": "Bình luận của bạn đã được gửi thành công."
    }
    ```

## 3. Lỗi Phổ Biến và Giải Pháp

- **401 Unauthorized:** Lỗi xác thực, kiểm tra lại `API Key` của bạn.
- **404 Not Found:** Số điện thoại hoặc `phone_id` không tồn tại trong cơ sở dữ liệu.
- **400 Bad Request:** Thiếu tham số yêu cầu hoặc tham số không hợp lệ.

## 4. Liên Hệ Hỗ Trợ

Nếu bạn gặp vấn đề trong quá trình sử dụng API, vui lòng liên hệ đội ngũ hỗ trợ của Timsdt.wiki qua email: [support@timsdt.wiki](mailto:support@timsdt.wiki).

## 5. Thực Hành An Toàn

- Bảo mật `API Key` của bạn.
- Tránh gửi thông tin nhạy cảm trong bình luận hoặc các yêu cầu API.

## 6. Cập Nhật và Phiên Bản

API này có thể được cập nhật và thay đổi. Hãy chắc chắn rằng bạn đang sử dụng phiên bản mới nhất của tài liệu để tránh các vấn đề không mong muốn.

---

# Timsdt.wiki API Usage Guide

Timsdt.wiki's API provides services for querying information and interacting with the website's database, allowing users to retrieve phone number details and submit related comments. Below is a detailed guide on how to use this API.

## 1. Basic Information

- **Base URL:** `https://timsdt.wiki/api/v1/`
- **Authentication:** The API uses `API Key` for authentication. You need to include your `API Key` in the header of each request with the following format:
  - `Authorization: Bearer your_api_key_here`

## 2. API Endpoints

### 2.1. Query Phone Number Information

- **Endpoint:** `/phone-info`
- **Method:** `GET`
- **Description:** Retrieves detailed information about a phone number, including the carrier, views, positive, negative, and unsure reviews, and the last updated date.
- **Request Parameters:**
  - `phone`: The phone number to be queried (required).
- **Sample Request:**

    ```http
    GET /api/v1/phone-info?phone=0912345678
    Authorization: Bearer your_api_key_here
    ```

- **Sample Response:**

    ```json
    {
      "phone_number": "0912345678",
      "provider": "Viettel",
      "views": 123,
      "positive_reviews": 45,
      "negative_reviews": 10,
      "unsure_reviews": 5,
      "created_at": "2024-07-01"
    }
    ```

### 2.2. Submit Comment for Phone Number

- **Endpoint:** `/submit-comment`
- **Method:** `POST`
- **Description:** Submits a comment and review for a phone number.
- **Request Parameters:**
  - `phone_id`: The ID of the phone number (required).
  - `comment`: The content of the comment (required).
  - `review_type`: The type of review, can be `positive`, `negative`, or `unsure` (required).
- **Sample Request:**

    ```http
    POST /api/v1/submit-comment
    Authorization: Bearer your_api_key_here
    Content-Type: application/json

    {
      "phone_id": 123,
      "comment": "This phone number has been bothering me.",
      "review_type": "negative"
    }
    ```

- **Sample Response:**

    ```json
    {
      "status": "success",
      "message": "Your comment has been successfully submitted."
    }
    ```

## 3. Common Errors and Solutions

- **401 Unauthorized:** Authentication error, check your `API Key`.
- **404 Not Found:** The phone number or `phone_id` does not exist in the database.
- **400 Bad Request:** Missing or invalid request parameters.

## 4. Contact Support

If you encounter issues while using the API, please contact Timsdt.wiki's support team via email: [support@timsdt.wiki](mailto:support@timsdt.wiki).

## 5. Safety Practices

- Keep your `API Key` secure.
- Avoid sending sensitive information in comments or API requests.

## 6. Updates and Versions

This API may be updated and changed. Ensure you are using the latest version of the documentation to avoid any unwanted issues.

For more information, visit: [Timsdt.wiki](https://timsdt.wiki)
