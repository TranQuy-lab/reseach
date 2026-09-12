# Machine Learning Preprocessed Dataset (NF-UQ-NIDS-v2)

Dữ liệu mạng đã qua tiền xử lý, tối ưu riêng biệt cho các mô hình Machine Learning dạng bảng (Tabular Models: Random Forest, XGBoost, LightGBM, CatBoost, Multi-Layer Perceptron...).

## 1. Thông số tổng quan
- **Tổng số mẫu:** 2,000,000 flows (lấy mẫu ngẫu nhiên có phân tầng - Stratified Sampling).
- **Phân chia:**
  - `train.parquet`: 1,400,000 dòng (70%) - 46 MB
  - `val.parquet`: 200,000 dòng (10%) - 6.6 MB
  - `test.parquet`: 400,000 dòng (20%) - 14 MB
- **Định dạng:** Apache Parquet (nén ZSTD / Snappy).

## 2. Đặc điểm kỹ thuật
- **Loại bỏ IP và Port:** 4 cột `IPV4_SRC_ADDR`, `IPV4_DST_ADDR`, `L4_SRC_PORT`, `L4_DST_PORT` đã được loại bỏ để ngăn ngừa hiện tượng rò rỉ dữ liệu (data leakage) và mô hình học vẹt địa chỉ IP tĩnh (overfitting).
- **Làm sạch:** Đã lọc toàn bộ các giá trị vô cực `+Inf`, `-Inf` và giá trị khuyết thiếu `NaN` về `0`.
- **Số lượng đặc trưng:** 39 đặc trưng số đo lưu lượng NetFlow chuẩn + nhãn `Label` (nhị phân 0/1) và `Attack` (tên dạng tấn công).
