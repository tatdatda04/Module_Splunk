# Module 5: Filtering and Formatting Data *(Lọc và Định dạng dữ liệu)*

## Module Objectives

- [Use the eval command *(Sử dụng lệnh eval)*](#eval-Command)

  + Perform calculations *(Thực hiện phép tính)*
		
  + Convert values *(Chuyển đổi giá trị)*
		
  + Round values *(Giá trị làm tròn)*
		
  + Format values *(Định dạng giá trị)*
		
  + Use conditional statements *(Sử dụng câu điều kiện)*

- [Use the search and where commands to filter calculated results *(Sử dụng lệnh search và where để lọc kể quả tính)*](#Filtering-Results – search-and-where)

- Use fillnull command *(Sử dụng lệnh fillnull)*

# eval Command

- **Overview** *(Tổng quan)*:
  + Cho phép tính toán và thao tác các giá trị trường trong báo cáo

	`eval fieldname1 = expression1 [, fieldname2 = expression2...]`

  + Hỗ trợ nhiều chức năng

  + Kết quả của eval được ghi vào trường mới hoặc trường hiện có đã chỉ định

    + Nếu trường đích tồn tại, các giá trị của trường được thay thế bằng kết quả của eval
			
	 + Dữ liệu được lập chỉ mục không bị sửa đổi và không có dữ liệu mới nào được ghi vào chỉ mục
			
	 + Giá trị trường được xử lý theo cách phân biệt chữ hoa chữ thường

- **Lệnh eval cho phép**
    + Tính biểu thức
    + Đặt kết quả vào một trường
	+ Sử dụng trường đó trong tìm kiếm hoặc các biểu thức khác

![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/c0d6c9b3-937f-4a64-ae3a-88e3ecc93389)

- **Convert Values** *(chuyển đổi giá trị)*

  + Ví dụ này hiển thị tổng số byte được sử dụng cho từng danh mục sử dụng
 
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/bdab1d4d-67f2-41d7-a050-4f7b1c4a234f)

    + Rất khó để xác định lượng băng thông đang được sử dụng bằng cách xem `byte`

	+ Đầu tiên, sử dụng `eval` để chuyển đổi giá trị `byte` thành `megabyte`

	+ Kết quả của `eval` phải được đặt thành một lĩnh vực mới hoặc hiện có

  + Trong ví dụ này:
 			
      + Tính số `byte` cho từng loại sử dụng
			
	  + Tạo một trường mới có tên là `băng thông` *(bandwidth)*
			
	  + Chuyển đổi giá trị của trường `Byte` thành `MB` bằng cách chia giá trị trường `Byte` cho (1024*1024)
   
  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/ba0d9233-6c72-4b42-a2d4-15f8872d1f82)

- **Round Values** *(giá trị round)*
		
	+ Kết quả của Băng thông rất khó đọc với rất nhiều dấu thập phân

	+ `Hàm round`*(trường/số, số thập phân)* đặt giá trị của trường thành số thập phân bạn chỉ định

  + Trong ví dụ này:

    + Chia giá trị của trường `Byte` cho (1024*1024)
			
	+ Làm tròn kết quả đến hai chữ số thập phân
		
  + Nếu số thập phân không xác định, kết quả là một số nguyên

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/756ea572-a759-43b8-8ff8-c3c50b33c52c)

- **Removing Fields** *(xóa fields)*
	
  + `Fields` không còn cần thiết có thể xóa

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/a8077667-8506-4537-805c-ce14d9f17346)

- **Calculating Values** *(Tính giá trị)*

  + Có thể thực hiện các hàm toán học đối với các `fields` có giá trị `fields số` 

  + Ví dụ:
 
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/79261dec-280e-4fed-9d2c-48c49c97a934) ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/f719afce-c8e2-4d07-9f15-15e688a8bc00)

    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/def6d62f-310f-4e9d-9f53-0ca00e05b2b6) ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/f135a0d7-d02c-477b-931c-566973bfcbcd)

- **tostring Function** *(Hàm tostring)*

  + `tostring` chuyển đổi một giá trị trường số thành một chuỗi

	`tostring(field,"option")`

  + Options:
	   + `commas`: áp dụng dấu phẩy

            > Nếu số bao gồm số thập phân, nó làm tròn đến hai chữ số thập phân
	   + `duration`: định dạng số dưới dạng `hh:mm:ss`

	  + `hex`: định dạng số trong hệ thập lục phân

    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/13211785-15b9-4907-8d2a-13ba69d8fd46)
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/be4635ea-5d13-4ecd-ba91-8862e6921bce)

- **duration Option** *(Tùy chọn thời lượng)*

    + `A` : thống kê tính toán `sessionTime` cho mỗi phiên *(JSESSIONID)*
 	
      + Sử dụng hàm phạm vi để trả về sự khác biệt giữa giá trị lớn nhất và nhỏ nhất của _time

	+ `B` : sắp xếp 5 hiển thị 5 giá trị thường xuyên nhất

	+ `C` : Tùy chọn thời lượng định dạng thời gian là `hh:mm:ss`

      ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/4202f5fd-55ff-432e-b266-674a63d42bb9)

