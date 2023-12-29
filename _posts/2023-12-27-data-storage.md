---
title: Minio
date: 2023-12-26 01:01:01 +0700
categories: [MLOPs, Data Storage, Minio]
tags: [kotlin]     # TAG names should always be lowercase
---

# 1. Types of storage
![Types of storage](/assets/2023-12-27-data-storage/types-of-storage.png)
_https://canonical.com/blog/what-are-the-different-types-of-storage-block-object-and-file_

# 2. So sánh file storage, block storage và object storage

| Build In Operator | Responsibility |
| :-----: | :-----: |
| BashOperator | executes a bash command   |
| BashOperator | executes a bash command|
| PythonOperator| calls an arbitrary Python function|
| EmailOperator | sends an email|

|So sánh | File storage | Block storage | Object storage |
| :-----: | :-----: | :------: | :------: |
| Kiến trúc lưu trữ | Lưu trữ file | Lưu trữ block | Lưu trữ hướng đối tượng |
|Đơn vị chuyển đổi  | files | blocks |Các object, hay các metadata tùy chỉnh|
|Hỗ trợ cập nhật | Hỗ trợ cập nhật tại chỗ | Hỗ trợ cập nhật tại chỗ | Không hỗ trợ cập nhật tại chỗ, cập nhật tạo ra các phiên bản object mới|
|Giao thức| CIFS và NFS | SCSI, SATA | REST và SOAP qua http|
|Phù hợp nhất cho | Chia sẻ file | Dữ liệu giao dịch và dữ liệu thay đổi thường xuyên | Dữ liệu tập trung và như 1 cloud storage|
|Lợi thể nổi bật | Đơn giản hóa truy cập và quản lý chia sẻ file | Hiệu năng cao | Khả năng mở rộng và truy cập phân tán|
|Tôc độ xử lý | Trở nên nặng nề khi số lượng file lến tới hàng tỷ | Phân mảnh dữ liệu, không thể truy xuất 1 file nhanh chóng | Truy xuất đến thẳng vị trí lưu trữ, tốc độ nhanh|
|Use case | Chạy ứng dụng | Thường xuyên thay đổi nội dung Sequential R/W |It thay đổi nội dung hơn,  Random R/W, ISO, Kho chứa hình ảnh/Video|

_https://bizflycloud.vn/tin-tuc/object-storage-luu-tru-doi-tuong-la-gi-khac-gi-voi-luu-tru-truyen-thong-20180702092808245.htm_

# 2. File Storage Framework Landscape
Dưới dây là danh sách một số storage frame work open source:
- MinIO: high-performance, S3 compatible object store. It is built for large scale AI/ML, data lake and database workloads.(_min.io_)
- Ceph: distributed object, block, and file storage platform.(_ceph.io_)
- JuiceFS: distributed POSIX file system built on top of Redis and S3.(_juicefs.com_)
- SeaweedFS: fast distributed storage system for blobs, objects, files, and data lake, for billions of files! Blob store has O(1) disk seek, cloud tiering. Filer supports Cloud Drive, cross-DC active-active replication, Kubernetes, POSIX FUSE mount, S3 API, S3 Gateway, Hadoop, WebDAV, encryption, Erasure Coding.

