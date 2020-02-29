### Leetcode Biweekly Contest 20
#### Leetcode 1356
**Độ khó**: Dễ
**Điểm** 3
**Đề bài**: Cho 1 mảng số nguyên *arr*. Bạn hãy sắp xếp mảng số nguyên theo thứ tự tăng dần bằng số lượng bit 1 trong biểu diễn nhị phân của nó, trong trường hợp có hai hoặc nhiều hơn các số có cùng số bit 1 trong biểu diễn nhị phân thì sắp xếp các số này theo thứ tự tăng dần.
**Test mẫu**:
| Input                                     | Output                              | Giải thích                                                                                   |
|-------------------------------------------|-------------------------------------|----------------------------------------------------------------------------------------------|
| arr = [0,1,2,3,4,5,6,7,8]                 | [0,1,2,4,8,3,5,6,7]                 | Số 0 có 0 bit 1 trong biểu diễn nhị phân. Số 1, 2, 4, 8 có cùng số bit nên sắp xếp tăng dần. |
| arr = [1024,512,256,128,64,32,16,8,4,2,1] | [1,2,4,8,16,32,64,128,256,512,1024] | Tất cả các số có cùng 1 bit trong biểu diễn nhị phân. Chỉ cần sắp xếp tăng dần.              |
| arr = [10000,10000]                       | [10000, 10000]                      |                                                                                              |
| arr = [2,3,5,7,11,13,17,19]               | [2,3,5,17,7,11,13,19]               |                                                                                              |
**Ràng buộc**:
$1 \leq arr.length \leq 500$.
$0 \leq arr[i] \leq 10^4$.
**Gợi ý cách giải**: Đầu tiên để tính số bit 1 trong biểu diễn nhị phân của 1 số nguyên thì ta có thể chuyển nó thành 1 sâu nhị phân, sau đó đến số ký tự 1 trong biểu diễn là xong. Trong python thì có thể dùng hàm *bin()* để làm điều này, hoặc phương án nhanh hơn là sử dụng [bitwise](https://www.java67.com/2016/01/how-to-count-number-of-1s-in-given-bit-sequence-in-java.html) (Tuy nhiên bài này giới hạn số cho quá nhỏ nên cách này không quá cần thiết).
Tiếp theo chỉ cần viết một hàm so sánh và đưa vào hàm sort là xong. Gọi hàm tính số bit 1 là $f(x)$, khi đó để so sánh 2 phần tử $x$ và $y$ thì ta chỉ cần so sánh $(f(x), x)$ và $(f(y), y)$.

#### Leetcode 1357
**Độ khó**: Trung bình.
**Điểm** 4.
**Đề bài**:
Một siêu thị đang có chương trình giảm giá cho mỗi $n$ khách hàng.
Các mặt hàng trong siêu thị sẽ có *id* của mặt hàng thứ $i$ là __products[i]__ và giá của mỗi sản phẩm đó là __prices[i]__.
Cứ mỗi khách hàng thứ $n$ đến mua hàng thì sẽ nhận được ưu đãi __discount__ vào hóa đơn. Khi đó ví dụ giá trị hóa đơn là $x$ thì hóa đơn sẽ được giảm giá xuống còn $x - (discount * x) / 100$. Và sau đó hệ thống bắt đầu đếm lại từ đầu.
Mỗi hóa đơn bao gồm 2 phần, sản phẩm mà khách hàng mua và số lượng của chúng, __product[i]__ là *id* sản phẩm mà khách hàng mua và __amount[i]__ là số lượng sản phẩm tương ứng mà khách hàng đã mua.
Bài toán yêu cầu viết class __Cashier__ bao gồm 2 phương thức:
* __Cashier(int n, int discount, int[] products, int[] prices)__: Khởi tạo đối tượng với danh sách sản phẩm, giá, và thông tin của chương trình khuyễn mãi.
* __double getBill(int[] product, int[] amount)__: Trả về giá trị hóa đơn sau khi đã giảm giá (nếu có).

**Test mẫu**
**Input**:
$["Cashier","getBill","getBill","getBill","getBill","getBill","getBill","getBill"]$
$[[3,50,[1,2,3,4,5,6,7],[100,200,300,400,300,200,100]]$,
$[[1,2],[1,2]]$, $[[3,7],[10,10]]$,
$[[1,2,3,4,5,6,7],[1,1,1,1,1,1,1]]$,
$[[4],[10]],[[7,3],[10,10]]$ ,$[[7,5,3,1,6,4,2],[10,10,10,9,9,9,7]]$,
$[[2,3,5],[5,3,2]]]$
**Output**:
$[null,500.0,4000.0,800.0,4000.0,4000.0,7350.0,2500.0]$
**Giải thích**:
Cashier cashier = new Cashier(3,50,[1,2,3,4,5,6,7],[100,200,300,400,300,200,100]);
**cashier.getBill([1,2],[1,2]);**                        // return 500.0, giá trị hóa đơn = 1 * 100 + 2 * 200 = 500.
**cashier.getBill([3,7],[10,10]);**                      // return 4000.0
**cashier.getBill([1,2,3,4,5,6,7],[1,1,1,1,1,1,1]);**    // return 800.0, giá trị hóa đơn là 1600, tuy nhiên đây là người mua hàng thứ 3 nên được giảm giá 50 %. Hệ thống lúc này bắt đầu đếm lại.
**cashier.getBill([4],[10]);**                           // return 4000.0
**cashier.getBill([7,3],[10,10]);**                      // return 4000.0
**cashier.getBill([7,5,3,1,6,4,2],[10,10,10,9,9,9,7]);** // return 7350.0, tương tự, người này được giảm giá 50%. 
**cashier.getBill([2,3,5],[5,3,2]);**                    // return 2500.0

**Ràng buộc**:
* $1 \leq n \leq 10^4$
* $0 \leq n \leq 100$
* $1 \leq products.length \leq 200$
* $1 \leq products[i] \leq 200$
* tất cả các giá trị trong mảng __products__ đều phân biệt.
* $prices.length == products.length$
* $1\leq prices[i] \leq 1000$
* $product.length \leq products.length$
* __product[i]__ luôn nằm trong mảng products.
* $amount.length == product.length$
* $1 \leq amount[i] \leq 1000$
* Có tối đa 1000 lới gợi tới hàm __getBill__


**Phương án giải quyết**: Đây là một bài mà mọi thứ đề bài cho rất rõ ràng, ta sẽ chỉ cần thêm một biến đếm số khách hàng đã vào mua hàng, biến đếm này cứ chia hết cho n thì ta sẽ giảm giá, ngược lại thì không giảm giá. Một điều lưu ý là *id* hàng là một giá trị bất kì, do đó để tìm nhanh giá của một sản phẩm có *id* bất kì thì ta sẽ sử dụng **hashmap** (hoặc dict ở trên Python).

#### Leetcode 1358
**Độ khó**: Trung bình.
**Điểm**: 5
**Đề bài**: Cho 1 xâu s chỉ chứa các ký tự a, b, c. Tính số xâu con của s chứa ít nhất 1 ký tự a, 1 ký tự b, 1 ký tự c.
**Test mẫu**:
| Input | Output |
|--------------|--------|
| s = "abcabc" | 10 |
| s = "aaacb" | 3 |
| s = "aaaaa" | 0 |
**Ràng buộc**:
* $3 \leq s.length \leq 50000$
* s chỉ chứa các ký tự a, b, c.

**Phương án giải quyết**: Đây là bài toán khó nhất trong đề này, ràng buộc để ở mức nhỏ nhưng vẫn yêu cầu một thuật toán tối ưu(2 bài trước thích code thể nào cũng được, miễn sao ra đúng kết quả). 
Phương án đầu tiên ta nghĩ đến đó là xét mọi xâu con có thể của s, sau đó kiểm tra xem xâu con này có thỏa mãn hay không. Với xâu s có kích thước $n$ thì số lượng xâu phải xét sẽ tương đương $O(n^2)$. Để kiểm tra xem xâu thỏa mãn hay không thì ta sẽ đếm số lượng ký tự a, b, c trong xâu con đang xét, quá trình này mất $O(n)$ trong trường hợp xấu nhất. Như vậy ta có một thuật toán $O(n^3)$. Tất nhiên sẽ không đủ để qua được bài này.
Để giảm độ phức tạp trong cách làm trên thì ta có thể đếm trước số lượng ký tự a, b, c của xâu con từ 0 đến i và lưu vào mảng prefix_a, prefix_b, prefix_c. Ta để ý là $prefix_a[i] = prefix_a[i - 1] + 1$ nếu s[i] == 'a', nếu không thì $prefix_a[i] = prefix_a[i - 1]$. Như vậy thì với xâu con $(i, j)$ bất kì(chứa các ký tự từ s[i] đến s[j]) thì ta có thể tính nhanh số ký tự 'a': $prefix_a[j] - prefix_a[i - 1]$. Lúc này độ phức tạp còn $O(n ^ 2)$. Đến đây vẫn không thể qua được bài này với ràng buộc đã cho.
Ta gọi $s(i, j)$ là xâu con chưa các ký tự $s[i], s[i + 1]...s[j]$. Ta nhận xét rằng nếu $s(i, j)$ thỏa mãn đề bài thì $s(i, j + 1)$, $s(i, j + 2)$... cũng thỏa mãn đề bài, trong 2 cách trên ta hoàn toàn không sử dụng thông tin này. Khi đó ta có cách giải tối ưu như sau:
* Ban đầu ta có 2 con trỏ *start* và *end*, ta khởi tạo *start* = 0 và *end* = -1(Điều này không quá quan trọng, khi đã hiểu thuật toán thì các bạn có thể sẽ có cách khởi tạo khác). Bây giờ ta sẽ nâng con trỏ *end* cho tới khi nào  $s(start, end)$ thỏa mãn điều kiện đề bài. Tất nhiên nếu không có trường hợp nào thỏa mãn thì ta kết thúc và lúc này kết quả dĩ nhiên là 0.
* Sau khi đã tìm được vị trí để $s(start, end)$ thỏa mãn đề bài thì lúc này dễ thấy các xâu $s(start, end + 1)$, $s(start, end+2)$... cũng thỏa mãn đề bài, ta có thể tính ngay số lượng xâu thỏa mãn lúc này là $s.length - end$, do đó ta không việc gì phải tiếp tục nâng *end* lên. Thay vào đó ta bắt đầu tăng *start* lên, cứ mỗi lần nâng *start* lên nếu xâu $s(start, end)$ còn thỏa mãn thì ta cộng thêm một lượng $s.length - end$ vào kết quả. Đến khi xâu $s(start, end)$ không còn thỏa mãn thì ta bắt đầu quay lại bước đầu tiên là nâng *end* lên và tiếp tục như vậy cho đến khi *end* đến cuối xâu.

Dễ thấy với phương án trên, ta chỉ duyệt qua xâu đúng 1 lần, cho nên độ phức tạp là $O(n)$.

#### Leetcode 1359
**Độ khó**: Khó.(cú lừa đến từ leetcode vì bài này dễ hơn bài trên rất nhiều).
**Điểm**: 6
**Đề bài**:
Có $n$ đơn hàng, mỗi đơn hàng thì gồm 2 quá trình, nhận hàng và vận chuyển.
Tính tất cả các dãy nhận hàng, vận chuyển của các đơn hàng sao cho quá trình nhận hàng của đơn hàng thứ i luôn nằm trước quá trình vận chuyển của đơn thứ i.
Do kết quả có thể rất lớn nên sẽ lấy mod cho $10^9 + 7$.
**Test mẫu**:
| Input | Output |
|-------|--------|
| n = 1 | 1 |
| n = 2 | 6 |
| n = 3 | 90 |

**Ràng buộc**: $1 \leq n \leq 500$.
**Phương án giải**:
Gọi quá trình nhận hàng và vận chuyển của đơn hàng thứ $i$ là $v_i$ và $c_i$, ta sẽ sắp xếp dãy gồm $2n$ số $v_1, v_2....v_n, c_1, c_2...,c_n$ sao cho $v_i < c_i$.
Đầu tiên ta để xếp $v_1$, $c_1$ vào dãy trên thì ta có: $\binom{2n}{2}$.
Tương tự ta xếp tiếp $v_2$, $c_2$: $\binom{2n - 2}{2}$
Như vậy để xếp $v_i$, $c_i$ thì $\binom{2n - 2(i - 1)}{2}$
Ta lấy tích của tất cả các giá trị này lại là xong.
$$\prod_{i = 1}^{n}\binom{2n - 2(i-1)}{2}$$
