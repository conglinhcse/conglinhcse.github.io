---
layout: post
title: Giới thiệu cơ sở dữ liệu
subtitle: Cơ sở dữ liệu là gì?
tags: [database]
comments: true
---

Công nghiệp 4.0 đang bùng nổ trên khắp thế giới. Biểu hiện rõ nhất có thể thấy đó chính là lượng dữ liệu được sinh đang tăng chóng mặt theo từng giây. Vì thế lưu trữ dữ liệu đang trở thành vấn đề đặc biệt đáng quan tâm. Hôm nay, mình sẽ giới thiệu qua về cơ sở dữ liệu. Bài viết sẽ trình bày những công nghệ từ cổ đại nhất cho đến hiện đại nhất.

## Lưu trữ dữ liệu bằng tệp tin riêng lẻ (file-based)

Đây là cách lưu trữ dữ liệu truyền thống nhất, dữ liệu được lưu trên một hoặc nhiều tệp tin riêng lẻ. Và mỗi tệp tin được xử lý thông qua một ứng dụng máy tính duy nhất được viết đặc thù theo quy ước lưu trữ dữ liệu trong tệp tin.

Vì đây là cách lưu trữ khá cổ điển, nên có nhiều yếu điểm, có thể kể đến như:

- Dư thừa dữ liệu (data redundancy): các dữ liệu trùng nhau có thể bị lưu trữ trên nhiều tệp tin khác nhau.  Ví dụ như tập dữ liệu về khách hàng được lưu trữ thành 2 tệp tin độc lập cho phòng marketing và phòng kế toán quản lý. Rõ ràng, điều này gây tiêu hao bộ nhớ một cách vô ích.

- Không thống nhất dữ liệu (data inconsistency): cùng một dữ liệu có thể tồn tại ở nhiều bản sao chép (copy) khác nhau do các phần mềm khác nhau xử lý và gây xung đột (conflict) cho hệ thống. Chẳng những thế, dữ liệu còn được lưu trên file theo những quy tắc không đồng nhất, gây nhập nhằng cho người lập trình xử lý dữ liệu.

Cách lưu trữ này chỉ phù hợp với với các cơ sở dữ liệu rất nhỏ. Nếu bạn là mới làm quen với lập trình, rất có thể đây là giải pháp lưu trữ được chọn cho phầm mềm đầu tay phải không nhỉ?

## Lưu trữ dữ liệu bằng tệp tin dùng chung (shared file)

Để khắc phục các yếu điểm trên, cách thức lưu trữ dữ liệu dạng shared file đã ra đời. Cách thức này cho phép chia sẽ dữ liệu giữa các ứng dựng với nhau, từ đó thống nhất được dữ liệu và giảm bớt tính dư thừa dữ liệu.

Tuy nhiên, cách thức này vẫn còn những yếu điểm khác:

- Cấu trúc dữ liệu cứng nhắc (rigid data structure): cấu trúc file phù hợp với phần mềm này có thể sẽ không phù hợp với phần mềm khác.

- Phần mềm bị phụ thuộc vào dữ liệu (physical data dependency): theo thời gian, có thể nhu cầu lưu trữ dữ liệu sẽ thay đổi dẫn đến cần phải thay đổi cấu trúc file, và điều này tương đương ta phải thay đổi toàn bộ các chương trình xử lý cơ sở dữ liệu này.

- Không hỗ trợ điều khiển truy suất dữ liệu đồng thời (no support of concurrency control): trong khi một tệp dữ liệu đang được xử lý bởi một ứng dụng, thì tệp đó sẽ không cho phép các ứng dụng khác truy suất.

## Cơ sở dữ liệu dạng phân cấp (hierarchical data structure)

![hierarchical](/img/database/hierarchical-dbms-model.webp)

Nếu đã học môn cấu trúc dữ liệu và giải thuật, chắc hẳn bạn sẽ nhận ra ngay cấu trúc dữ liệu cây (tree) quen thuộc. Đúng rồi, chính là nó đó.

Theo mô hình này thì cơ sở dữ liệu được tổ chức theo mô hình cây, phân nhánh từ trên xuống. Các dữ liệu được biểu hiện bằng các nút khác nhau, mỗi một nút chính là một thực thể dữ liệu. Mối liên hệ trong dữ liệu chỉ thể hiện giữa nút mẹ và nút con, cây thư mục từ từ phân cấp, một nút mẹ có thể có nhiều nút con, nhưng mỗi nút con chỉ xuất phát từ một nút mẹ. Việc lưu trữ dữ liệu dạng phân cấp rất cần thiết trong một số trường hợp, ví dụ như menu phân nhiều cấp hay comment hỗ trợ reply lồng nhau.



