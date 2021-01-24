# spark_mapreduce_demtansuattu
Spark
1. Giới thiệu về Apache Spark
- Apache Spark là một framework mã nguồn mở tính toán cụm.  Spark cung cấp một giao diện để lập trình toàn bộ các cụm với tính song song dữ liệu ngầm và khả năng chịu lỗi. Ban dầu được phát triển bởi Đại học California, AMPlab sau đó được foundation duy trì phát triển từ 2013 cho đến nay.
- Việc tính toán của Spark được thực hiện trong bộ nhớ trong (in-memories) hay trong RAM. Đồng thời việc tính toán được thực hiện cùng lúc trên nhiều máy tính khác nhau nên Spark có tốc độ xử lý nhanh.
- Spark cho phép xử lý dữ liệu theo thời gian thực, vừa nhận dữ liệu từ các nguồn khác nhau đồng thời thực hiện ngay việc xử lý trên dữ liệu vừa nhận được ( Spark Streaming).
- Spark không có hệ thống file của riêng mình, nó sử dụng hệ thống file khác như: HDFS, Cassandra, S3,…. Spark hỗ trợ nhiều kiểu định dạng file khác nhau (text, csv, json…) đồng thời nó hoàn toàn không phụ thuộc vào bất cứ một hệ thống file nào.
2. Thành phần của Spark
 Spark có 5 thành phần chính : Spark Core, Spark Streaming, Spark SQL, MLlib và GraphX, trong đó:
Spark Core: là nền tảng của các phần còn lại đảm nhận vai trò thực hiện tính toán trong bộ nhớ trong và tham chiếu các dữ liệu được lưu trữ ở bên ngoài, các thành phần còn lại muốn thực hiện phải thông qua Spark Core
SparkSQL: cung cấp một kiểu data abstraction mới (SchemaRDD) nhằm hỗ trợ cho cả kiểu dữ liệu có cấu trúc (structured data) và dữ liệu nửa cấu trúc (semi-structured data – thường là dữ liệu dữ liệu có cấu trúc nhưng không đồng nhất và cấu trúc của dữ liệu phụ thuộc vào chính nội dung của dữ liệu ấy). Spark SQL hỗ trợ DSL (Domain-specific language) để thực hiện các thao tác trên DataFrames bằng ngôn ngữ Scala, Java hoặc Python và nó cũng hỗ trợ cả ngôn ngữ SQL với giao diện command-line và ODBC/JDBC server.
Spark Streaming được sử dụng để thực hiện việc phân tích stream bằng việc coi stream là các mini-batches và thực hiệc kỹ thuật RDD transformation đối với các dữ liệu mini-batches này. Qua đó cho phép các đoạn code được viết cho xử lý batch có thể được tận dụng lại vào trong việc xử lý stream, làm cho việc phát triển lambda architecture được dễ dàng hơn. Tuy nhiên điều này lại tạo ra độ trễ trong xử lý dữ liệu (độ trễ chính bằng mini-batch duration) và do đó nhiều chuyên gia cho rằng Spark Streaming không thực sự là công cụ xử lý streaming giống như Storm hoặc Flink.
MLlib (Machine Learning Library): MLlib là một nền tảng học máy phân tán bên trên Spark do kiến trúc phân tán dựa trên bộ nhớ. Theo các so sánh benchmark Spark MLlib nhanh hơn 9 lần so với phiên bản chạy trên Hadoop (Apache Mahout)
GrapX: Grapx là nền tảng xử lý đồ thị dựa trên Spark. Nó cung cấp các Api để diễn tảcác tính toán trong đồ thị bằng cách sử dụng Pregel Api.
Những điểm nổi bật của Spark
•	Xử lý dữ liệu: Spark xử lý dữ liệu theo lô và thời gian thực
•	Tính tương thích: Có thể tích hợp với tất cả các nguồn dữ liệu và định dạng tệp được hỗ trợ bởi cụm Hadoop.
•	Hỗ trợ ngôn ngữ: hỗ trợ Java, Scala, Python và R.
•	Phân tích thời gian thực:
o	Apache Spark có thể xử lý dữ liệu thời gian thực tức là dữ liệu đến từ các luồng sự kiện thời gian thực với tốc độ hàng triệu sự kiện mỗi giây. Ví dụ: Data Twitter chẳng hạn hoặc luợt chia sẻ, đăng bài trên Facebook. Sức mạnh Spark là khả năng xử lý luồng trực tiếp hiệu quả.
o	Apache Spark có thể được sử dụng để xử lý phát hiện gian lận trong khi thực hiện các giao dịch ngân hàng. Đó là bởi vì, tất cả các khoản thanh toán trực tuyến được thực hiện trong thời gian thực và chúng ta cần ngừng giao dịch gian lận trong khi quá trình thanh toán đang diễn ra.
•	Mục tiêu sử dụng:
o	Xử lý dữ liệu nhanh và tương tác
o	Xử lý đồ thị
o	Công việc lặp đi lặp lại
o	Xử lý thời gian thực
o	joining Dataset
o	Machine Learning
o	Apache Spark là Framework thực thi dữ liệu dựa trên Hadoop HDFS. Apache Spark không thay thế cho Hadoop nhưng nó là một framework ứng dụng. Apache Spark tuy ra đời sau nhưng được nhiều người biết đến hơn Apache Hadoop vì khả năng xử lý hàng loạt và thời gian thực.
MapReduce
MapReduce được chia thành hàm là Map và Reduce. Những hàm này được định nghĩa bởi người dùng và là hai giai đoạn liên tiếp trong quá trình xử lý dữ liệu.

+ Map nhận input là tập các cặp khóa/giá trị và output là tập các cặp khóa/giá trị trung gian và ghi xuống đĩa cứng và thông báo cho Reduce nhận dữ liệu đọc.

+ Reduce sẽ nhận khóa trung gian I và tập các giá trị ứng với khóa đó, ghép nối chúng lại để tạo thành một tập khóa nhỏ hơn. Các cặp khóa/giá trị trung gian sẽ  được đưa vào cho hàm reduce thông qua một con trỏ vị trí (iterator). Điều này cho phép ta có thể quản lý một lượng lớn danh sách các giá trị để phù hợp với bộ nhớ.

Thực chất giữa bước map và reduce còn có một bước phụ mà bước này thực hiện song song với bước reduce đó là shuffle. Tức là sau khi map thực hiện xong toàn bộ công việc của mình,  output của map được đặt rải rác trên các cluster khác nhau nên shuffle sẽ làm nhiệm vụ thu thập các cặp khóa-giá trị trung gian do map sinh ra mà có cùng khóa để chuyển qua cho reduce thực hiện tiếp công việc của mình.
