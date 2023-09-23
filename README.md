# Cache, và cách sử dụng cache trong dự án spring

Spring Boot là một dự án được xây dựng dựa trên Spring Framework, cung cấp cách thức thiết lập, định cấu hình và chạy cả ứng dụng đơn giản và ứng dụng dựa trên web dễ dàng hơn và nhanh hơn. Đây là một trong những framework phổ biến đối với các nhà phát triển hiện nay vì môi trường sẵn sàng sản xuất nhanh chóng, cho phép các nhà phát triển tập trung trực tiếp vào logic thay vì phải vật lộn với cấu hình và thiết lập. Nó là một framework dựa trên microservice được sử dụng để tạo một ứng dụng dựa trên Spring độc lập mà chúng ta có thể chạy với cấu hình Spring tối thiểu.

## Tính năng

- Không có yêu cầu về cấu hình XML nặng .
- Việc phát triển và thử nghiệm ứng dụng Spring Boot thật dễ dàng vì nó cung cấp công cụ dựa trên CLI và nó cũng có các máy chủ HTTP nhúng như Tomcat, Jetty, v.v.
- Vì nó sử dụng quy ước về cấu hình nên nó tăng năng suất và giảm thời gian phát triển.

![image](https://github.com/thangdtph27626/cache/assets/109157942/8e4efa1f-4bb3-432b-abfb-d73c6e2919d8)

Bộ đệm là bất kỳ vị trí lưu trữ tạm thời nào nằm giữa ứng dụng và cơ sở dữ liệu lâu dài hoặc ứng dụng của bên thứ ba lưu trữ dữ liệu được truy cập thường xuyên nhất hoặc gần đây nhất để có thể phục vụ các yêu cầu trong tương lai về dữ liệu đó nhanh hơn. Nó tăng hiệu suất truy xuất dữ liệu bằng cách giảm nhu cầu truy cập vào lớp lưu trữ chậm hơn bên dưới. Truy cập dữ liệu từ bộ nhớ luôn nhanh hơn so với việc lấy dữ liệu từ cơ sở dữ liệu. Bộ nhớ đệm giúp các đối tượng, hình ảnh và dữ liệu được truy cập thường xuyên đến gần nơi bạn cần hơn, tăng tốc truy cập bằng cách không truy cập cơ sở dữ liệu hoặc bất kỳ ứng dụng bên thứ ba nào nhiều lần cho cùng một dữ liệu và tiết kiệm chi phí tiền tệ. Dữ liệu không thay đổi thường xuyên có thể được lưu trữ.

## Các loại bộ nhớ đệm

Có 4 loại bộ nhớ đệm chủ yếu:

- CDN Caching
- Database Caching
- In-Memory Caching
- Web server Caching

  ### 1. CDN Caching

network (CDN) là một nhóm các máy chủ phân tán giúp tăng tốc độ phân phối nội dung web bằng cách đưa nội dung đó đến gần hơn với vị trí của người dùng. Các trung tâm dữ liệu trên toàn cầu sử dụng bộ nhớ đệm để phân phối nội dung Internet đến thiết bị hoặc trình duyệt hỗ trợ web nhanh hơn thông qua máy chủ ở gần bạn, giảm tải cho nguồn ứng dụng và cải thiện trải nghiệm người dùng. CDN lưu vào bộ nhớ đệm nội dung như trang web, hình ảnh và video trong máy chủ proxy gần vị trí thực tế của bạn.

### 2. Database Caching

 Database Caching cải thiện khả năng mở rộng bằng cách phân phối khối lượng công việc truy vấn từ hệ thống phụ trợ đến nhiều hệ thống giao diện người dùng. Nó cho phép linh hoạt trong việc xử lý dữ liệu. Nó có thể giảm đáng kể độ trễ và tăng thông lượng cho khối lượng công việc ứng dụng đọc nhiều bằng cách tránh truy vấn cơ sở dữ liệu quá nhiều.

### 3. In-Memory Caching 

In-Memory Caching  tăng hiệu suất của ứng dụng. Bộ đệm trong bộ nhớ là một kho lưu trữ truy vấn phổ biến, do đó, giúp giảm bớt khối lượng công việc đọc cơ sở dữ liệu. Bộ đệm của Redis là một trong những ví dụ về bộ đệm trong bộ nhớ. Redis được phân phối và công cụ bộ đệm nâng cao cho phép sao lưu và khôi phục cơ sở vật chất. Bộ nhớ đệm trong bộ nhớ cung cấp chức năng truy vấn ngoài bộ nhớ đệm.

### 4. Web server Caching

Web server Caching lưu trữ dữ liệu, chẳng hạn như bản sao của trang web do máy chủ web cung cấp. Nó được lưu vào bộ đệm hoặc lưu trữ trong lần đầu tiên người dùng truy cập trang và khi lần tiếp theo người dùng yêu cầu cùng một trang, nội dung sẽ được gửi từ bộ đệm, giúp máy chủ gốc không bị quá tải. Nó tăng cường đáng kể tốc độ phân phối trang và giảm bớt công việc cần thực hiện bởi máy chủ phụ trợ.

##   các Annotations  Cache trong spring boot 

### 1. @Cacheable

Cách đơn giản nhất để kích hoạt hành vi bộ đệm cho một phương thức là đánh dấu nó bằng @Cacheable và tham số hóa nó bằng tên của bộ đệm nơi kết quả sẽ được lưu trữ. 

```
@Cacheable(“name”)

public String getName(Customer customer) {…}
```

Lệnh gọi getName() trước tiên sẽ kiểm tra tên bộ đệm trước khi thực sự gọi phương thức và sau đó lưu kết quả vào bộ nhớ đệm. Chúng ta cũng có thể áp dụng điều kiện trong chú thích bằng cách sử dụng thuộc tính condition:

```
@Cacheable(value=”Customer”, condition=”#name.length<10″)  

public Customer findCustomer(String name)  {…}  
```

### 2. @Cache Evict

Vì bộ đệm có kích thước nhỏ. Chúng tôi không muốn đưa vào bộ đệm những giá trị mà chúng tôi không cần thường xuyên. Bộ nhớ đệm có thể phát triển khá lớn, khá nhanh. Chúng ta có thể sử dụng chú thích @CacheEvict để xóa các giá trị để các giá trị mới có thể được tải lại vào bộ đệm:

```
@CacheEvict(value=”name”, allEntries=true)

public String getName(Customer customer) {…}
```

Nó cung cấp một tham số có tên allEntries để loại bỏ tất cả các mục nhập thay vì một mục nhập dựa trên khóa.

### 3. @CachePut

 @CachePut có thể cập nhật nội dung của bộ đệm mà không can thiệp vào việc thực thi phương thức. 

```
@CachePut(value=”name”)

public String getName(Customer customer) {…}
```
 @CachePut cập nhật có chọn lọc các mục bất cứ khi nào chúng tôi thay đổi chúng để tránh xóa quá nhiều dữ liệu khỏi bộ đệm. Một trong những điểm khác biệt chính giữa chú thích @Cacheable và @CachePut là @Cacheable bỏ qua việc thực thi phương thức trong khi @CachePut chạy phương thức và lưu kết quả vào bộ đệm.


 ### 4. @Caching

 @Caching được sử dụng trong trường hợp chúng ta muốn sử dụng nhiều chú thích cùng loại trên cùng một phương thức.

 ```
@CacheEvict(“name”)

@CacheEvict(value=”directory”, key=”#customer.id”)

public String getName(Customer customer) {…}

```

Mã được viết ở trên sẽ không biên dịch được vì Spring-Boot không cho phép khai báo nhiều chú thích cùng loại cho một phương thức nhất định.

```
@Caching(evict = {  

 @CacheEvict(“name”),  

 @CacheEvict(value=”directory”, key=”#customer.id”) })

public String getName(Customer customer) {…}
```
Như được hiển thị trong đoạn mã trên, chúng ta có thể sử dụng nhiều chú thích bộ nhớ đệm với @Caching và tránh các lỗi biên dịch.

### 5. @CacheConfig

@CacheConfig, chúng ta có thể đơn giản hóa một số cấu hình bộ đệm vào một vị trí duy nhất ở cấp lớp để không phải khai báo mọi thứ nhiều lần.

```
@CacheConfig(cacheNames={“name”})

public class CustomerData {

  @Cacheable

   public String getName(Customer customer) {…}
```


## Bộ nhớ đệm có điều kiện


Đôi khi, một phương thức có thể không phù hợp để lưu vào bộ nhớ đệm mọi lúc. Các chú thích bộ đệm hỗ trợ chức năng đó thông qua tham số có điều kiện có biểu thức SpEL được đánh giá là đúng hoặc sai. Nếu đúng, phương thức này sẽ được lưu vào bộ đệm, nếu không nó sẽ hoạt động như thể phương thức đó không được lưu vào bộ đệm, phương thức này được thực thi mọi lúc bất kể giá trị nào trong bộ đệm hoặc đối số nào được sử dụng. 


```
@Cacheable(value=”name”, condition=”#customer.name ==  ‘Megan’ “)

public String getName(Customer customer) {…}
```

Phương thức trên sẽ được lưu vào bộ đệm, chỉ khi tên đối số bằng Megan.

## Parameter


Chúng ta cũng có thể kiểm soát bộ nhớ đệm dựa trên đầu ra của phương thức thay vì đầu vào thông qua tham số trừ khi :

```
@Cacheable(value=”name”, unless=”#result.length() < 20″)

public String getName(Customer customer) {….}
```
Chú thích ở trên sẽ lưu địa chỉ vào bộ đệm trừ khi chúng ngắn hơn 20 ký tự. Điều quan trọng là phải biết điều kiện và các tham số trừ khi có thể được sử dụng cùng với tất cả các chú thích bộ nhớ đệm.

## Cache Dependency

Nếu chúng ta muốn kích hoạt cơ chế bộ đệm trong ứng dụng Spring Boot, chúng ta cần thêm phụ thuộc bộ đệm vào tệp pom.xml. Nó cho phép lưu vào bộ đệm và định cấu hình CacheManager.
```
<dependency>  

     <groupId>org.springframework.boot</groupId>  

    <artifactId>spring-boot-starter-cache</artifactId>  

</dependency>
```