## Cơ sở dữ liệu dạng mạng 

![network](/img/database/network-dbms-model.webp)

Trong mô hình này thì các file riêng biệt được tập hợp lại trong một hệ thống file phẳng gọi là bản ghi. Các bản ghi này sẽ được phân loại theo cùng một kiểu và tập hợp lại gọi là kiểu thực thể dữ liệu. Giữa các kiểu thực thể dữ liệu này được kết nối với nhau theo quan hệ mẹ con. Ưu điểm của mô hình này chính là dễ biểu đạt mô hình dữ liệu phức tạp, nhìn vào là có thể hiểu được cơ sở dữ liệu muốn nói đến là gì. Tuy vậy, nó cũng có những hạn chế nhất định đó là khả năng truy xuất của mô hình cơ sở dữ liệu dạng mạng khá chậm, không phù hợp cho việc quản lý cơ sở dữ liệu ở quy mô lớn.

Chắc hẳn sẽ có các bạn hỏi rằng: "Ủa thằng này y chang cơ sở dữ liệu dạng phân cấp mà?".  Khác đấy:

- CSDL dạng phân cấp sử dụng cấu trúc dữ liệu cây để hiện thực, mối quan hệ giữa các nút là one to many, vì thế việc truy suất dữ liệu khó khăn và ít linh hoạt

- CSDL dạng mạng sử dụng cấu trúc dữ liệu đồ thị để hiện thực, mối quan hệ giữa các nút là many to many, vì thế tốn nhiều bộ nhớ hơn để lưu trữ dữ liệu nhưng lại dễ dàng truy suất dữ liệu và linh hoạt hơn.

## Cơ sở dữ liệu quan hệ (relation database)

Cơ sở dữ liệu quen thuộc với quần chúng nhân dân là đây. Nếu bạn không lớn lên ở vùng quê, thì chắc chắn là đã được học cái này ở cấp 3 rồi, chính là thằng Microsoft Access đó. Ngày trước mình nhớ phải đi thi bằng tin học B gì đó về cái này để được cộng điểm thi tốt nghiệp cấp 3 :v.

![relation](/img/database/sql-database-tools.webp)

Cấu trúc cơ sở dữ liệu quan hệ:

- Dữ liệu được thể hiện thông qua các bảng, mỗi bảng đại diện cho một nhóm các thực thể dữ liệu (như nhân viên, đơn hàng ...)
- Mỗi bảng bao gồm các hàng và các cột. Các cột là thuộc tính của thực thể dữ liệu (như tên, tuổi .. của nhân viên). Mỗi hàng là một bộ dữ liệu tương ứng với các cột, đại diện cho một cá thể (như thông tin của nhân viên A).

Hầu hết các các CSDL quan hệ nổi tiếng như SQL server, MySQL, PostgreSQL đều sử dụng ngôn ngữ SQL cho các thao tác thêm (insert), xóa (delete), sửa (update) dữ liệu.

//ACID

## Cơ sở dữ liệu hướng tài liệu (document store database)

MongoDB, thằng này không biết sao chứ đi đâu mình cũng nghe tên ẻm được sướng lên, không biết có phốt gì không mà hot thế :v.

![document](/img/database/document-database.png)

Cơ sở dữ liệu hướng tài liệu, một thiết kế riêng biệt cho việc lưu trữ tài liệu dạng văn kiện JSON, BSON hoặc XML. Vì là cấu trúc dữ liệu không ràng buộc khác với SQL, các CSDL này không đòi hỏi người dùng tự tạo bảng nhập liệu trước khi nhập dữ liệu vào. Các tài liệu có thể chứa bất kì dữ liệu nào. CSDL dạng này có các cặp khoá – giá trị nhưng cũng có đính kèm các trị số siêu dữ liệu (metadata) giúp việc truy vấn (query) dễ dàng hơn. CSDL hướng tài liệu rất linh hoạt, có thể xử lí dữ liệu nửa cấu trúc và không cấu trúc rất tốt. CSDL dạng lưu trữ tài liệu hy sinh các yếu tố ACID để đổi lấy sự linh hoạt. Ngoài ra, việc truỵ vấn chỉ có thể được thực hiện trong từng tài liệu, không thể truy vấn dữ liệu trên nhiều tài liệu khác nhau.

## Cơ sở dữ liệu  dạng khoá – giá trị

