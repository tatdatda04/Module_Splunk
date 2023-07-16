# Module 7 Introduction to Knowledge Objects 

## Module Objectives

- [Identify the categories of knowledge objects *( Các loại knowledge objects)*](#What-are-Knowledge-Objects)

- [Define the role of a knowledge manager *( Vai trò của knowledge manager)*](#What-is-a-Knowledge-Mangager)

- [Identify naming conventions *(Quy ước đặt tên)*](#Defining-Naming-Conventions)

- [Review permissions *(Quyền hành)*](#Reviewing-Permissions)

- [Manage knowledge objects *( Quản lí knowldge objects)*](#Managing-Knowledge-Objects)

- [Describe the Splunk Common Information Model `CIM` *(Mô hình thông tin Splunk)*](#Using-the-Splunk-Common-Information-Model)

# What are Knowledge Objects?

- Là công cụ để điều tra và phân tích các khía cạnh khác nhau của dữ liệu 

  - Data interpretation – Fields and field extractions *(Giải trình dữ liệu – `Field` và trích xuất `field`)*

  - Data classification – Event types *(Phân loại dữ liệu – Các loại sự kiện)*

  - Data enrichment – Lookups and workflow actions *(Bổ sung dữ liệu – Tra cứu và vận hành quy trình)*

  - Normalization – Tags and field aliases *(Chuẩn hóa – `Tags` và tên `field`)*

  - Datasets – Data models *(Bộ dữ liệu – Mô hình dữ liệu)*

![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/d4aa567f-0951-4354-80da-3e803269f77a)

- `Shareable` 
  - Có thể được chia sẻ giữa những người dùng

- `Reusable`
  - Đối tượng lưu trữ có thể được sử dụng bởi nhiều người hoặc ứng dụng, như các macro và báo cáo
 
- `Searchable`
  - Các đối tượng được lưu trữ, có thể được sử dụng trong quá trình tìm kiếm

# What is a Knowledge Mangager?

- Giám sát quá trình tạo ra và sử dụng `knowledge objects` cho một nhóm hoặc quy trình triển khai cụ thể.

- Chuẩn hóa các dữ liệu sự kiện

- Tạo mô hình dữ liệu cho `Pivot users`

# Defining Naming Conventions

- Quy ước đặt tên trong môi trường được khuyến nghị. Ví dụ:
  - Group: Tương ứng với (các) nhóm làm việc của `user` lưu đối tượng
      >Ví dụ: `SEG`, `NEG`, `OPS`, `NOC`
  - Object Type: Loại đội tượng
      >`alert`, `report`, `summary-index-populating`
  - Description: Có nghĩa về ngữ cảnh và mục đích của việc tìm kiếm, giới hạn trong một hoặc hai từ nếu có thể; để đảm bảo tên tìm kiếm là duy nhất
      >Ví dụ: `SEG_Alert_WinEventlogFailures`

# Reviewing Permissions
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/95cc0aac-b491-426b-b600-020bff9741e1)

- `*` Quyền đọc hoặc viết nếu người tạo cấp quyền cho vai trò đó

- Khi một object được tạo, `Display For` được đặt thành `Owner` theo mặc định

- Khi quyền của đối tượng được đặt thành `App` hoặc `All app`, tất cả các vai trò đều được cấp quyền đọc
  - Quyền ghi được dành riêng cho `admin` và `the object creator` trừ khi người tạo chỉnh sửa quyền
 
- Chỉ vai trò `admin` mới có thể thăng cấp đối tượng *(promote an object)* cho tất cả các ứng dụng
  - Các vai trò khác có `All app` chuyển sang màu xám

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/3dee435d-dd0d-41dd-9589-45d928360632)

# Managing Knowledge Objects

- `Knowledge objects` được quản lí chung từ `Setting > Knowledge`

- Vai trò và quyền xác định khả năng sửa đổi cài đặt của object

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/577c5bed-0dbc-4479-84d8-d97d4eb3f610)

# Using the Splunk Common Information Model

- Là phương pháp chuẩn hóa dữ liệu
- Dễ dàng liên kết dữ liệu từ các nguồn và loại nguồn khác nhau
- Tận dụng để tạo ra các đối tượng khác nhau - trích xuất trường,
  - field extractions *(Trích xuất lĩnh vực)*
  - field aliases *(Tên lĩnh vực)*
  - event types *(loại sự kiện)*
  - tags
  
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/84873042-a265-421d-996e-a8596bc37f7a)



