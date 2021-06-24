---
layout: post
title: "[ML] BÀI 0: CÁC BƯỚC CƠ BẢN ĐỂ GIẢI QUYẾT MỘT BÀI TOÁN MACHINE LEARNING "
categories: machine_learning
author:
- Nguyễn Thị Thu Hằng
---

![IMAGE](https://aiwithmisa.com/img/in-post/aml/ml-step.png)

# **1. THU THẬP DỮ LIỆU (GET DATA)**

>Bản thân mình là một đứa ngô nghê về việc phải crawl dữ liệu về như thế nào, làm sao để đọc được dữ liệu nên mình phải đứng ở giai đoạn này khá lâu và cũng nhiều lần suýt từ bỏ. Chắc hẳn rất buồn cười nhỉ? Vì đây chỉ là bước gửi xe mà thôi. 

Cũng dễ hiểu thôi mình muốn máy học thì mình phải cho nó dữ liệu để học chứ. Tất nhiên data càng lớn thì càng tốt(nguồn học càng nhiều càng biết rộng hiểu sâu).

Để thực hành các kỹ năng ML, chúng ta có thể tận dụng những nguồn dữ liệu (dataset) dồi dào từ các nguồn nổi tiếng như Kaggle (Kaggle: Your Home for Data Science), UCI (UCI Machine Learning Repository). 

[**THỰC HÀNH DOWNLOAD DATASET TẠI ĐÂY.**](https://github.com/NT-ThuHang/Machine-Learning-Tutorial/blob/main/%5BTH0%5DDownload_Dataset.ipynb) 
Trong bài thực hành trên mình thực hiện trên nền tảng của google colab.

# **2. TIỀN XỬ LÍ DỮ LIỆU (PRE-PROCESSING)**
Khi có được dữ liệu, chúng ta cần phải tiền xử lý (pre-processing) trước khi tiến hành training model. Đây là giai đoạn rất quan trọng, nó giống như việc chúng ta cần phải cắt, gọt, rửa rau, thịt, cá trước khi đưa vào nồi để nấu. Bước đầu tiên để tiền xử lý dữ liệu chúng ta cần phải khám phá và phân tích dữ liệu – Explory Data Analysis (EDA).

Trong EDA chúng ta sẽ khám phá và phân tích những thông tin về tập dữ liệu (dataset) như số lượng cá thể (instance), số biến (variable), phân phối (distribution) giá trị của các biến, mối quan hệ giữa các biến không phụ thuộc (independent variable) và biến phụ thuộc (dependent variable) cũng như kiểm tra các vấn đề như dữ liệu trống (missing values), mất cân bằng dữ liệu (imbalanced dataset), kiểm tra các cá thể ngoại biên (outlier). Để có thể nhìn nhận một cách trực quan các vấn đề, khi thực hiện EDA chúng ta sẽ sử dũng các biểu đồ như biểu đồ cột, hộp (box-plot), phân phối (distribution).

# **3. HUẤN LUYỆN DỮ LIỆU**
Khi dữ liệu đã được thu thập và tiền xử lý (pre-process) xong, giờ chúng ta sẽ bắt đầu tiến hành huấn luyện (training) cho ML model. Chúng ta sẽ phải lựa chọn ML model phù hợp với yêu cầu của bài toán. Với bài toán regression chúng ta có thể lựa chọn các model: Linear Regression, Polynomial Regression, Decision Tree (DT), Support Vector Machine (SVM), Artificial Neural Network (ANN). Với bài toán classification chúng ta có thể lựa chọn các model: Naive Bayes, Logistic Regression, DT, SVM, ANN. Để có thể lựa chọn ML model chính xác chúng ta cần suy xét về phân phối (distribution) của các cá thể (instance) trong tập dữ liệu (dataset).

![IMAGE](https://aiwithmisa.com/img/in-post/aml/distribution.jpg)
Ở hình trên mô tả một tập dữ liệu (dataset) có 2 nhóm (class) được biểu thị bằng các ký hiệu vuông và cộng. ML model sau quá trình huấn luyện sẽ cho ra một đường phân định (decision boundary) giúp phân loại các cá thể (instance) trong tập dữ liệu (dataset). Trong trường hợp đơn giản như ở hình đầu tiên, đường phân định (decision boundary) của chúng ta chỉ cần là một đường thẳng tuyến tính (linear) đã có thể phân loại được hai nhóm (class) một cách chính xác. Nhưng ở hình ở giữa, mọi thứ đã phức tạp hơn một chút, chúng ta phải sử dụng tới 2 đường thẳng tuyến tính (linear) kết hợp mới phân định được các nhóm. Ở hình cuối cùng mọi thứ trở nên rất phức tạp, đường phân định (decision boundary) là một đường phi tuyến (nonlinear) để sinh ra được đường phân định (decision boundary) này cần phải sử dụng các nonlinear ML model.

Để thuận tiện cho quá trình training, tập dữ liệu (dataset) sẽ được sẽ được chia ta thành 3 tập nhỏ hơn: tập dữ liệu huấn luyện (training set), tập dữ liệu xác nhận (validation set) và tập dữ liệu kiểm thử (testing set). Trong quá trình huấn luyện, ML model sẽ ‘học’ trên tập dữ liệu huấn luyện (training set) và sau đó kiểm tra trên tập dữ liệu xác nhận (validation set). Quá trình huấn luyện ML model cần đảm bảo sao cho ML model không bị thiếu vừa vặn (underfit) cũng như quá vừa vặn (overfit). Việc nhận biệt sẽ dựa vào chỉ số mất mát của việc huấn luyện (training loss) và chỉ số mất mát của việc xác nhận (validation loss). Chỉ số mất mát (loss) này sẽ cho biết lỗi (error) của ML model trong việc dự đoán. Nếu chỉ số mất mát ở cả quá trình huấn luyện (training loss) và xác nhận (validation loss) đều cao, đó là dấu hiệu của việc thiếu vừa vặn (underfit), lúc này chúng ta cần tiến hành huấn luyện (tranining) thêm cho ML model. Nếu chỉ số mất mát của việc huấn luyện (training loss) là thấp trong khi đó chỉ số mất mát của việc xác nhận (validation loss) lại rất cao, điều đó chứng tỏ ML model đã có dấu hiệu của việc quá vừa vặn (overfit) và cần dừng việc huấn luyện (training) cho ML model.

![IAMGE](https://aiwithmisa.com/img/in-post/aml/over-underfit.png)

![IMAGE](https://aiwithmisa.com/img/in-post/aml/training.png)
# **4. KIỂM THỬ**
Sau khi đã trải qua quá trình huấn luyện (training), model giờ có thể đưa ra dự đoán kết quả trên tập dữ liệu kiểm thử (testing set) và so sánh với giá trị thực của chúng. Để đánh giá hiệu năng (performance) của ML model một trong cách phổ biến đó là dựa vào ma trận nhầm lẫn (confusion matrix).

![IMAGE](https://aiwithmisa.com/img/in-post/aml/confusion-matrix.png)
Ma trận nhầm lẫn sẽ giúp chúng ta biết được có bao nhiêu cá thể (instance) được ML model dự đoán là khớp (match) với nhãn (label) của chúng và bao nhiêu bị dự đoán sai. Như hình trên chúng ta có 2 nhóm (class) 1 và 0, chúng ta sẽ ngầm hiểu nhóm 1 là dương tính (Positive) và nhóm 0 là âm tính (Negative). Từ đó sẽ có 4 giá trị trong ma trận nhầm lẫn (confusion matrix).

True Positives (TPs): Số cá thể (instance) được dự đoán là dương tính (Positive) và nhãn (label) của chúng cũng là dương tính (Positive)
True Negatives (TNs): Số cá thể (instance) được dự đoán là âm tính (Negative) và nhãn (label) của chúng cũng là âm tính (Negative)
False Positives (FPs): Số cá thể (instance) được dự đoán là dương tính (Positive) nhưng nhãn (label) của chúng lại là âm tính (Negative)
False Negatives (FNs): Số cá thể (instance) được dự đoán là âm tính (Negative) nhưng nhãn (label) của chúng lại là dương tính (Positive)
Từ các con số TPs, TNs, FPs, FNs chúng ta sẽ tính được các chỉ số sau:
![](https://2.bp.blogspot.com/-EvSXDotTOwc/XMfeOGZ-CVI/AAAAAAAAEiE/oePFfvhfOQM11dgRn9FkPxlegCXbgOF4QCLcBGAs/w1200-h630-p-k-no-nu/confusionMatrxiUpdated.jpg)
Độ chính xác (accuracy) sẽ cho chúng ta biết tỉ lệ cá thể (instance) được dự đoán chính xác, nếu để ý chúng ta sẽ thấy tử số của accuracy chính là tổng giá trị ở các ô nằm trên đường chéo (diagonal) của ma trận nhầm lẫn (confusion matrix). Tuy nhiên độ chính xác (accuracy) đôi khi không nói lên hết được vấn đề, đặc biệt là nếu tập dữ liệu kiểm thử (testing set) có hiện tượng mất cân bằng (imbalanced dataset). Ví dụ trong bài toán phân loại gian lận (fraud) thẻ tín dụng, tập dữ liệu kiểm thử (testing dataset) của chúng ta có 100 cá thể (instance), trong đó 99 cá thể (instance) thuộc nhóm không gian lận và chỉ có 1 cá thể (instance) thuộc nhóm gian lận. ML model của chúng ta dự đoán 100 cá thể này đều thuộc nhóm không gian lận và theo cách tính độ chính xác (accuracy) sẽ là 0.99 hay 99%, wow một con số rất hoàn hảo đúng không, nhưng bạn có thấy có gì đó sai sai ?

Vì lẽ đó mà chúng ta cần tính thêm các chỉ số như độ bao phủ (recall), độ chuẩn xác (precision). Độ bao phủ (recall) sẽ cho chúng ta biết trong tổng số các cá thể (instance) dương tính (positive) tỉ lệ được dự đoán chính xác là dương tính (positive) là bao nhiêu. Độ chuẩn xác (precision) sẽ cho chúng ta biết trong tổng số các cá thể (instance) được dự đoán là dương tính (positive) tỉ lệ các cá thể (instance) thực sự là dương tính (positive) là bao nhiêu. F1-score là chỉ số tổng hợp cân bằng giữa độ bao phủ (recall) và độ chuẩn xác (precision) . 
Dựa vào ma trận nhầm lẫn trên chúng ta có thể thấy, độ bao phủ (recall), độ chuẩn xác (precision) và F1-score của ML model sẽ đều là 0%. Như vậy độ bao phủ (recall) và độ chuẩn xác (precision) cho chúng ta thêm những cái nhìn toàn diện hơn về hiệu năng (peformance) của ML model.

Ngoài việc sử dụng ma trận nhầm lẫn (confusion matrix) và tính các chỉ số trên, một phương pháp khác để kiểm tra hiệu năng hiệu năng (peformance) của ML model cũng khá phổ biến đó là dùng chỉ số AUC. AUC là viết tắt của Area Under Curve, hay diện tích dưới vòng cung. Để tính được AUC, chúng ta cần vẽ ra được vòng cung ROC (ROC curve), ROC là viết tắt của receiver operating characteristic curve. Vòng cung ROC sẽ cho chúng ta biết sự thay đổi của tỉ lệ dương tính đúng (True Positive Rate) và tỉ lệ dương tính sai (False Positive Rate) khi ngưỡng (threshold) của ML model thay đổi. Ngưỡng (threshold) của ML model thông thường sẽ là 0.5, khi output của ML model lớn hơn ngưỡng (threshold) thì sẽ được phân loại vào nhóm dương tính (Positive class) nếu nhỏ hơn ngưỡng (threshold) thì sẽ phân loại vào nhóm âm tính (Negative class). Chúng ta sẽ hiểu rõ hơn về ngưỡng khi đi sâu vào từng ML model.
![](https://www.researchgate.net/profile/Andreas-Fallgatter/publication/230830197/figure/fig1/AS:267609178374146@1440814408186/Confusion-matrix-summarizing-the-errors-made-by-the-classifier-on-the-test-set.png)

![](https://aiwithmisa.com/img/in-post/aml/roc-curve.png)
Vòng cung ROC ở hình trên chính là đường xanh kẻ gạch, và AUC sẽ là diện tích bao bởi hình cung đó. AUC sẽ giao động từ 0 cho đến 1, càng gần 1 thì ML model có hiệu năng (performance) càng tốt.
# **5. MỘT SỐ KHÁI NIỆM CƠ BẢN KHI TÌM HIỂU MACHINE LEARNING**
Có những khái niệm cơ bản cần nắm khi tìm hiểu về Machine learning.

**Data**: dữ liệu đầu vào.

**Label**: đầu ra (hay còn gọi là nhãn).

**Model**: được tạo ra từ data và label, sử dụng model để dự đoán những data khác.

**Thư viện numpy**: một thư viện toán học phổ biến và mạnh mẽ của Python.

**Thư viện tensorflow**: thư viện mã nguồn mở hỗ trợ cho việc tính toán số học dựa trên biểu đồ mô tả sự thay đổi của dữ liệu.

**Loss**: hàm đánh giá độ chính xác của giá trị dự đoán.

**Optimizer**: hàm đưa ra giá trị dự đoán sao cho giá trị của hàm loss là nhỏ nhất.

**Epochs**: Số lần lặp khi train model.

**Neural network**: là một hệ thống tính toán lấy cảm hứng từ sự hoạt động của các neuron trong hệ thần kinh.