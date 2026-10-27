# Ứng dụng thống kê CSV (ipywidgets + Voilà + Render)

Web app cho phép upload file CSV, xem bảng dữ liệu, tính thống kê mô tả và vẽ
biểu đồ (histogram, boxplot, scatter, đường, cột). Dữ liệu chỉ tồn tại trong
RAM của phiên hiện tại, không lưu vào database hay ổ đĩa.

## Cấu trúc

```
csv-statistics-voila/
|-- app.ipynb            # sinh ra bởi build_notebook.py
|-- dashboard.py         # toàn bộ giao diện và logic
|-- build_notebook.py    # tạo app.ipynb
|-- requirements.txt
|-- runtime.txt
|-- render.yaml
|-- sample_data.csv
|-- README.md
`-- .gitignore
```

## Chạy cục bộ

```bash
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell
.venv\Scripts\activate

python -m pip install --upgrade pip
pip install -r requirements.txt
python build_notebook.py
voila app.ipynb
```

Mô phỏng môi trường Render:

```bash
voila app.ipynb --no-browser --Voila.ip=0.0.0.0 --port=10000
```

Mở http://localhost:10000 rồi upload `sample_data.csv`.

## Triển khai trên Render

1. Push mã nguồn lên GitHub.
2. Render > New > Blueprint > chọn repository > Apply.
3. Hoặc tạo Web Service thủ công:
   - Build Command:
     `python -m pip install --upgrade pip && pip install -r requirements.txt && python build_notebook.py`
   - Start Command:
     `voila app.ipynb --no-browser --Voila.ip=0.0.0.0 --port=$PORT`

## Giới hạn

- File tối đa 15 MB, 300.000 dòng, 200 cột.
- Không có đăng nhập, rate limit hay lưu trữ bền vững.
- Không dùng cho dữ liệu cá nhân, tài chính, sức khỏe hoặc dữ liệu mật.
