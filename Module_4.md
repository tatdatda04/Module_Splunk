# Module 4: Advanced Visualizations

## Module Objectives *( Mục tiêu của Mô-đun)*:

- [Tạo trendline *(đường xu hướng)*](#Trendline-Command)
- [Tạo bản đồ :](#Map)
	+ Vị trí
	+ Thống kê
	+ Geom
- [Tạo và định dạng các giá trị đơn lẻ](#Create-and-format-single-values)
- [Sử dụng lệnh addtotals](#Use-the-addtotals-command)

# Trendline Command
- Sử dụng để vẽ đường xu hướng trên biểu đồ dữ liệu. Đường xu hướng là một đường thẳng hoặc đường cong được tạo ra để đại diện cho xu hướng hay mô hình ẩn trong dữ liệu.
- Command: 
	`trendline <trendtype><period>(field) [AS newfield]`
	
	- Trong đó `trendtype` gồm:
	
		+ `sma` *(Simple Moving Average - Trung bình động đơn giản)*: tính trung bình giá trị của dữ liệu trong một khoảng thời gian cố định. Nó được tính bằng cách lấy tổng các giá trị trong khoảng thời gian và chia cho số lượng điểm dữ liệu trong khoảng đó, giúp mịn dần dữ liệu và làm nổi bật xu hướng chung trong biểu đồ. Điểm yếu là nó trung bình hóa tất cả các giá trị trong khoảng, không quan tâm nhiều đến sự biến đổi gần đây hơn.

		+ `ema` *(Exponential Moving Average - Trung bình động mũi tên)*: tính trung bình giá trị của dữ liệu dựa trên trọng số khác nhau cho các điểm dữ liệu. Trọng số cao nhất được đặt cho dữ liệu gần đây nhất và giảm dần khi xa về quá khứ. Điều này cho phép nó đáp ứng nhanh hơn với các biến động gần đây hơn so với `sma` . `ema` thường được sử dụng để theo dõi xu hướng ngắn hạn và phản ứng nhanh hơn với các sự thay đổi gần đây. 

		+ `wma` *(Weighted Moving Average - Trung bình động có trọng số)*: tính trung bình giá trị của dữ liệu trong một khoảng thời gian cố định, tương tự như `sma` . Tuy nhiên, `wma` gán trọng số khác nhau cho các điểm dữ liệu trong khoảng. Trọng số cao nhất được đặt cho dữ liệu gần đây nhất và giảm dần khi xa về quá khứ. `wma` cung cấp sự linh hoạt hơn so với `sma` bằng cách đặt nhiều trọng số khác nhau cho các điểm dữ liệu, giúp nhận biết các biến động gần đây hơn.
- Ta phải xác định được khoảng thời gian *(period)* qua đó mới có thể tính toán được xu hướng.

- Khoảng thời gian *(period)* phải là số nguyên từ 2 đến 10000.

	- Trong ví dụ dưới, `sma2()` có hiệu lực 
		
	-  Những `sma()` không hiệu lực và báo lỗi vì chưa xác định khoảng thời gian `(period)`	

![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/39c270a3-7798-45dc-9774-8dbd8c974ad4)
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/03663789-aa14-4ad8-a5dc-3d67caa8eced)

# Map 
	
- **Có 2 dạng map**:
		
	- `Cluster Map`: là một loại biểu đồ dữ liệu được sử dụng để hiển thị sự phân cụm *(clustering)* của các sự kiện dữ liệu dựa trên các đặc trưng tương tự hoặc gần nhau. Nó giúp tạo ra một cái nhìn tổng quan về cách các sự kiện dữ liệu được nhóm lại thành các cụm dựa trên mối quan hệ tương đồng.
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/4093b67c-be29-4023-be83-3ba30c9680bc)

	- `Choropleth Map`: là một loại biểu đồ dữ liệu trong đó các khu vực địa lý được tô màu theo giá trị của một biến số cụ thể. Điều này cho phép hiển thị mức độ hoặc giá trị của biến số đó trên một bản đồ địa lý.
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/175e2e2e-9810-4fb9-96bf-b2c65346fefd)

- **iplocation Command**

	+ Sử dụng `iplocation` để tra cứu và thêm thông tin vị trí một sự kiện nào đó. Chúng sẽ bao gồm thành phố, quốc gia, khu vực, vĩ độ và kinh độ

	+ Không phải tất cả các Ip đều có sẵn các thông tin trên 

	+ Splunk tự động xác định các trường *(field)* mặc định lat và lon *(latitude và longitude)* được yêu cầu bởi `lệnh geostats` khi làm việc với dữ liệu địa lý.
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/8e31f4c4-3815-4117-bfaa-4d95b23e97b6)
![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/6105c37c-59a0-45d5-a10b-c71d3e7173c0)


- **geostats Command**

	+ Sử dụng `geostats` để tính toán các thống kê và hiển thị bản đồ cụm

	`geostats [latfield=string] [longfield=string] [stats-agg-term]* [by-clause]`

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/7ccd7556-44be-4dce-bfcd-5f8eafeb0c77)
	
	+ Data phải bao gồm các giá trị vĩ độ và kinh độ.

	+ Chỉ xác định vĩ độ và trường dài nếu chúng khác với các trường vĩ độ và vĩ độ mặc định

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/53518b4f-1c2b-47c8-94a9-5ebe98040eda)

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/95d05f33-61d9-4e47-b5e0-1c3cb409fb19)