- **Formatting and Sorting Values** *( Định dạng và sắp xếp giá trị )*

  + Với các ký tự được thêm vào sẽ chuyển đổi giá trị trường số thành chuỗi

  + Để sắp xếp theo số, trước tiên hãy sắp xếp, sau đó sử dụng `eval`
 
      ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/00eadecd-12ea-47ee-95cf-30553aacd9da)

- **eval Command witn Multiple Expressions** *( lệnh eval với nhiều biểu thức)*

  + Nhiều biểu thức có thể được kết hợp thành một lệnh eval

  + Mỗi biểu thức tiếp theo tham chiếu đến kết quả của biểu thức trước đó

  + Các biểu thức phải được phân tách bằng dấu phẩy

	`eval fieldname1 = expression1,
    fieldname2 = expression2,
    fieldname3 = expression3...`

- **if Function Syntax** *(Cú pháp hàm if)* :
    `if(X,Y,Z)`

  + Hàm if nhận ba đối số
		
  + Đối số đầu tiên `X`, là một biểu thức `Boolean`

    + Nếu nó đánh giá là `TRUE`, kết quả sẽ đánh giá đối số thứ hai `Y`

    + Nếu nó đánh giá là `FALSE`, kết quả sẽ đánh giá đối số thứ ba `Z`

  + Các giá trị không phải là số phải được đặt trong "dấu nháy kép"

  + Giá trị trường được xử lý theo cách phân biệt chữ hoa chữ thường

- **case Function** *(hàm case)*:
  `case(X1, Y1, X2, Y2,...)`

  + Đối số đầu tiên `X1`, là một biểu thức `Boolean`

  + Nếu nó đánh giá là `TRUE`, kết quả sẽ đánh giá là `Y1`

  + Nếu nó đánh giá là `FALSE`, biểu thức Boolean tiếp theo `X2`, được đánh giá,...

  + Nếu bạn muốn một mệnh đề "otherwise”, chỉ cần kiểm tra một điều kiện mà bạn biết là đúng ở cuối

- **eval function** *(hàm đánh giá)*

  + Để đếm số sự kiện có chứa một giá trị trường cụ thể, hãy sử dụng hàm đếm và `eval`

    + Được sử dụng trong lệnh chuyển đổi, chẳng hạn như số liệu thống kê

    + Yêu cầu mệnh đề  `as`

    + Dấu ngoặc kép là bắt buộc đối với giá trị trường ký tự

    + Giá trị trường phân biệt chữ hoa chữ thường

# Filtering Results – search and where

- `Lệnh search` và `lệnh where` đều lọc kết quả

  + `search`

    + Có thể dễ dàng hơn nếu quen thuộc với cú pháp tìm kiếm cơ bản

    + Xử lý các giá trị trường theo cách không phân biệt chữ hoa chữ thường

    + Cho phép tìm kiếm theo từ khóa

    + Có thể được sử dụng tại bất kỳ điểm nào trong đường ống tìm kiếm

  + `where`

    + Có thể so sánh các giá trị từ hai trường khác nhau

    + Các hàm có sẵn, chẳng hạn như `isnotnull()`

    + Xử lý các giá trị trường theo cách phân biệt chữ hoa chữ thường

    + Không thể xuất hiện trước đường dẫn đầu tiên trong đường dẫn tìm kiếm
   
   
- `search Command `

  + Để lọc kết quả, hãy sử dụng tìm kiếm tại bất kỳ điểm nào trong quy trình tìm kiếm

  + Hoạt động chính xác như chuỗi tìm kiếm trước đường ống đầu tiên

    + Sử dụng ký tự đại diện `“*”`

    + Xử lý các giá trị trường theo cách không phân biệt chữ hoa chữ thường
   
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/72f5abe5-d525-4090-9dfd-689a562df2d5)

- `where Command` : where eval-expression

  + Sử dụng cú pháp biểu thức giống như lệnh `eval`

  + Sử dụng biểu thức `boolean` để lọc kết quả tìm kiếm và chỉ giữ kết quả là `True`

  + Chuỗi trích dẫn kép được hiểu là giá trị trường

    * Xử lý các giá trị trường theo cách phân biệt chữ hoa chữ thường

  + Chuỗi không trích dẫn hoặc trích dẫn đơn được coi là trường

- `where Command With like Operator` *( Lệnh where với toán tử like )*

  + Có thể thực hiện tìm kiếm ký tự đại diện với lệnh `where`

  + Sử dụng `_` cho một ký tự và `%` cho nhiều ký tự

  + Phải sử dụng toán tử like với ký tự đại diện
 
# fillnull Command

  - Sử dụng `fillnull` để thay thế giá trị `null` trong các `field`
  
  - Sử dụng `value=string` để chỉ định một chuỗi bạn muốn hiển thị thay thế
		
      > Ví dụ: fillnull value=NULL

  - Nếu không có `value= clause` , giá trị thay thế mặc định là `0`

  - Tùy chọn, giới hạn trường nào `fillnull` áp dụng bằng cách liệt kê chúng ở cuối lệnh
		
      > Ví dụ: fillnull VALUE=“N/A” hoàn tiền chiết khấu












