---
layout: post
title:  "Design Pattern Oberver"
date:   2019-08-14 21:03:36 +0530
---

# Design Pattern Oberver
---

## Vấn đề (Problem):
Cách bản của bạn vài cây số có một cửa hàng (Store) bán đồ công nghệ. Sản phẩm mới về cửa hàng một ngày bất kì mà không có lịch cụ thể. Bạn không muốn thường xuyên tới (Store) và hỏi xem có sản phẩm mới nào không thay vào đó muốn nhận được thông báo mỗi khi có sản phẩm mới. Cửa hàng không thể gửi thông báo (Notification) tới mọi người trong bản của bạn vì sẽ làm phiền mọi người. Vậy cần có cơ chế để giải quyết vấn đề trên. Hình ảnh: *[refactoring.guru](https://refactoring.guru)*
![observer-comic!](/assets/images/design_pattern/observer-comic.png)



## Giải quyết (Solution)
---
Mỗi khách hàng có lựa chọn đăng kí nhận thông báo mỗi khi có sản phẩm mới về cửa hàng hay là không

## Mô hình (Structure)
---
**Publisher(Store)**: Đối tượng thực hiện việc cung cấp thông tin theo yêu cầu.  
**Oberver**: Đối tượng tiếp nhận thông tin dưới góc nhìn của publisher, trong một vài trường hợp nó còn có tên là listener chuyên dùng để lắng nghe. Giống như việc bạn để lại thông tin cho cửa hàng chứ không phải để lại body ở đó.  
**Subcriber(Person)**: Đối tượng nhận thông tin từ publisher.

![observer-class-diagram!](/assets/images/design_pattern/observer-class-diagram.png)