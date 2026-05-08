# 🧠 GM_H_NHAN OS

## 🚀 Live Demo 
👉 Dùng thử MYOS v1.0 ngay: https://devnhancook.github.io/MYOS_v1.0/

### 📋 Tổng quan dự án

**GM_H_NHAN OS** là một hệ thống quản lý tri thức và năng suất cá nhân được xây dựng dưới dạng **single-file HTML application**. Đây là công cụ all-in-one giúp tổ chức kiến thức, quản lý công việc theo ma trận Eisenhower, và time-boxing hiệu quả.

### Đặc điểm chính

- **Single HTML File**: Toàn bộ ứng dụng nằm trong một file HTML duy nhất, không cần server hay database
- **Local Storage**: Dữ liệu được lưu vào `localStorage` của trình duyệt
- **Dark Theme**: Giao diện tối với màu sắc xanh lá (terminal/hacker aesthetic)
- **Không cần cài đặt**: Chỉ cần mở file trong trình duyệt là sử dụng được

---

## 🗂️ Cấu trúc hệ thống

### 1. 🌳 KNOWLEDGE TREE (Cây tri thức)

Hệ thống phân cấp 4 cấp độ:

| Cấp độ | Tên gọi | Mô tả |
|--------|---------|-------|
| Level 0 | **GỐC (Root)** | Nhánh chính, lĩnh vực lớn |
| Level 1 | **CON (Child)** | Nhánh con trực thuộc Gốc |
| Level 2 | **TÁN (Canopy)** | Nhánh tán - phân nhánh tiếp theo |
| Level 3+ | **LÁ (Leaf)** | Lá - chi tiết cụ thể nhất |

Mỗi node có thể chứa:

- **Children**: Các nhánh con bên dưới
- **Leaves**: Các leaf item ( checklist items )

**Cấu trúc dữ liệu cây:**

```json
{
  "name": "",
  "children": [
    {
      "name": "",
      "children": [
        { "name": "", "children": [], "leaves": [ ] }
      ],
      "leaves": []
    }
  ],
  "leaves": []
}
```

### 2. ♟️ EISENHOWER MATRIX

Ma trận 4 góc phân loại công việc:

| Góc | Màu | Ý nghĩa |
|-----|-----|----------|
| **Q1** | 🔴 Đỏ | Quan trọng + Khẩn cấp (Deadline) |
| **Q2** | 🔵 Xanh dương | Quan trọng + Không khẩn (Planning) |
| **Q3** | 🟡 Vàng | Không quan trọng + Khẩn (Delegate) |
| **Q4** | ⚪ Xám | Không quan trọng + Không khẩn (Eliminate) |

### 3. 📦 TIME BOXING

Bảng quản lý thời gian theo khung giờ:

- Cột **Thời gian**: Khung giờ (VD: 03:00 - 05:00)
- Cột **Mô tả**: Hoạt động trong khung giờ đó
- Cột **Tag**: Phân loại (Q1, Q2, SLEEP, etc.)

### 4. 📊 PROGRESS TRACKER

Theo dõi tiến độ các mục tiêu với checkbox:
- ✅ Hoàn thiện Knowledge Tree HTML
- ✅ Tích hợp Time Boxing
---

## 💾 Lưu trữ dữ liệu

- **Storage Key**: `GM_H_NHANOS_levels_v1`
- **Nền tảng**: `localStorage` API của trình duyệt
- **Định dạng**: JSON string

```javascript
{
  "tree": [...],        // Cấu trúc cây tri thức
  "matrix": {           // Ma trận Eisenhower
    "q1": [...],
    "q2": [...],
    "q3": [...],
    "q4": [...]
  },
  "timebox": [...],     // Mảng các khung thời gian
  "progress": {         // Trạng thái checkbox
    "targetPhan": false,
    "treeHtml": false,
    "timeboxIntegrated": false
  }
}
```

---

## 🎨 Design System

### Màu sắc (Dark Green Terminal Theme)

- **Background**: `#0b1210` (đen xanh)
- **Primary**: `#b1f0da`, `#d2efe3` (xanh lá nhạt)
- **Accent**: `#2a6b53`, `#3f8f72` (xanh lá trung)
- **Text**: `#d2efe3` (xanh trắng)
- **Border**: `#286349`, `#2e7a5e` (xanh lá đậm)

### Typography

- **Font**: `'Courier New', Courier, 'SF Mono', monospace`
- **Headings**: `2.5rem` (h1), `1.8rem` (h2)
- **Body**: `1rem` - `1.15rem`

### UI Components

- **Tabs**: Button-style navigation với active state
- **Cards**: Border-radius 20-24px, shadow nhẹ
- **Inputs**: Border-bottom dotted style
- **Buttons**: Pill shape, dashed border

---

## ⚙️ Cách sử dụng

### Chạy ứng dụng

```bash
# Mở file trong trình duyệt mặc định
open MY_OS.html

# Hoặc dùng VSCode Live Server
```

### Tính năng chính

