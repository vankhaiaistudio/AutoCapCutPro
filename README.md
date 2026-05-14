<div align="center">
  <img src="https://img.icons8.com/color/144/000000/capcut.png" alt="Logo" width="100"/>
  <h1>Auto CapCut Pro</h1>
  <p><strong>Công cụ Tự Động Hóa Xây Dựng Dự Án CapCut Bằng Trí Tuệ Nhân Tạo (AI)</strong></p>

  [![Python](https://img.shields.io/badge/Python-3.11+-blue.svg?logo=python&logoColor=white)](#)
  [![PyQt5](https://img.shields.io/badge/PyQt5-GUI-green.svg?logo=qt)](#)
  [![AI](https://img.shields.io/badge/AI-Whisper%20%7C%20TTS-orange.svg)](#)
  [![License](https://img.shields.io/badge/License-Proprietary-red.svg)](#)

</div>

<br/>

## 🌟 Giới Thiệu
**Auto CapCut Pro** là ứng dụng Desktop mạnh mẽ được phát triển bởi **Văn Khải AI Studio**, giúp các nhà sáng tạo nội dung (Content Creators) biến kịch bản văn bản thành một Video Dự Án (Draft) hoàn chỉnh trên CapCut Desktop chỉ với vài cú click chuột.

Hệ thống tích hợp hàng loạt công nghệ AI tiên tiến (Text-to-Speech, Silence Detection, Whisper Subtitling) để tự động sinh giọng đọc, tạo phụ đề, lồng ghép hiệu ứng hình ảnh (Ken Burns) và tự động lắp ráp chúng vào Timeline của CapCut.

---

## 🔥 Tính Năng Nổi Bật

### 🤖 1. AI Text-To-Speech (Khử Khoảng Lặng)
- Tích hợp Engine TTS siêu thực (Voice Cloning).
- **Silence Detection**: Tự động phát hiện và cắt bỏ những khoảng lặng thừa trong file âm thanh AI bằng thuật toán phân tích biên độ (`pydub`), giúp video giữ được nhịp độ dồn dập, lôi cuốn.

### 📝 2. Tự Động Tạo Phụ Đề (Auto Subtitles)
- Hỗ trợ **Const-me Whisper** (phiên bản Whisper tối ưu GPU siêu tốc trên Windows) và `faster-whisper`.
- Tự động tạo phụ đề khớp 100% với giọng đọc đã được khử khoảng lặng.
- Chỉnh sửa trực tiếp font chữ, màu sắc, viền (stroke), bóng chữ (shadow) và vị trí của phụ đề ngay trên App.

### 🎨 3. Auto Sync & Ken Burns Effects
- Khớp nối Ảnh/Video với nội dung đọc một cách tự động dựa trên quy tắc đặt tên (`1_anh.jpg`, `2_video.mp4`).
- Tự động thêm **Hiệu ứng Ken Burns** (Pan/Zoom) đa chiều (Trái, Phải, Trên, Dưới, Random) giúp ảnh tĩnh trở nên sinh động.
- Hỗ trợ gán **Chuyển cảnh (Transitions)** ngẫu nhiên hoặc cố định giữa các clip.

### ⚙️ 4. Build CapCut Draft Nội Bộ
- Đọc thông số trực tiếp từ CapCut Draft JSON.
- Hỗ trợ **Compound Clip**: Tự động gộp Video & Audio để giữ Timeline CapCut siêu gọn gàng.
- Định cấu hình sẵn Tỷ lệ khung hình, FPS, Color Space, Watermark.

### 🔐 5. Hệ Thống License & Thanh Toán Tự Động (PayOS)
- Tích hợp hệ thống phân phối mã bản quyền (HWID-based).
- Tích hợp cổng thanh toán **PayOS** với mã QR động, tự động nhận dạng giao dịch và cấp Key kích hoạt ngay trên Desktop App.

---

## 🛠️ Công Nghệ Sử Dụng (Tech Stack)
- **Ngôn ngữ:** Python 3.11+
- **Giao diện:** PyQt5 (Thiết kế Modern UI, QThread multiprocessing)
- **Xử lý Audio/Video:** FFmpeg, Pydub, Soundfile
- **AI Models:** HuggingFace Transformers, Const-me Whisper
- **Bảo mật & Đóng gói:** Cython (Compile `.py` to `.pyd` C-Extensions), PyInstaller, Inno Setup

---

## 📂 Cấu Trúc Dự Án

```bash
Auto_Capcut_Pro/
├── auto_capcut_pro.py       # Entry point
├── build.py                 # Pipeline đóng gói tự động (Cython -> PyInstaller -> Inno)
├── src/                     # Source code (Classes, Workers, UI Panels, Utils)
│   ├── main_window.py       # Cửa sổ chính của ứng dụng
│   ├── panels.py            # Logic UI của 3 bước (Kịch bản, Media, Xuất CapCut)
│   ├── capcut_builder.py    # Module sinh file draft_content.json cho CapCut
│   ├── workers.py           # Luồng chạy ngầm AI (TTS, Whisper, Silence)
│   ├── payment_dialog.py    # Giao diện PayOS QR Code
│   └── license_manager.py   # Quản lý HWID & Key mã hóa
├── vkai_tts/                # Core AI Engine (Đã được Obfuscated)
└── build_temp/              # Thư mục xử lý quá trình Build
```

---

## 🚀 Hướng Dẫn Cài Đặt (Dành Cho Dev)

### 1. Yêu cầu hệ thống
- Windows 10/11 (64-bit)
- Python 3.11+
- Visual C++ Build Tools (để chạy Cython compile)
- FFmpeg (Thêm vào biến môi trường `PATH`)

### 2. Cài đặt thư viện
```bash
pip install -r requirements.txt
```

### 3. Khởi chạy ở chế độ Development
```bash
python auto_capcut_pro.py
```

### 4. Build File Thực Thi (.exe) & Installer
Ứng dụng sử dụng script build đa bước tự động hóa cực mạnh:
```bash
# Lệnh build toàn diện (Cython -> PyInstaller -> InnoSetup)
python build.py

# Nếu chỉ muốn test build nhanh bỏ qua Cython & Inno Setup
python build.py --skip-cython --skip-installer
```
*File `AutoCapCutPro_Setup_vX.X.X.exe` sẽ được lưu trong thư mục `dist/`.*

---

## 💡 Workflow Sử Dụng Ứng Dụng (User Guide)

1. **Bước 1 (Kịch bản & AI):** Nhập văn bản kịch bản (chia theo từng phần). Chọn Giọng đọc mẫu. App sẽ tự động tạo âm thanh, lọc khoảng lặng, và quét phụ đề.
2. **Bước 2 (Media & Hiệu Ứng):** Cấu hình Nhạc nền, Watermark. Chọn hiệu ứng Pan/Zoom, Font chữ phụ đề, Căn lề, Drop Shadow.
3. **Bước 3 (Xuất File):** Trỏ đường dẫn lưu đến thư mục Draft của CapCut Desktop (vd: `AppData/Local/CapCut/User Data/Projects/com.lveditor.draft/`). Nhấn **Xuất Project**.
4. **Mở CapCut:** Draft sẽ xuất hiện ngay trong danh sách dự án nội bộ của CapCut, sẵn sàng cho bạn review và Export!

---

<div align="center">
  <i>Bản quyền thuộc về <b>Văn Khải AI Studio</b> © 2026. Mọi hành vi sao chép không xin phép đều bị cấm.</i>
</div>
