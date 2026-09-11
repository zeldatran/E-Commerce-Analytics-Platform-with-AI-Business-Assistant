# E-Commerce Analytics Platform with AI Business Assistant

Nền tảng phân tích dữ liệu thương mại điện tử tích hợp Machine Learning và trợ lý AI hỗ trợ khai thác dữ liệu bằng ngôn ngữ tự nhiên.

## Giới thiệu

Trong thương mại điện tử, dữ liệu thường đến từ nhiều nguồn khác nhau như khách hàng, đơn hàng, sản phẩm, thanh toán, đánh giá và người bán. Nếu chỉ lưu trữ dữ liệu thô thì sẽ khó khai thác trực tiếp cho việc phân tích và ra quyết định.

Project này được xây dựng với mục tiêu xử lý và tổ chức dữ liệu thương mại điện tử thành một hệ thống phân tích hoàn chỉnh. Dữ liệu sau khi được làm sạch sẽ được lưu trữ trong PostgreSQL, sử dụng cho phân tích dữ liệu, xây dựng các mô hình Machine Learning và trực quan hóa bằng Power BI.

Ngoài dashboard, project xây dựng thêm một AI Business Assistant. Trợ lý cho phép người dùng đặt câu hỏi bằng ngôn ngữ tự nhiên về tình hình kinh doanh, khách hàng, sản phẩm và kết quả của các mô hình Machine Learning.

## Mục tiêu

Các chức năng chính dự kiến của hệ thống:

- Làm sạch và chuẩn hóa dữ liệu thương mại điện tử.
- Lưu trữ và tổ chức dữ liệu bằng PostgreSQL.
- Phân tích dữ liệu và các chỉ số kinh doanh.
- Phân nhóm khách hàng bằng RFM và K-Means.
- Phân tích các sản phẩm thường được mua cùng nhau bằng Apriori.
- Xây dựng mô hình dự đoán nguy cơ khách hàng rời bỏ.
- So sánh các mô hình Logistic Regression, Random Forest và XGBoost.
- Trực quan hóa dữ liệu bằng Power BI.
- Xây dựng API bằng FastAPI.
- Tích hợp LLM để xây dựng AI Business Assistant.

## Dataset

Project sử dụng bộ dữ liệu:

**Brazilian E-Commerce Public Dataset by Olist**

Dataset:
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Bộ dữ liệu chứa khoảng 100.000 đơn hàng thương mại điện tử tại Brazil và bao gồm nhiều thông tin liên quan đến khách hàng, đơn hàng, sản phẩm, người bán, thanh toán, đánh giá và vị trí địa lý.

Các file chính:

```text
olist_customers_dataset.csv
olist_geolocation_dataset.csv
olist_order_items_dataset.csv
olist_order_payments_dataset.csv
olist_order_reviews_dataset.csv
olist_orders_dataset.csv
olist_products_dataset.csv
olist_sellers_dataset.csv
product_category_name_translation.csv
```

Khi phân tích hành vi khách hàng, `customer_unique_id` được sử dụng để xác định một khách hàng duy nhất qua nhiều đơn hàng.

## Quy trình tổng thể

```text
Olist Dataset
      |
      v
Data Cleaning
Python / Pandas / NumPy
      |
      v
Data Transformation
      |
      v
PostgreSQL
      |
      v
EDA + Feature Engineering
      |
      +--------------------------+
      |             |            |
      v             v            v
   K-Means       Apriori       Churn
 Segmentation    Analysis    Prediction
                               |
                     Logistic Regression
                     Random Forest
                     XGBoost
      |             |            |
      +-------------+------------+
                    |
                    v
                 FastAPI
                    |
          +---------+---------+
          |                   |
          v                   v
      Power BI        AI Business Assistant
                              |
                              v
                             LLM
```

## Xử lý và phân tích dữ liệu

Dữ liệu ban đầu được xử lý bằng Python, Pandas và NumPy.

Một số bước chính:

- Kiểm tra dữ liệu thiếu.
- Kiểm tra dữ liệu trùng lặp.
- Chuyển đổi kiểu dữ liệu.
- Xử lý các giá trị không hợp lệ.
- Kết hợp dữ liệu từ nhiều bảng.
- Tổng hợp dữ liệu.
- Exploratory Data Analysis.
- Feature Engineering.