1. **Thêm/Sửa/Xóa nhánh cây**: Click trực tiếp vào tên để edit
2. **Thêm nhánh con**: Nhấn nút "+ Nhánh con"
3. **Thêm leaf**: Nhấn nút "+ Lá"
4. **Ma trận Eisenhower**: Thêm/sửa task trực tiếp trong các ô
5. **Time Boxing**: Thêm khung giờ mới, edit trực tiếp
6. **Lưu dữ liệu**: Nhấn nút "💾 Lưu toàn bộ"
7. **Reset**: Nhấn "⟲ Reset mặc định" để khôi phục factory settings

---

## 📦 Cấu trúc file

```
MYOS/
└── MY_OS.html          # Single file chứa toàn bộ app
    ├── <style>         # CSS (Dark theme, ~300 lines)
    ├── <body>         # HTML structure
    │   ├── .header    # Logo, mantra, clock
    │   ├── .tabs-nav  # Tab navigation
    │   ├── .tab-panel # Panel content (Tree/Matrix/Timebox)
    │   └── .footer   # Rules & Progress
    └── <script>       # JavaScript (~400 lines)
        ├── DEFAULT_TREE
        ├── DEFAULT_MATRIX
        ├── DEFAULT_TIMEBOX
        └── Functions (render, save, events)
```

---

## 🔒 System Laws (Quy tắc hệ thống)

1. **🐕 Dogfooding** · Sống trong file này - Sử dụng chính công cụ mình tạo ra
2. **🧱 First Principles** · Không giải pháp hời hợt - Giải quyết từ gốc
3. **🔒 Zero Trust** · 2FA tuyệt đối - Bảo mật tối đa
4. **⚡ Consistency > Intensity** · Nhất quán hơn cường độ

---

## 🚀 Tech Stack

- **HTML5**: Semantic markup
- **CSS3**: Custom styles, flexbox/grid
- **JavaScript (ES6+)**: Vanilla JS, no frameworks
- **LocalStorage API**: Persistence
- **No dependencies**: Không cần npm/backend

---

## 📌 Mục tiêu/Roadmap (nếu có)

- [ ] Thêm tính năng export/import JSON
- [ ] Thêm dark/light mode toggle
- [ ] Tích hợp với file system (File System Access API)
- [ ] Thêm keyboard shortcuts
- [ ] PWA support (service worker)

---

## 🆕 Cập nhật (Update Log)

### Phiên bản demo: v1.7 (Notebook LM & Clock Focus)

#### 1. 📓 Notebook LM (Archiver) - Tính năng mới
- **Quản lý ghi chú**: Thêm/sửa/xóa ghi chú với tiêu đề, mô tả, tags
- **Tags system**: Tự động thêm tag với Enter (tự động thêm `#` nếu chưa có), chip tag có thể click để xóa
- **Import/Export**: Hỗ trợ JSON format để sao lưu/khôi phục dữ liệu
- **Tìm kiếm & Sắp xếp**: Lọc theo từ khóa (tiêu đề, mô tả, tags), sắp xếp theo Mới nhất/Cũ nhất/Tiêu đề (A-Z)
- **Lưu trữ**: Dữ liệu lưu trong `localStorage` (key: `GM_H_NHANOS_levels_v1`), `currentTags` không được lưu theo yêu cầu

#### 2. ⏰ Clock Focus - Tính năng mới
- **2 chế độ**: Stopwatch (bấm giờ) và Countdown (đếm ngược)
- **Laps**: Ghi lại các mốc thời gian khi chạy Stopwatch (chỉ khả dụng ở chế độ Stopwatch)
- **Vòng tròn tiến độ**: Hiển thị tiến độ đếm ngược với SVG stroke-dashoffset
- **Quản lý thời gian**: Start/Pause/Reset, tự động báo "⏰ Hết giờ!" khi kết thúc Countdown
- **Khôi phục trạng thái**: `clockMode`, `clockRemaining`, `clockLaps` được khôi phục khi reload (không khôi phục `clockElapsed` và `clockIsRunning` theo yêu cầu)

#### 3. 🔧 Cập nhật hệ thống
- **State mở rộng**: Thêm `archiverItems`, `currentTags`, `clockMode`, `clockIsRunning`, `clockElapsed`, `clockRemaining`, `clockLaps`
- **Persistence**: Cập nhật `loadState()`/`saveState()` để xử lý dữ liệu mới (không lưu `currentTags`)
- **UI Integration**: Thêm tab Notebook với 2 sub-tab (Text/Archiver), tab Clock Focus
- **Event Handling**: Thêm event delegation cho Archiver list, keyboard events (Enter) cho tag input

#### 4. 📦 Cấu trúc file cập nhật
- **JavaScript**: Thêm ~300 dòng code cho Archiver (CRUD, tags, import/export, filter/sort) và Clock (stopwatch/countdown, laps, progress circle)
- **CSS**: Thêm styles cho `.archiver-*`, `.clock-*` components
- **HTML**: Thêm UI cho Notebook Archiver panel và Clock Focus panel

---

## 👤 Tác giả

**"GM_H_NHAN**"

---

## 📄 License

MIT License - Tự do sử dụng và mod theo nhu cầu.

---

*Build with 💚 for personal productivity*