CSDL Key-value lưu trữ dữ liệu dưới dạng key (là một chuỗi duy nhất) liên kết với value có thể ở dạng chuỗi văn bản đơn giản hoặc các tập, danh sách dữ liệu phức tạp hơn. Quá trình tìm kiếm dữ liệu thường sẽ được thực hiện thông qua key, điều này dẫn đến sự hạn chế về độ chính xác.

Một "key" là một định danh độc nhất được gán cho một giá trị. Keys có thể là bất cứ thứ gì cho phép bởi DBMS. Trong Redis, keys có thể là một hàm nhị phân lên tới 512MB

"Giá trị" có thể được lưu trữ dưới dạng blob (Là kiểu dữ liệu của một cột trong bảng RDBMS, có thể lưu ảnh lớn hoặc dữ liệu văn bảng như những thuộc tính.) và không cần schema định sẵn.. Các gía trị này có thể được gán bất cứ loại giá trị nào: số, chuỗi giá trị, bộ đếm, JSON, XML, HTML, PHP,, nhị phân, hình ảnh, video ngắn, danh sách ...

![keyvalue](/img/database/key-value-database.jpg)

Dạng CSDL này có rất nhiều lợi thế. Nó rất linh hoạt và có thể xử lí nhiều loại dữ liệu một cách nhanh chóng. Các chìa khoá được dùng để truy xuất thẳng tới các giá trị tìm kiếm, mà không cần thông qua quá trình index, giúp quá trình tìm kiếm diễn ra nhanh chóng. 

Tính linh hoạt của CSDL dạng key – value bị đánh đổi bởi tính chính xác. Hầu như rất khó để truy xuất giá trị chính xác từ CSDL dạng này vì dữ liệu được lưu trữ theo blob, nên kết quả trả về hầu như đều theo blob. Điều này gây ra khó khăn khi báo cáo số liệu hoặc cần chỉnh sửa một phần của các giá trị. Cuối cùng, không phải objects nào cũng có thể được cấu hình thành cặp chìa khoá – giá trị được.

## Cơ sở dữ liệu phi quan hệ lưu trữ theo dạng cột

Mô hình wide – column là một dạng lưu CSDL phi quan hệ lưu trữ theo dạng cột. Mô hình này có vài điểm tương đồng với mô hình key – value nhưng cũng có vài tính chất của dạng CSDL quan hệ.

Mô hình wide – column dựa trên khái niệm keyspace thay vì schema. Một keyspace bao gồm nhiều cụm column (tương tự như table nhưng linh hoạt hơn về cấu trúc), mỗi cụm bao gồm nhiều hàng và nhiều cột riêng biệt. Mỗi hàng không cần phải có số lượng hoặc loại cột.

![column](/img/database/wide-column-database.png)

Loại CSDL này có cả lợi ích của CSDL quan hệ và phi quan hệ, có thể xử lí dữ liệu cấu trúc và phi cấu trúc, đồng thời cũng dễ dàng nâng cấp. So với CSDL quan hệ, khả năng mở rộng theo chiều ngang cũng dễ dàng và nhanh chóng hơn. CSDL dạng cột có khả năng nén tốt hơn CSDL dạng dòng. Đồng thời, data set lớn có thể dễ dàng duyệt hơn. Mô hình wide – column có khả năng xử lí tốt các yêu cầu truy xuất tập trung. CSDL dạng cột dễ dàng update theo cụm, bù lại việc upload và update số liệu cá nhân rất khó.

## Cơ sở dữ liệu dạng bộ máy tìm kiếm 

Elasticsearch về cốt lõi là một bộ máy tìm kiếm và không hoàn toàn là là CSDL chuyên biệt như các loại trên, nhưng ngày càng được giới developers tận dụng để giảm thiểu độ lag khi tìm kiếm thông tin. Elasticsearch được xem như một CSDL dạng phi quan hệ, dựa trên nền tảng lưu trữ dữ liệu dạng văn kiện, thiết kế chuyên biệt để tối ưu hoá lưu trữ và trao đổi dữ liệu nhanh chóng.

![column](/img/database/elasticsearchscylla.jpg)

Elasticsearch có khả năng mở rộng cao, với schema linh hoạt và tốc độ trả về thông số lưu trữ nhanh, hỗ trợ khả năng tìm kiếm nâng cao: tìm kiếm full text, khuyến nghị các kết quả tìm kiếm, và hỗ trợ các thông tin tìm kiếm phức tạp.

Elasticsearch được sử dụng với hình thức thay thế hoặc bổ trợ cho CSDL có sẵn hơn là độc lập. Elasticsearch còn có nhược điểm là độ ổn định và bảo mật kém.
