# KHDV

## Dự án Dự đoán Giá Airbnb - New York (KHDV)

## Tổng quan

Dự án này phân tích dữ liệu từ các căn hộ cho thuê trên Airbnb tại thành phố New York để dự đoán giá thuê bằng các mô hình học máy và cung cấp các giải thích về AI.

## Cấu trúc dữ liệu

Bộ dữ liệu gồm thông tin từ [airbnb-usa-ny-newyork](https://huggingface.co/datasets/michaelmallari/airbnb-usa-ny-newyork) với các tệp:

- listings-detailed.csv - Dữ liệu chi tiết về các căn hộ
- listings-summary.csv - Dữ liệu tóm tắt về các căn hộ
- neighbourhoods.csv - Dữ liệu về khu vực
- neighbourhoods.geojson - Dữ liệu địa lý về khu vực

## Quy trình xử lý

### 1. Tiền xử lý dữ liệu ([data_preprocessing/data_preprocessing.ipynb](data_preprocessing/data_preprocessing.ipynb))

- Xử lý giá trị null
- Chuyển đổi kiểu dữ liệu
- Tạo features mới:
  - Khoảng cách đến trung tâm thành phố
  - Số lượng tiện nghi
  - Tỷ lệ giường/phòng ngủ
- One-hot encoding cho các biến category
- Tính toán điểm MOS cho chất lượng hình ảnh

### 2. Dự đoán và giải thích ([prediction_and_explainable.ipynb](prediction_and_explainable.ipynb))

- Phân tích và loại bỏ outliers
- Chuẩn hóa dữ liệu
- Huấn luyện các mô hình:
  - Linear Regression
  - Decision Tree
  - Random Forest
  - XGBoost
  - Neural Network
- Đánh giá mô hình bằng K-fold Cross Validation
- Giải thích mô hình với SHAP values

## Yêu cầu

- Python 3.x
- Các thư viện chính (và phiên bản):
  - pandas (1.3.3)
  - numpy (1.21.2)
  - scikit-learn (0.24.2)
  - xgboost (1.4.2)
  - tensorflow (2.6.0)
  - geopy (2.2.0)
  - shap (0.39.0)

## Cài đặt thư viện:

Chạy các notebook theo thứ tự:

1. data_preprocessing.ipynb
2. prediction_and_explainable.ipynb

## Đóng góp

Mọi đóng góp và phản hồi đều được chào đón. Vui lòng tạo issue hoặc pull request.

## Giấy phép

Dự án này sử dụng dữ liệu công khai từ Airbnb và tuân theo các điều khoản sử dụng của họ.

## Hướng dẫn cài đặt

1. **Clone repository**:

   ```bash
   git clone https://github.com/yourusername/airbnb-price-prediction.git
   cd airbnb-price-prediction
   ```

2. **Tạo môi trường ảo**:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Cài đặt các thư viện cần thiết**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Chạy các notebook**:
   - Mở Jupyter Notebook:
     ```bash
     jupyter notebook
     ```
   - Chạy các notebook theo thứ tự:
     - `data_preprocessing.ipynb`
     - `prediction_and_explainable.ipynb`

## Kết quả

- **Dự đoán giá**: Các mô hình học máy sẽ dự đoán giá thuê căn hộ dựa trên các đặc trưng đã xử lý.
- **Giải thích mô hình**: Sử dụng SHAP values để giải thích các yếu tố ảnh hưởng đến dự đoán của mô hình.

### Hiệu suất mô hình

| Mô hình           | MAE   | MAD   | MSE     | R² ngoài mẫu | Thời gian dự đoán (ms) |
| ----------------- | ----- | ----- | ------- | ------------ | ---------------------- |
| Dummy (mean)      | 64.39 | 57.53 | 6371.26 | -0.0         | 0.07                   |
| Dummy (median)    | 62.32 | 49.8  | 6832.07 | -0.07        | 0.06                   |
| Linear Regression | 43.03 | 32.38 | 3383.74 | 0.47         | 7.54                   |
| Decision Tree     | 53.56 | 35.0  | 5852.75 | 0.08         | 2.31                   |
| Neural Network    | 42.02 | 30.6  | 3316.95 | 0.48         | 3.39                   |
| Random Forest     | 39.95 | 28.96 | 3016.55 | 0.53         | 31.88                  |
| XGBoost           | 41.03 | 29.02 | 3218.01 | 0.49         | 9.62                   |
