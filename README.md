# Build-recomendaton-system-with-movie-data
Trong bài này m sẽ sử dụng Colaborative filtering để xây dựng recomender system trên tập dữ liệu movie. Cụ thể là sử dụng thuật toán SVD trên thư viện surprise. 
## What is the recomender system?

Recomender system là một hệ thống gợi ý những item mà một user có thể thích. But how? Hệ thống sẽ sử dụng các dữ liệu trong quá khứ để dự báo **'rating'** hoặc **'preference'** mà user dành cho các item. **'Rating'** càng cao chứng tỏ user càng thích item đó. Recomender system sẽ lọc ra những item có rating cao nhất và hiển thị nó ra. Ví dụ, khi bạn xem phim trên netflix, netflix sẽ dựa vào những thông tin trong quá khứ của bạn( users) để hiển thị ra những bộ phim( items) mà bạn có thể thích. Điều tương tự cũng diễn ra khi bạn sử dụng facebook hay các trang thương mại điện tử

## Approaches
Có 2 cách tiếp cận chính đối với recomender system là **Collaborative Filtering** và **Content-based filtering**. Hai cách tiếp cận này khác nhau chủ yếu ở loại dữ liệu đầu vào. Collaborative Filtering model dử dụng dữ liệu phản hồi( feedback) của khách hàng( user) đỗi với items( ví dụ: star rating, thumb um/down,..) để làm dữ liệu đầu vào. Trong khi đó, Content-base filtering sử dụng các featrue của item để làm input. Ví dụ đối với recommend phim, feature của các bộ phim có thể là diễn viên,nội dung, thể loại, chi phí, tác giả, doanh thu,..
### Collaborative Filtering
Như ta đã biết, model này dử dụng bộ dữ liệu phản hồi của user. Dữ liệu đó có thể là **implicit feedback** hoặc **explicit feedback**. Explicit feedback là những phản hồi rất rõ ràng như star rating hay thumb up/ down. Trái lại, implicit feedback là những phản hồi mang tính tiềm ẩn ví dụ như số lần nghe một bài hát, số lần clicks, thời gian xem items,..

Chúng ta sẽ tiếp tục phân loại model này dựa trên cách model sử lý dữ liệu đầu vào
#### User- User
Y tưởng của thuật toán này là: hệ thống sẽ gợi ý item đối với user nếu user tương tự cũng thích item đó. Như vậy ta cần đo lường mức độ giống nhau giữa 2 user. Đại lượng này được tính từ lượng item mà 2 user này cùng có. 2 user càng có nhiều item chung và feedback đối với các item đó càng giống nhau thì 2 user càng giống nhau. Đại lượng này có thể là khoảng cách hoặc là correlation

Thuật toán này sẽ rất hiệu quả nếu số user nhơ hơn nhiều so với số item. Ngoài ra, hạn chế của thuật toán này là việc thêm một user mới sẽ rất đắt. Vì khi đó ta phải cập nhật lại tất cả những số liệu thể hiện mối quan giống nhau giữa các user.
#### Items- Items
Thuật toán này giống với thuật toán trên, chỉ đảo ngược vai trò giữa users  và itens.
Y tưởng của thuật toán này là: Nếu bạn thích items này thì có khả năng bạn cũng sẽ thích item kia. Hay nói cách khác, hệ thống sẽ gợi ý những item tương tự như item mà bạn đã thích. Sự giống nhau giữa 2 item được tính từ số lượng user mà 2 item cùng có

Hai thuật toán này có thể được minh họa qua hình sau:

![alt Recommender](https://takuti.github.io/Recommendation.jl/latest/assets/images/cf.png)
#### User - items
User - items là thuật toán kết hợp cả 2 loại trên. Thuật toán này có khá nhiều dạng nhưng phổ biến nhất là **Matrix Factorization**. Và trong bài này m sẽ sử dụng thuật toán SVD trong thư viện surprise để thực hiện Matrix Factorization. Để hiểu kĩ hơn thuật toán, mọi người có thể tham khảo tại đây [matrix_factorization](https://surprise.readthedocs.io/en/stable/matrix_factorization.html)

### Content-based filtering

Một trong những vấn đề chính của colaborative filtering là đối với những item hoặc user mới, ta sẽ không có đủ dữ liệu để đưa ra gợi ý chính xác. Hiện tượng này được gọi là **Cold start**

Để hạn chế vấn đề này ta có thể sử dụng một cách tiếp cận khác được gọi là Content- based filtering. Cách tiếp cận này giống hệt các thuật toán trước. Chỉ khác là, model này sử dụng dữ liệu content- based feature. Hay nói cách khác, mô hình sẽ sử dụng đặc điểm của các items để xác định mức độ giống nhau giữa các item. Nếu một user thích Item a thì khả năng là anh ta cũng sẽ thích các ite tương tự với item a.

Mô hình này tận dụng dữ liệu về item để cái thiện chất lượng model

### Hybrid Models and Deep Learning
Mô hình này sẽ sử dụng deep learning mdoel để kết hợp 2 cách tiếp cận trên, colaborative filtering và content-based filtering. Và đây cũng là một trong những thuật toán recomender tốt nhất hiện nay
### Tài liệu tham khảo
- [what-are-the-top-recommendation-engine-algorithms-used-nowadays](https://itnext.io/what-are-the-top-recommendation-engine-algorithms-used-nowadays-646f588ce639)
- [Recommender_system_wikipedia](https://en.wikipedia.org/wiki/Recommender_system)