Dữ liệu sau khi xử lý sẽ được lưu trong PostgreSQL để phục vụ SQL Analytics, Machine Learning, Power BI và AI Business Assistant.

## Customer Segmentation

Phần Customer Segmentation sử dụng phương pháp RFM kết hợp với thuật toán K-Means.

Ba đặc trưng RFM chính:

- **Recency:** khoảng thời gian kể từ lần mua gần nhất.
- **Frequency:** tần suất mua hàng.
- **Monetary:** tổng giá trị mua hàng.

Quy trình dự kiến:

```text
Customer Data
      |
      v
RFM
      |
      v
Data Preprocessing
      |
      v
Feature Scaling
      |
      v
Elbow Method
Silhouette Score
      |
      v
K-Means
      |
      v
Customer Segments
```

Kết quả phân cụm được sử dụng để tìm hiểu đặc điểm của từng nhóm khách hàng, ví dụ nhóm khách hàng có giá trị cao, nhóm mua hàng ít hoặc nhóm đã lâu chưa quay lại mua hàng.

## Market Basket Analysis

Apriori được sử dụng để tìm các sản phẩm hoặc danh mục sản phẩm thường xuất hiện cùng nhau trong một đơn hàng.

Các association rules được đánh giá bằng:

- Support
- Confidence
- Lift

Kết quả có thể hỗ trợ phân tích hành vi mua hàng, cross-selling và đề xuất các sản phẩm phù hợp để bán cùng nhau.

## Customer Churn Prediction

Project xây dựng thêm bài toán dự đoán nguy cơ khách hàng rời bỏ.

Một số đặc trưng dự kiến:

```text
Recency
Frequency
Monetary
Average Order Value
Average Review Score
Average Delivery Time
Order Count
```

Các mô hình được thử nghiệm:

```text
Logistic Regression
Random Forest
XGBoost
```

Sau khi huấn luyện, các mô hình sẽ được so sánh bằng:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- ROC-AUC hoặc PR-AUC khi phù hợp

Nhãn churn sẽ được xác định dựa trên thời gian không phát sinh giao dịch và khoảng thời gian của bộ dữ liệu Olist.

## Power BI Dashboard

Power BI được sử dụng để xây dựng dashboard trực quan hóa dữ liệu.

Một số nội dung dự kiến:

- Tổng doanh thu.
- Số lượng đơn hàng.
- Số lượng khách hàng.
- Doanh thu theo thời gian.
- Phân tích sản phẩm và danh mục.
- Customer Segmentation.
- Market Basket Analysis.
- Customer Churn Risk.

Power BI giúp người dùng theo dõi tổng quan tình hình kinh doanh, trong khi AI Business Assistant được sử dụng khi cần hỏi sâu hơn về dữ liệu.

## FastAPI

FastAPI đóng vai trò backend để cung cấp dữ liệu phân tích và kết quả Machine Learning.

Một số endpoint dự kiến:

```text
/analytics/revenue
/analytics/customers
/segments
/market-basket
/churn/predict
/chat
```

FastAPI cũng là lớp trung gian giữa AI Business Assistant với PostgreSQL và các mô hình Machine Learning.

## AI Business Assistant

AI Business Assistant là phần trợ lý AI chuyên về phân tích dữ liệu thương mại điện tử.

Mục tiêu của trợ lý là giúp người dùng khai thác dữ liệu mà không cần trực tiếp viết SQL hoặc chạy Python.

Một số câu hỏi dự kiến:

```text
Doanh thu tháng nào cao nhất?

Top 5 danh mục sản phẩm có doanh thu cao nhất là gì?

Nhóm khách hàng nào có giá trị cao nhất?

Cluster 2 có đặc điểm gì?

Những danh mục nào thường được mua cùng nhau?

Nhóm khách hàng nào có nguy cơ rời bỏ cao?

Mô hình churn hiện tại có F1-score bao nhiêu?

Có điểm gì đáng chú ý trong hành vi khách hàng?
```

LLM không trực tiếp tạo ra các số liệu kinh doanh.

Luồng xử lý dự kiến:

```text
Người dùng đặt câu hỏi
        |
        v
       LLM
        |
        v
Phân tích ý định
        |
        v
Chọn Tool / API
        |
        v
PostgreSQL / ML Model
        |
        v
Kết quả thực tế
        |
        v
       LLM
        |
        v
Giải thích kết quả
        |
        v
Người dùng
```

