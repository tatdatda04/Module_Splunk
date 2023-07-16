# Module 6 Correlating Events 

## Module Objectives

- Identify transactions *(Xác định giao dịch)*
- Group events using fields *(Nhóm sự kiện bằng cách sử dụng các trường)*
- Group events using fields and time *(Nhóm sự kiện bằng cách sử dụng các trường và thời gian)*
- Search with transactions *(Tìm kiếm với các giao dịch)*
- Report on transactions *(Báo cáo giao dịch)*
- Determine when to use transaction vs. stats *(Xác định thời điểm sử dụng giao dịch so với số liệu thống kê)*

# Transactions 

## what is a Transacsion ?
- **Giao dịch** là bất kỳ nhóm sự kiện liên quan nào kéo dài thời gian

- **Sự kiện** có thể đến từ nhiều ứng dụng hoặc máy chủ

   - Các **sự kiện** liên quan đến một lần mua hàng từ cửa hàng trực tuyến có thể trải dài trên máy chủ ứng dụng, cơ sở dữ liệu và công cụ thương mại điện tử

  - Một email có thể tạo nhiều sự kiện khi nó di chuyển qua nhiều hàng đợi khác nhau

  - Mỗi sự kiện trong nhật ký lưu lượng mạng đại diện cho một người dùng tạo một yêu cầu http duy nhất

  - Truy cập một trang web thường tạo ra nhiều yêu cầu http
      >Tệp HTML, JavaScript, CSS
      
      >Flash, hình ảnh, v.v.

## transaction Command

- transaction `field-list`
  - `field-list` có thể là một tên trường hoặc danh sách tên trường
  - Các sự kiện được nhóm thành các giao dịch dựa trên giá trị của các trường này
  - Nếu nhiều trường được chỉ định và tồn tại mối quan hệ giữa các trường đó, các sự kiện có giá trị trường liên quan được nhóm thành một giao dịch
-  Quy ắc chung:
    -  `maxspan`, `maxpause`, `startswith`, `endswith`

## Sự kiến giống với JSESSIONID

- `Log` hiển thị một số sự kiện có cùng giá trị `JSESSIONID`(SD0SL10FF3ADFF4950)

- Tuy nhiên, khó để:
  - Xem các sự kiện theo nhóm
  - Có được cái nhìn sâu sắc về những gì đang xảy ra với những sự kiện này
  - Biết nếu có các sự kiện khác nằm rải rác trong tập hợp kết quả
 
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/ea5ab61d-f9dc-46ea-82d2-5c81acb862ff)

## Specific Fields *(Lĩnh vực cụ thể)*

- Lệnh `transaction` tạo ra các trường bổ sung, như:
  - `thời lượng` sự khác biệt giữa dấu thời gian cho sự kiện đầu tiên và sự kiện cuối cùng trong giao dịch
  -  `eventcount` số lượng sự kiện trong giao dịch
 
## maxspan/ maxpause

- Có thể xác định khoảng thời gian tổng thể tối đa và khoảng cách tối đa giữa các sự kiện
  - `maxspan`= 10m
    >Tổng thời gian tối đa giữa các sự kiện `earliest` và `latest`

    >Nếu không chỉ định, mặc định là -1 (hoặc không giới hạn)
  - `maxpause`= 1m

    >Tổng thời gian tối đa giữa các sự kiện

    >Nếu không chỉ định, mặc định là -1 (hoặc không giới hạn)
  
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/da8e55a3-f320-4bc1-8800-032cb9110081)


## starswith/ endswith

- Để hình thành các giao dịch dựa trên các điều khoản, giá trị trường hoặc đánh giá, sử dụng các tùy chọn bắt đầu và kết thúc

  - Trong ví dụ này:
    - Sự kiện đầu tiên trong giao dịch bao gồm `addtocart`
    - Sự kiện cuối cùng bao gồm mua hàng
  
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/17e7ffd5-c908-4e20-b4a1-94f7954929bf)
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/62a70168-f7ba-4495-8284-c07fc1861490)

## Investigating *(Điều tra)*
- Giao dịch có thể hữu ích khi một sự kiện đơn lẻ không cung cấp đủ thông tin
- Ví dụ này tìm kiếm trong nhật ký email cho cụm từ `“REJECT”`
- Các sự kiện bao gồm thuật ngữ không cung cấp nhiều thông tin về việc từ chối
- Bằng cách tạo giao dịch, có thể tìm kiếm và xem các sự kiện bổ sung liên quan đến việc từ chối, chẳng hạn như:
  - Địa chỉ IP của người gửi
  - Đảo ngược kết quả tra cứu DNS
  - Hành động được thực hiện bởi hệ thống thư sau khi từ chối
- `mid` – ID tin nhắn
- `dcid` – ID kết nối phân phối
- `icid` – ID kết nối đến

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/003d94b6-eaba-46a8-9410-3a5a8d2b1b0b)

## Reporting *(Báo cáo)*

- Có thể sử dụng các lệnh thống kê và báo cáo với các giao dịch
- Trong ví dụ này, một giao dịch được xác định bởi các sự kiện chia sẻ `clientip` và phù hợp trong khoảng thời gian 10 phút
- hàm `count()` đếm số lượng giao dịch và phân tách số lượng theo thời lượng của mỗi giao dịch

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/fec70af2-d285-49d8-bdfe-f7a14498c508)

    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/e9dcbbed-819a-48a6-b7b0-2172e18f41f5)


## vs.stats *(So sánh số liệu thống kê)*

- Khi có lựa chọn, sử dụng `stats`—việc này nhanh hơn và hiệu quả hơn, đặc biệt là trong môi trường Splunk rộng lớn
- Chỉ sử dụng giao dịch khi :
  - Cần xem các sự kiện tương quan với nhau
  - Phải xác định nhóm sự kiện dựa trên giá trị bắt đầu/kết thúc hoặc phân đoạn theo thời gian
- Sử dụng số liệu thống kê khi bạn:
  - Muốn xem kết quả của một phép tính
  - Có thể nhóm các sự kiện dựa trên giá trị trường 
- Theo mặc định, có giới hạn 1.000 sự kiện cho mỗi giao dịch
  - Không có giới hạn như vậy áp dụng cho số liệu thống kê
  - Quản trị viên có thể thay đổi giới hạn bằng cách định cấu hình
  - `max_events_per_bucket trong limits.conf`


  

