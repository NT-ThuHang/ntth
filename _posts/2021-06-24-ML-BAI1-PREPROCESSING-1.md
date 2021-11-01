---
layout: post
title: "[ML] BÀI 1: TIỀN XỬ LÍ DỮ LIỆU"
categories: machine_learning
author:
- Nguyễn Thị Thu Hằng
---

![image](https://serokell.io/files/df/dfsdv4ab.2_(23)_(1).jpg)

**Tiền xử lý dữ liệu** là một bước rất quan trọng trong việc giải quyết bất kỳ vấn đề nào trong lĩnh vực Học Máy. Hầu hết các bộ dữ liệu được sử dụng trong các vấn đề liên quan đến Học Máy cần được xử lý, làm sạch và biến đổi trước khi một thuật toán Học Máy có thể được huấn luyện trên những bộ dữ liệu này. Các kỹ thuật tiền xử lý dữ liệu phổ biến hiện nay bao gồm: xử lý dữ liệu bị khuyết (missing data), mã hóa các biến nhóm (encoding categorical variables), chuẩn hóa dữ liệu (standardizing data), co giãn dữ liệu (scaling data),… Những kỹ thuật này tương đối dễ hiểu nhưng sẽ có nhiều vấn đề phát sinh khi chúng ta áp dụng vào các dữ liệu thực tế. Bởi lẽ các bộ dữ liệu ứng với các bài toán trong thực tế rất khác nhau và mỗi bài toàn thì đối mặt với những thách thức khác nhau về mặt dữ liệu. Trong bài viết này, mình sẽ cùng nhau tìm hiểu về các kỹ thuật tiền xử lý dữ liệu và cách áp dụng chúng trong các bài toán thực tế.

# **1. MISSING DATA**
## **1.1 Phân loại**
Dữ liệu bị thiếu được chia ra làm ba dạng:
* ***Khuyết ngẫn nhiên (Missing at Random – MAR)***: sự khuyết dữ liệu của đặc trưng này có điều kiện hoặc phụ thuộc vào một hoặc một vài các đặc trưng khác.
* ***Khuyết hoàn toàn ngẫu nhiên (Missing Completely at Random – MCAR)***:  Không có mối quan hệ nào giữa đặc trưng bị khuyết với các giá trị giả định hoặc các ràng buộc trên các đặc trưng khác. Ở đây, tập dữ liệu bị khuyết chỉ là một tập con ngẫu nhiên của bộ dữ liệu.
* ***Khuyết không ngẫu nhiên (Missing not at Random – MNAR)***: Khuyết không ngẫu nhiên xảy ra khi một điểm dữ liệu bị khuyết phụ thuộc cả vào các giá trị giả định (ví dụ như những người giàu có thường không tiết lộ mức thu nhập của họ khi bạn khảo sát) và các giá trị của các đặc trưng khác (ví dụ như khi bạn muốn khảo sát tuổi của một người, mà người đó là con gái thì thường là bạn sẽ không nhận được câu trả lời từ họ).

Trong hai trường hợp đầu tiên, xóa đi các điểm dữ liệu bị thiếu dựa vào số lần xuất hiện của chúng là chấp nhận được. Nhưng trong trường hợp thứ ba, việc xóa đi các quan sát bị khuyết giá trị có thể khiến cho mô hình bị ảnh hưởng. Do đó, chúng ta cần rất lưu tâm trước khi xóa đi những điểm dữ liệu này.

Ngoài ra, chúng ta cũng cần hiểu rằng cách bỏ qua (không xử lý gì) những điểm dữ liệu bị khuyết này là cách không nên áp dụng, nó có thể rất tai hại nếu như bạn không xử lý đúng đắn khi phân tích dữ liệu của bạn. *Bởi lẽ dữ liệu bị khuyết sẽ khiến bạn đưa ra những kết luận sai lầm về bộ dữ liệu của bạn khi bạn nhìn vào các giá trị sai về tổng, trung bình hoặc phân phối của bộ dữ liệu.*


## **1.2 Xóa dữ liệu khuyết**

Nói thẳng ra thì các gì mập mờ cũng không tốt. Ví dụ như TRÊN TÌNH BẠN DƯỚI TÌNH YÊU. Ủa là cái gì? Rõ ràng đi chứ. Cái gì mập mờ quá mình bỏ đi để không lại sai. Nhưng trong ML data càng nhiều là càng tốt nhưng nếu xóa đi quá nhiều thì tiếc lắm, mà không xóa thì lại dễ dẫn đến sai. Vậy chúng ta phải làm sao?
### Listwise

Phương pháp xóa dữ liệu listwise xóa đi tất cả các điểm dữ liệu có một hoặc một vài giá trị đặc trưng bị khuyết. Phương pháp này thường chỉ được sử dụng khi bạn đang tiến hành một nghiên cứu để so sánh với một phương pháp xử lý khác. Vì trong thực tế thì phương pháp này đem lại nhiều bất lợi. Bởi lẽ dữ liệu khuyết hoàn toàn ngẫu nhiên MCAR thường hiếm gặp, do đó, phương pháp này nhiều khả năng tạo ra các tham số và ước lượng bị lệch cho mô hình.


### Pairwise

Phương pháp xóa pairwise cố gắng tối thiểu hóa sự mất mát khi sử dụng phương pháp xóa listwise. Để hiểu đơn giản về phương pháp xóa pairwise, ta hãy liên tưởng đến **ma trận tương quan**. Mỗi giá trị tương quan thể hiện mức độ liên kết giữa hai biến (đặc trưng). Với mỗi cặp biến mà dữ liệu không bị khuyết, hệ số tương quan sẽ được đưa vào tính toán. Do đó, phương pháp xóa pairwise tối đa hóa các dữ liệu có sẵn bởi một phân tích cơ sở. Một thế mạnh của phương pháp này là nó làm tăng sức mạnh và tính hiệu quả của các phân tích mà bạn muốn thực hiện. Mặc dù phương pháp này được khuyến nghị dùng nhiều hơn là phương pháp xóa listwise, nhưng nó cũng sử dụng giả thiết rằng dữ liệu bị khuyết thuộc dạng khuyết hoàn toàn ngẫu nhiên MCAR.

### Xóa nguyên cột luôn nếu cột không quan trọng
[**CÁC CÚ PHÁP CỦA CÁC LỆNH XÓA CỤ THỂ Ở LINK NÀY!**](https://datasciencevn.com/thao-tac-voi-du-lieu/xu-ly-o-du-lieu-trong.html)

## **1.3 Điền khuyến dữ liệu**
Với một đặc trưng dữ liệu dạng số, có rất nhiều lựa chọn mà chúng ta có thể xem xét khi điền vào một giá trị bị khuyết, ví dụ:

* Một giá trị hằng có ý nghĩa trong miền xác định của dữ liệu, ví dụ như 0.
* Một giá trị của một đặc trưng từ một mẫu dữ liệu ngẫu nhiên trong tập dữ liệu.
* Các giá trị thống kê cơ bản như giá trị trung bình, giá trị trung vị hay giá trị mốt (mode) của cột.
* Một giá trị được ước lượng từ một mô hình dự đoán khác.

#### Cụ thể
#### Thay thế những dữ liệu missing với các giá trị: -1, -99, -999
Với những features có tính liên tục thì việc chúng ta thay thế những giá trị missing bằng các giá trị **-1, -99, -999, ...** sẽ giúp cho những mô hình cây như (RF - Random Forest) hoạt động tốt hơn bởi khi thay thế bằng những giá trị ở trên thì các mô hình này có thể giải thích cho việc thiếu dữ liệu thông qua việc encoding này. **Nhược điểm của nó làm giải hiệu suất của mô hình tuyến tính sẽ bị ảnh hưởng.**

```python
dataset.Fare.fillna(-99,inplace=True)
```
#### Thay thế bằng giá trị mean, midian, mode

Với phương pháp này chúng ta điền những giá trị bị thiếu bằng giá trị **mean** hay **median** của một vài biến nếu biến liên tục và điền mode nếu biến là biến categorical. **Tuy phương pháp này nhanh nhưng lại làm giảm phương sai của dữ liệu.** Bên cạnh đó khi thực hiện cách này thì nó *phù hợp với mô hình tuyến tính đơn giản và NN. Nhưng đối với những bài toán dựa trên tree thì có vẻ không phù hợp lắm.*
Ví dụ code:
```python
dataset.Age.fillna(dataset.Age.mean(),inplace=True)
```
Hoặc
```python
dataset.Age.fillna(dataset.Age.median(),inplace=True)
```
Hoặc với biến categorical chúng ta sử dụng mode:
```python
dataset.Cabin.fillna(dataset.Cabin.mode()[0],inplace=True)
```
#### Sử dụng mô hình dự đoán cho data impution

Ở đây chúng ta có thể sử dụng K-NN, Linear-Regression để dự đoán các giá trị còn thiếu:
