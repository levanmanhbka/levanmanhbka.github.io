---
title: Log Library
date: 2024-03-10 01:01:01 +0700
categories: [log]
tags: [log]     # TAG names should always be lowercase
---

# 1. Tại sao phải log
Khi chạy chương trình và muốn biết các hàm gọi nhau như thế nào, luồng hoạt động của data ra sao, tại sao chương trình crash. Ta cần log lại thông tin để phân tích

# 2. Tính năng của một thư viện log
Debug < Infor < Warn < Faltal Sinh ra log level giúp việc chọn các loại log cần show ra hoặc ghi vào file.

Log layout: Giúp cấu trúc một message sẽ như thế nào ví dụ [ClassName][LogLevel][Time][Message]

Log có thể được xuất ra đâu
- Debug Window
- Console window
- File txt hoặc json
- Database

Một số tính năng khi lưu log ra file:
- Tự động chia file log thành các file con theo dung lượng hoặc theo một khoảng thời gian.
- Chế động rolling tức lưu log theo vòng, log cũ nhất sẽ được lưu vào file cuối


Các cấu hình ở phía trên có thể cấu hình thông qua code hoặc thông qua file cấu hình ví dụ file xml.

# 3. Một số thư viện log nổi tiếng

NLog, Serilog, Apache log4net, spdlog for c++
