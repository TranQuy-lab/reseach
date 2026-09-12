# Deep Learning / Graph Neural Networks Full Dataset (NF-ToN-IoT-v2)

Toàn bộ tập dữ liệu đồ thị mạng đã qua tiền xử lý chuẩn hóa cho các mô hình Graph Neural Networks (GNN: E-GraphSAGE, Anomal-E, GCN, GAT...) và Deep Learning.

## 1. Thông số tổng quan
- **Tổng số dòng:** 13,552,395 flows
- **Phân chia:**
  - Tập Train: 11,858,347 dòng (~316 MB)
    - Do giới hạn file của GitHub (< 100 MB/file), tập Train được lưu dưới dạng Multi-part Parquet (4 parts, ~76-86 MB/part):
      - `train/part_01.parquet` (3,000,000 dòng)
      - `train/part_02.parquet` (3,000,000 dòng)
      - `train/part_03.parquet` (3,000,000 dòng)
      - `train/part_04.parquet` (2,858,347 dòng)
  - Tập Validation: 1,694,048 dòng (`val/val.parquet`, ~45 MB)
- **Định dạng:** Apache Parquet (nén Snappy).

## 2. Cách đọc dữ liệu cực kỳ đơn giản (1 dòng code)
Pandas, PyArrow và DuckDB tự động nhận diện cả thư mục Multi-part:

```python
import pandas as pd

# Đọc toàn bộ 11.85 triệu dòng Train:
df_train = pd.read_parquet("data/dl_processed/train")
print(f"Loaded train shape: {df_train.shape}")

# Đọc tập Validation:
df_val = pd.read_parquet("data/dl_processed/val")
print(f"Loaded val shape: {df_val.shape}")
```

Hoặc với DuckDB:
```python
import duckdb
con = duckdb.connect()
df = con.execute("SELECT * FROM data/dl_processed/train/*.parquet").df()
```

## 3. Cấu trúc Đồ thị (Graph Topology)
- **Đỉnh nguồn (Source Node):** `src_node` = `IPV4_SRC_ADDR:L4_SRC_PORT`
- **Đỉnh đích (Destination Node):** `dst_node` = `IPV4_DST_ADDR:L4_DST_PORT`
- **Đặc trưng cạnh (Edge Features):** 39 đặc trưng NetFlow số thực.
- **Nhãn cạnh (Edge Labels):** 
  - `Label`: 0 (Benign), 1 (Attack)
  - `Attack`: Tên loại tấn công gốc.
