---
layout: post
title: "[ML] BÀI 4: LOGISTIC PREGRESSION "
categories: machine_learning
author:
- Nguyễn Thị Thu Hằng
---

Hôm nay chúng ta sẽ tìm hiểu về Logistic Regression model, đây là một linear model giúp giải quyết các bài toán classification ví dụ như phân loại ốm hay khỏe mạnh, gian lận hay không gian lận,..

# **1. Đường phân định - Decision boundary**

Trong bài toán phân loại, chúng ta cần Logistic Regression tạo ra một đường phân định (decision boundary) giúp phân loại các nhóm (class) của dữ liệu như hình mô tả dưới đây:

![](https://aiwithmisa.com/img/in-post/aml/logistic-regression.png)

Hàm số tuyến tính (linear function) chúng ta mong muốn sẽ là: 
<center> Score = w0 + w1x</center>

Sự khác biệt của hàm số tuyến tính (linear function) trên với hàm số của Linear Regression nằm ở bên vế trái, giá trị của biến không phụ thuộc (dependent variable) y giờ được thay bằng score, vậy score này là gì ? Score này được kỳ vọng sẽ giúp chúng phân loại cá thể (instance) vào các nhóm (class). Ở đây chúng ta sẽ để ý đến 2 thứ:
1. **Dấu của score** => giúp phân biệt nhóm (class). Giả sử chúng ta có 2 nhóm (class) là -1 và 1. Nếu dấu của score là âm thì nó sẽ thuộc về nhóm (class) -1 và dấu là dương thì nó sẽ thuộc về nhóm (class) 1.
2. **Độ lớn của score** => xác định vị trí của cá thể so với đường  phân định (decision boundary) các thể càng ở xa càng chắc chắn điểm đó thuộc về nhóm (class) đó. Các cá thế (instance) ở càng gần đường phân định, tương ứng với score bằng 0 sẽ có thể thuộc về 1 trong 2 nhóm (class), và những điểm này là những điểm khá mơ hồ (confuse), ở hình trên chúng ta thấy có một vài cá thể (instance) thuộc nhóm (class) xanh nhưng thuộc khu vực của nhóm (class) đỏ và ngược lại.

![](https://aiwithmisa.com/img/in-post/aml/score-logistic.png)


# **2. Hàm Logistic - Logistic function**

Tuy nhiên score không thể làm chúng ta hài lòng, điều chúng ta muốn là xác xuất (probability) của cá thể (instance) này thuộc về nhóm (class) là bao nhiêu phần trăm. Do đó, score sẽ được đưa vào logistic function, hay tên gọi khác đó là softmax của score. Softmax trong trường hợp chỉ có 2 nhóm (class) - binary classification còn được gọi là Sigmoid. Vậy hàm số Sigmoid (Sigmoid function) có tác dụng gì ?

![](https://aiwithmisa.com/img/in-post/aml/sigmoid.png)

Sigmoid sẽ chuyển đổi score chúng ta có được ở trên, thành xác suất (probability) của cá thể đó thuộc nhóm (class) 1
.**P(y = 1| x_{i}, w)**. Trong đó , **x_{i}, w** chính là biểu thị của hàm số tuyến tính w0 + w1x , ký hiệu trên được hiểu là xác xuất của cá thể (instance) thuộc nhóm (class) 1 với hàm số tuyến tính (linear function) đã cho (given). Thông thường chúng ta sẽ đặt 0.5 là ngưỡng (Threshold) như đã đề cập ở bài số 3, nếu xác xuất (probability) lớn hơn 0.5 chúng ta sẽ quy định cá thể (instance) thuộc nhóm class (1), nếu nhỏ hơn sẽ thuộc nhóm (class) 0. Để hình dùng cụ thể hơn về cách Sigmoid chuyển đổi Score thành xác suất (probability) chúng ta hãy xem công thức của hàm số Sigmoid, cũng như đồ thị của nó.

![](https://aiwithmisa.com/img/in-post/aml/sigmoid-plot.png)


Có thể thấy đặc chưng của Sigmoid function đó là bão hòa (saturate) ở 0 và 1 khi các giá trị của score càng lớn hoặc càng nhỏ, giúp chuyển đổi score ra xác xuất (probability) mà chúng ta mong muốn.

# **3. àm mất mát - Loss function**

Đối với các bài toán phân loại (classification), hàm mất mát (loss function) thường được sử dụng đó là cross entropy loss.

![](https://i.postimg.cc/L51gS1qc/lossfunc-logictic-R.png)

Trong đó n là số cá thể (instance) của tập dữ liệu

Để hiểu cách hoạt động của cross entropy loss, chúng ta hãy cùng xét trường hợp sau. Chúng ta có cá thể (instance) thuộc nhóm (class) 1, tương ứng với  bằng 1, tuy nhiên Logistic regression model của chúng ta lại dự đoán  bằng 0, khi đó  tương ứng với  và có giá trị âm vô cùng, loss của chúng ta sẽ rất lớn, chứng tỏ model đang dự đoán sai. Điều tương tự sẽ xảy ra trong trường hợp cá thể thuộc nhóm (class) 0, nhưng lại được dự đoán với xác suất là 1.

# **4. Kết luận**

Có thể thấy hồi quy Logistic - Logistic Regression là một biến thể của hồi quy tuyến tính Linear Regression giải quyết phân loại (classification) dữ liệu. Hai ML model này các tính chất tương đương nhau. 

[**HÃY THỰC HÀNH THEO BÀI TẬP NÀY ĐỂ MÌNH CÓ THỂ HIỂU VỀ LOGISTIC REGRESSION HƠN NHÉ!**](https://colab.research.google.com/drive/1waGRJkeFmGQnK1sKzcAY5-CxltPff110?usp=sharing)