- **Choropleth Map** 
		
	+ Sử dụng `shading` *(đổ màu)* để hiển thị các thông số tương đối, chẳng hạn như doanh số bán hàng, các cuộc xâm nhập mạng và các thông số tương tự, cho các vùng địa lý được định nghĩa trước.

	+ Để xác định ranh giới vùng địa lý, bạn cần có một trong hai loại sau:

		- `KML` *(Keyhole Markup Language)*: là một ngôn ngữ đánh dấu được sử dụng để biểu thị thông tin địa lý trên bản đồ, và nó có thể chứa các định nghĩa vùng địa lý cho **bản đồ Choropleth**.

   		- `KMZ` *(compressed Keyhole Markup Language)*: là một phiên bản nén của tệp tin `KML`, chứa thông tin địa lý và định nghĩa vùng địa lý cho **bản đồ Choropleth**.

	+ Splunk có cung cấp :

		- `geo_us_states`: United States
			
		- `geo_countries`: các quốc gia trên thế giới

		` ...| geom [featureCollection][featureIdField=string]`
- **geom Command**

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/4dedf1f8-6296-486d-80d0-0d6646c0760f)

  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/bcbb81b2-04ab-4e0a-a1a2-993d50200fec) ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/c18f2242-7364-42e8-a258-844da960c5d6)

# Create and format single values

- **Viewing Results as a Single Value** *(Xem kết quả dưới 1 giá trị)*

	+ Trực quan hóa giá trị cung cấp nhiều tùy chọn

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/00c32073-1b67-43e2-ae6c-883baef2b3ff)

- **Single Value Visualizations: Formatting** *(Định dạng)* 

	+ Đặt màu bằng UI người dùng hoặc bằng lệnh máy đo

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/9918bd49-d02b-46a3-9b7f-512b5497e4a2)

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/b720deeb-0041-4038-8889-7e7f13ff5cb1)

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/f288d2f4-99c0-4ccb-ac63-4005e2b4a7a0)

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/fefbeaed-3249-4250-8f1f-f8ddba8e4fd5)


	+ Thay đổi kích thước phông chữ, hay khung.

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/16642243-c0ba-46df-afa0-7c46a3d3d97f)
	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/4659f926-65a7-4093-9be7-e16da44e8b42)

	+ Tùy chỉnh , xác định thông tin định dạng số cho một giá trị trên `tab Number Format`

 	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/a6f06e7e-a022-4859-b9ef-2340152f001f)

- **Single Value Visualizations: timechart** *(Biểu đồ thời gian)* 
	+ Với lệnh biểu đồ thời gian *(timechart command)*, có thể thêm biểu đồ thu nhỏ và xu hướng
   
	+ `Sparkline` là một biểu đồ nội tuyến
			
		+ Nó được thiết kế để hiển thị các xu hướng dựa trên thời gian liên quan đến khóa chính

	+ Xu hướng cho thấy hướng mà các giá trị đang di chuyển

		+ Nó xuất hiện ở bên phải của một giá trị
 
    ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/b47b7dfd-a938-474f-a310-9b654b0f8c70)

 	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/24e62d50-0141-425e-b56a-f55284b39e42)

# Use the addtotals command

-  **Adding Totals Using Format Options** *(Thêm tổng số bằng cách sử dụng các tùy chọn định dạng)* 

	+ Tự động cộng tất cả các cột bằng cách sử dụng tùy chọn định dạng

	+ Khi sử dụng phương pháp này, bạn:

		+ Không thể chỉ ra cột nào để tính tổng; tất cả các cột luôn được tính tổng

		+ Không thể thêm thuộc tính
	
 	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/6d76ac18-6d7f-4f92-ba5a-3b749c2bed6c)

	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/92ec8043-0055-4098-8eb1-bec28bd109fa)![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/93f3a03f-08e6-4931-9124-66a780989c42)

	+ **summary Tab** *(Sử dụng tab tóm tắt)* , có thể thêm một hàng % vào cuối bảng thống kê

	+ **columms** *(Tất cả các cột)*  được sử dụng để tính tỷ lệ phần trăm – tất cả tỷ lệ phần trăm từ tất cả các cột cộng lại sẽ xấp xỉ bằng 100%

 	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/1e676995-a42e-466c-9f05-f2d13250ba52)

 	![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/96b18e91-e95a-41ea-ac12-147c864dd0b6)

- **Adding Totals Using addtotals Command** *(Thêm tổng số bằng cách sử dụng lệnh addtotals)* 

	+ Sử dụng lệnh `addtotals` để:

		+ Tính tổng tất cả hoặc chọn các trường số cho mỗi cột và đặt tổng ở hàng cuối cùng 

	  	+ Tính tổng tất cả hoặc chọn các trường số cho mỗi hàng và đặt tổng vào cột cuối cùng

	  ![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/cff09f33-61c2-4fad-b51a-463f4339d495)

 - **addtotals Command: Syntax** *(Cú pháp lện addtotals)* 

`addtotals [row=bool] [fieldname=field] [col=bool][labelfield=field] [label=string] field-list`

![ảnh](https://github.com/tatdatda04/Module_Splunk/assets/118095276/d6ed98f2-585e-43b2-bdca-203645a8c773)














 

