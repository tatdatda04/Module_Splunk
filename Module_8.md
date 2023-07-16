# Module 8: Creating and Managing Fields

## Module Objectives

- **Review the Field Extractor (FX) methods**
  >*(Xem xét các phương pháp Trích xuất Trường)*
  - Regex
  - Delimiter

- **Identify the different options to get to the Field Extractor**
  >*(Xác định các tùy chọn khác nhau để truy cập Trình trích xuất trường)*
  - Settings
  - Fields sidebar
  - Event actions

- **Review the process of extracting fields manually using regular expressions**
   >*(Xem lại quá trình trích xuất trường bằng cách sử dụng biểu thức chính quy theo cách thủ công)*

- **Use the Field Extraction Manager to modify extracted fields**
    >*(Sử dụng Trình quản lý Trích xuất Trường để chỉnh sửa các trường đã được trích xuất)*

# Field Extractions 

## Field Auto-Extraction *(Tự động trích xuất)*

- Tự động phát hiện nhiều trường dựa trên loại nguồn và `key`/`value` được tìm thấy trong dữ liệu

- Trước khi tìm kiếm, một số trường *(field)* dữ liệu đã được lưu trữ cùng với sự kiện trong chỉ mục *(index)*
  - Meta fields: `host`, `source`, and `sourcetype`
  - Internal fields:  `_time` and `_raw`

- Lúc tìm kiếm, trường khám phá *(field discovery)* khám phá các trường liên quan trực tiếp đến kết quả tìm kiếm

- Có thể trích xuất các trường khác từ dữ liệu sự kiện thô không liên quan trực tiếp đến tìm kiếm

## Performing Field Extractions *(Thực thi)*

- Có thể trích xuất các trường riêng bằng `Field Extractor (FX)`

- `FX` để trích xuất các trường tĩnh và thường sử dụng trong tìm kiếm
  - Graphical UI
  - Trích xuất trường từ các sự kiện bằng cách sử dụng biểu thức chính quy `regex` hoặc ký tự phân định `delimiter`
  - Các trường đã trích xuất được lưu trữ như các knowledge objects
  - Có thể chia sẻ và sử dụng lại trong nhiều tìm kiếm

- Truy cập `FX` từ `Settings`, `Fields Sidebar`, hoặc `Event Actions menu`

## Field Extraction Methods *(Các phương pháp)*

- Regex
  - Sử dụng option này khi sự kiện chứa dữ liệu phi cấu trúc như tệp nhật ký hệ thống
  - `FX` cố gắng trích xuất trường sử dụng Biểu thức Chính quy *(Regular Expression)* khớp với các sự kiện tương tự

- Delimiter
  - Sử dụng option này khi sự kiện của bạn chứa dữ liệu có cấu trúc như tệp `.csv`
  - Dữ liệu không có tiêu đề và các trường phải được phân tách bằng các dấu phân tách

## Workflows – RegEx *(Quy trình làm việc)*

  - `Settings > Fields > Field extractions > Open Field Extractor`
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/3ab9c4be-9fae-4416-a063-3f8f58ca6fc5)
    1 . Chọn `Data Type`
    - sourcetype
    - source
    
    2 . Chọn  `Source Type`
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/9cf88735-2df6-48e8-b9ef-d043c9832af9)

    3 . Chọn sự kiện mẫu, nhấp vào nó

    4 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/22806600-2a5c-4638-91c0-24e15733a860)

    5 . Chọn `Regular Expression`

    6 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/a2d2d961-a6de-4959-9f4b-42d1ca6ec6f2)

    7 . Chọn `value(s)` muốn trích xuất.

    8 . Cung cấp `a field name`

    9 . Chọn `Add Extraction`
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/678d0ba3-2af1-41fe-9c4d-9d53dab50b53)

    10 . `Preview` Xem trước sự kiện mẫu

    11 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/48372776-f812-4cb3-9d8a-6662d918739b)

    12 . `Validate` Xác thực các giá trị trường *(field)* thích hợp được trích xuất

    13 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/9a2d3e38-0ebf-4b53-a22e-7c93f5724a9c)

    14 . Xem lại tên cho các trường mới được trích xuất và đặt quyền

    15 . Click Finish
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/67092d29-7b44-4113-bd6f-0830c025b444)

## Using the Extracted Fields *(Sử dụng)*
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/7c93ffa1-be37-4af1-9e4a-95de5cf9177a)

## Editing Regex for Field Extractions *(Chỉnh sửa )*

1 . Từ `Select Method`, chọn `Regular Expression`

2 . Click Next 
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/8a385608-a116-4e9b-a3da-c47e3918bba5)

3 . Chọn `field` từ `extract`

4 . Cung cấp `Field Name`

5 . Chọn `Add Extraction`
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/b3612fd2-1389-4bb3-9956-3431d045c483)

6 . Chọn `Show Regular Expression >`

7 . Chọn `Edit the Regular Expression`
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/8151e312-e1b4-4cd1-9d74-7d80ec354eca)

8 . Cập nhật `regular expression`

9 . Chọn `Save`
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/53017a08-ba87-48e7-827b-ae246fbe2163)

10 . Xem lại `Extractions Name` và `set permissions` *(đặt quyền)*

11 . Chọn `> Finish`
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/f412977f-2ec7-419d-b4ed-be69dba778cd)

# Delimited Field Extractions

- Sử dụng trích xuất trường dựa trên dấu phân tách khi nhật ký sự kiện `event log` không có tiêu đề và các trường được phân tách bằng khoảng trắng, dấu phẩy hoặc các ký tự khác
- Ví dụ:
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/869959cd-8ad5-4751-ac54-aad80bdfa206)

## Workflows – Delimiters *(Quy trình làm việc)*

  - `Settings > Fields > Field extractions > Open Field Extractor`
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/abef8102-38ce-4765-a74e-494321c49cb6)
    
    1 . Chọn `Data Type`
      - sourcetype
      - source
    2 . Chọn `Source Type`
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/e500ce92-9460-4929-bf25-9ec91c937f9a)

    3 . Chọn sự kiện mẫu

    4 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/5a631f1e-f980-44e8-9802-5d29985e16af)

    5 . Chọn `Delimiters`

    6 . Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/bc087ff8-17d6-4d65-81cd-0e3451f0d3e2)

    7 . Chọn dấu phân cách `Delimiter `
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/10109a56-9e2b-4f32-b427-1c2f377081f6)

    8 . Chọn ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/1456648f-a3a0-431f-995f-1ac0270463cb) bên cạnh `field name`

    9 . Nhập `new field name`

    10 . Chọn `Rename Field`

    11 . Lặp lại với các `fields` còn lại

    12 . Sau khi xong thì Click Next
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/8341a474-9d7a-4d8d-880f-f5bcd842a8bf)

    13 . Đặt tên cho `extraction`

    14 . Click Finish
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/8bd8775f-92f7-4f15-8d32-312f279fbf9a)

## Using a Delimited Field Extraction *(Sử dụng)*

![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/89449ae9-dc4c-41fa-a682-3876420e9319)





    

    






    









    





