# FACE RECOGNITION IN CLASS - NHẬN DIỆN KHUÔN MẶT SINH VIÊN TRONG LỚP
Nguyễn Bảo Hân - 31251027458 - DA0001

Dự án nhận diện khuôn mặt bằng **keras/tensorflow**, train trên tập ảnh 29 người, chạy trên **Google Colab**.

---

## Cấu trúc project

```
├── facerecog.ipynb                      # Notebook train + predict
└── my_image_classification_model.keras  # File model (tải riêng, xem bên dưới)
```

> File model (~129MB) không được lưu trong repo do giới hạn GitHub. Tải về theo hướng dẫn bên dưới.

---

## Tải model về

Model được lưu trên Google Drive: **https://drive.google.com/file/d/1F143zL26U7waSk_UFkDo2DcosbpLwl4P/view?usp=sharing**

Tải file `my_image_classification_model.keras` về rồi upload lên Google Drive của bạn (cùng thư mục với notebook hoặc `/content/`).

---

## Cách chạy

1. Mở `facerecog.ipynb` trên **Google Colab**
2. Mount Google Drive khi được yêu cầu
3. Chạy từng cell theo thứ tự

---

## Hướng dẫn chỉnh sửa

### Đổi đường dẫn thư mục ảnh train

Tìm cell này (cell 3):

```python
drive_folder_path = '/content/drive/MyDrive/60 ẢNH'
```

Thay `60 ẢNH` thành tên thư mục ảnh của bạn trên Drive.

---

### Thêm / bớt người bị loại khỏi training

Vì có một số tệp ảnh không đạt yêu cầu nên đã bị loại bớt để giảm gây nhiễu mô hình.
Tìm cell load data, dòng này:

```python
excluded_classes = ['nguyen dong hai', 'nguyen thi thanh ha']
```

Thêm tên vào list nếu muốn loại thêm, hoặc xóa bớt nếu muốn giữ lại. Tên phải **viết thường** và **khớp với tên thư mục ảnh**.

---

### Đổi ảnh để test predict

Tìm cell predict (gần cuối notebook):

```python
path = '/content/bhan.jpg'
```

Thay bằng đường dẫn tới ảnh bạn muốn test. Nhớ upload ảnh lên Colab trước (kéo thả vào Files panel bên trái).

---

## Kiến trúc model

- **Base model**: MobileNetV2 (pretrained ImageNet, frozen)
- **Custom layers**: Flatten → Dense(512) → Dropout(0.5) → Dense(29, softmax)
- **Input size**: 128×128×3
- **Optimizer**: Adam (lr=0.0001)
- **Loss**: Categorical Crossentropy
- **Callbacks**: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint

---

## Cấu trúc thư mục ảnh train

```
MyDrive/
└── 60 ẢNH/
    ├── TEN_NGUOI_1/
    │   ├── anh1.jpg
    │   └── ...
    ├── TEN_NGUOI_2/
    └── ...
```

Mỗi thư mục con là 1 người, tên thư mục = tên class.
