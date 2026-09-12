# Deep Learning / Graph Neural Networks Preprocessed Dataset (NF-BoT-IoT-v2)

Dữ liệu đồ thị mạng đã qua tiền xử lý, tối ưu cho các mô hình Graph Neural Networks (GNN: E-GraphSAGE, Anomal-E, GCN, GAT...) và Deep Learning.

## 1. Thông số tổng quan
- **Tổng số mẫu:** 500,000 flows (lấy mẫu phân tầng chuẩn xác cả 5 lớp tấn công).
- **Phân chia:**
  - `train.parquet`: 350,000 dòng (70%) - 5.1 MB
  - `val.parquet`: 50,000 dòng (10%) - 794 KB
  - `test.parquet`: 100,000 dòng (20%) - 1.5 MB
- **Tổng số đỉnh duy nhất (Unique Nodes):** 234,664 đỉnh (cặp IP:Port).
- **Định dạng:** Apache Parquet (nén Snappy).

## 2. Cấu trúc Đồ thị (Graph Topology)
- **Đỉnh nguồn (Source Node):** `src_node` = `IPV4_SRC_ADDR:L4_SRC_PORT`
- **Đỉnh đích (Destination Node):** `dst_node` = `IPV4_DST_ADDR:L4_DST_PORT`
- **Đặc trưng cạnh (Edge Features):** 39 đặc trưng NetFlow số thực.
- **Nhãn cạnh (Edge Labels):** 
  - `Label`: 0 (Benign), 1 (Attack)
  - `Attack`: DDoS, DoS, Reconnaissance, Benign, Theft (bảo toàn tỷ lệ phân tầng).

## 3. Phân bố nhãn trong tập mẫu:
- **DDoS:** ~48.5%
- **DoS:** ~44.1%
- **Reconnaissance:** ~6.9%
- **Benign:** ~0.4%
- **Theft:** ~0.1%
