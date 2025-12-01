# Employee Attrition Prediction

Đây là dự án toàn diện để phân tích và dự đoán **nhân viên rời công ty (Attrition)**, gồm:

1. **Client**: Giao diện Next.js sử dụng TailwindCSS, Framer Motion, Lucide Icons, Shadcn UI.
2. **AI Module**: Backend Python FastAPI để xử lý dữ liệu, huấn luyện model và dự đoán.

---

## 1. Cấu trúc dự án

```

root/
├── client/ # Next.js client
│ ├── src/
│ │ ├── app/
│ │ │ ├── about-dataset/
│ │ │ ├── prediction/
│ │ │ ├── sup-train-model/
│ │ │ ├── unsup-train-model/
│ │ │ ├── components/
│ │ │ ├── global.css
│ │ │ └── layout.js
│ │ ├── components/ui/ # Shadcn UI components
│ │ └── lib/
│ ├── package.json
│ └── tailwind.config.js
├── ai-module/ # Python backend & ML
│ ├── data/
│ │ ├── raw/
│ │ └── processed/
│ ├── notebooks/
│ ├── config/
│ ├── common/
│ ├── services/
│ ├── routes/
│ ├── models/
│ ├── main.py
│ └── requirements.txt
├── .gitignore
├── README.md
└── ... # các file cấu hình khác

```

---

## 2. Client - Next.js

Dự án Next.js hiển thị giao diện người dùng cho:

- **Tổng quan dữ liệu**: thống kê dataset IBM HR Analytics, phân phối lớp Attrition, boxplot các biến số.
- **Huấn luyện mô hình**: hiển thị kết quả training các model ML (Logistic Regression, KNN, Decision Tree…), so sánh các metric (Precision, Recall, F1, ROC-AUC) và mô hình tốt nhất.
- **Dự đoán nhân viên**: nhập dữ liệu nhân viên, chọn model và dự đoán khả năng rời công ty với hiển thị xác suất trực quan.

**Chạy client:**

```bash
cd client
npm install
npm run dev
# hoặc yarn dev / pnpm dev / bun dev
```

Mở [http://localhost:3000](http://localhost:3000) để xem giao diện.

---

## 3. AI Module - FastAPI + ML

Module Python xử lý:

- **Supervised Learning**: Logistic Regression, Decision Tree, Random Forest → dự đoán Attrition.
- **Unsupervised Learning**: K-means, Hierarchical Clustering → phân nhóm nhân viên.
- **Visualization**: phân tích Age, MonthlyIncome, YearsAtCompany theo Attrition hoặc JobRole.

**Cài đặt & chạy:**

```bash
cd ai-module
python -m venv venv
# Windows
.\venv\Scripts\activate
# Linux/macOS
# source venv/bin/activate
pip install -r requirements.txt

uvicorn main:app --reload
```

**API Endpoints:**

| Endpoint       | Mục đích                                |
| -------------- | --------------------------------------- |
| `/train-model` | Huấn luyện model và trả về kết quả JSON |
| `/predict`     | Dự đoán nhân viên rời công ty           |
| `/overview`    | Thống kê dữ liệu                        |

Swagger UI: `http://127.0.0.1:8000/docs`

---

## 4. Dataset

Dataset IBM HR Analytics (fictional nhưng sát thực tế). Một số feature quan trọng:

| Feature            | Kiểu        | Mô tả                          |
| ------------------ | ----------- | ------------------------------ |
| Age                | Numeric     | Tuổi nhân viên                 |
| Attrition          | Categorical | Nhân viên rời công ty (Yes/No) |
| BusinessTravel     | Categorical | Tần suất đi công tác           |
| Department         | Categorical | Bộ phận làm việc               |
| DistanceFromHome   | Numeric     | Khoảng cách nhà → công ty (km) |
| Education          | Ordinal     | 1=Below College → 5=Doctor     |
| JobRole            | Categorical | Vị trí công việc               |
| JobSatisfaction    | Ordinal     | 1=Low → 4=Very High            |
| MonthlyIncome      | Numeric     | Lương tháng                    |
| OverTime           | Categorical | Có làm thêm giờ hay không      |
| YearsAtCompany     | Numeric     | Số năm tại công ty             |
| YearsInCurrentRole | Numeric     | Số năm ở vị trí hiện tại       |

Các biến Ordinal có thể dùng trực tiếp cho ML hoặc chuyển thành dummy variables nếu cần.

---

## 5. Yêu cầu hệ thống

- Node.js >= 18 (Client)
- Python >= 3.10 (AI Module)
- Các thư viện:

  - Client: `tailwindcss`, `framer-motion`, `lucide-react`, `shadcn/ui`
  - Backend: `fastapi`, `uvicorn`, `numpy`, `pandas`, `scikit-learn`, `joblib`, `pydantic`

---

## 6. Triển khai

**Client**: Vercel
**AI Module**: bất kỳ server Python/Cloud hosting có hỗ trợ FastAPI

---

## 7. Lưu ý

- Dataset giả lập, dùng cho học tập và demo ML
- Trước khi train model: xử lý categorical variables, missing values, scale numeric features nếu cần
- Có thể mở rộng module với feature hoặc thuật toán mới