Một số tool có thể được xây dựng:

```python
get_revenue_analysis()
get_customer_segments()
get_market_basket_rules()
get_customer_churn_risk()
```

Ví dụ, khi người dùng hỏi:

> Nhóm khách hàng nào có nguy cơ rời bỏ cao?

LLM sẽ xác định đây là câu hỏi liên quan đến churn, gọi chức năng phân tích churn, nhận kết quả từ backend rồi mới tạo câu trả lời.

Cách làm này giúp chatbot trả lời dựa trên dữ liệu của hệ thống thay vì tự suy đoán số liệu.

## Công nghệ sử dụng

| Công nghệ | Mục đích |
| --- | --- |
| Python | Ngôn ngữ lập trình chính |
| Pandas | Làm sạch và biến đổi dữ liệu |
| NumPy | Xử lý dữ liệu số |
| PostgreSQL | Lưu trữ dữ liệu |
| SQL | Truy vấn và phân tích |
| scikit-learn | Machine Learning và preprocessing |
| K-Means | Customer Segmentation |
| mlxtend | Apriori và Association Rules |
| XGBoost | Churn Prediction |
| Power BI | Dashboard |
| FastAPI | Backend và Model API |
| LLM | AI Business Assistant |
| Docker | Đóng gói hệ thống, dự kiến |
| MLflow | Theo dõi thí nghiệm và model, dự kiến |

## Cấu trúc project dự kiến

```text
ecommerce-analytics-platform/
|
|-- data/
|   |-- raw/
|   `-- processed/
|
|-- notebooks/
|   |-- eda/
|   |-- customer_segmentation/
|   |-- market_basket/
|   `-- churn_prediction/
|
|-- src/
|   |-- data_processing/
|   |-- features/
|   |-- models/
|   `-- analytics/
|
|-- sql/
|   |-- schema/
|   `-- analytics/
|
|-- api/
|
|-- chatbot/
|
|-- powerbi/
|
|-- docs/
|
|-- requirements.txt
|-- .gitignore
`-- README.md
```

Cấu trúc thư mục có thể thay đổi trong quá trình phát triển project.

## Tiến độ

Project hiện đang trong quá trình phát triển.

```text
[x] Chọn đề tài
[x] Chọn dataset
[x] Thiết kế ý tưởng hệ thống
[x] Hoàn thành báo cáo ý tưởng

[ ] Khảo sát dữ liệu
[ ] Data Cleaning
[ ] PostgreSQL Database
[ ] EDA
[ ] Feature Engineering
[ ] Customer Segmentation
[ ] Market Basket Analysis
[ ] Churn Prediction
[ ] Model Evaluation
[ ] Power BI Dashboard
[ ] FastAPI
[ ] AI Business Assistant
[ ] Docker / Deployment
```

Các module sẽ được cập nhật dần trong quá trình thực hiện.

## Hướng phát triển

Sau khi hoàn thành các chức năng chính, project có thể mở rộng thêm:

- Recommendation System.
- Revenue Forecasting.
- SHAP để giải thích kết quả mô hình.
- RAG để AI Assistant đọc thêm báo cáo hoặc tài liệu doanh nghiệp.
- MLflow để quản lý các lần huấn luyện model.
- Tự động hóa data pipeline.
- Docker hóa backend.
- Triển khai trên cloud.
- Model monitoring.

## Tài liệu tham khảo

Olist - Brazilian E-Commerce Public Dataset  
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Olist Customer Segmentation - RFM + K-Means  
https://github.com/helloitswinnie/Olist-Customer-Segmentation

Olist Data Warehouse  
https://github.com/cardonajsebas/olist-data-warehouse

Brazilian E-Commerce Warehouse  
https://github.com/mmorsi4/brazilian-ecommerce-warehouse

E-Commerce Data Modeling  
https://github.com/tunguyenn99/ecommerce-data-modeling

FastAPI Documentation  
https://fastapi.tiangolo.com/

scikit-learn Documentation  
https://scikit-learn.org/stable/

XGBoost Documentation  
https://xgboost.readthedocs.io/

MLflow Documentation  
https://mlflow.org/docs/latest/

## Tác giả

Trần Nguyễn Diễm Hạnh

GitHub: https://github.com/zeldatran
