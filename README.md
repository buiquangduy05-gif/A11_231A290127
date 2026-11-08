# Báo Cáo Thực Hành Lab A11: Dialog, Toast & Menu

> **Trường Đại học Văn Hiến (VHU)**  
> **Khoa Công nghệ Thông tin**  
> **Môn học:** INT4211 – Lập trình trên các thiết bị di động  
> **Sinh viên thực hiện:** Bùi Quang Duy  
> **Mã số sinh viên (MSSV):** 231A290127  
> **Package name:** `vn.edu.vhu.ltdd.a11dialog`  

---

## 📱 1. Giới thiệu dự án

Dự án **A11_231A290127** là bản nâng cấp trực tiếp từ ứng dụng thực đơn của **Lab A9**, bổ sung các cơ chế giao tiếp và điều khiển chuẩn trong Android:
1. **Options Menu (`res/menu/menu_main.xml`):** Thanh tiêu đề hiển thị nút Thêm món (`+` với `showAsAction="always"`) và menu 3 chấm (`⋮` với `showAsAction="never"`) gồm: *Sắp xếp theo tên*, *Sắp xếp theo giá*, và *Xóa tất cả*.
2. **Context Menu (`res/menu/menu_context.xml`):** Nhấn giữ lâu một dòng trong `ListView` sẽ mở menu ngữ cảnh có tiêu đề là tên món ăn đó cùng 2 tùy chọn: *Sửa món* và *Xóa*.
3. **AlertDialog thông báo & xác nhận:**
   * Chạm vào một dòng để xem chi tiết món ăn bằng `AlertDialog`.
   * Hỏi xác nhận rõ ràng tên món trước khi xóa một món hoặc xóa toàn bộ thực đơn.
4. **Custom AlertDialog (`res/layout/dialog_mon_an.xml`):** Hộp thoại tự thiết kế bằng `setView()` để Thêm/Sửa món ăn, tích hợp kiểm tra dữ liệu hợp lệ (tên không trống, giá là số nguyên dương) và **không tự đóng hộp thoại khi dữ liệu sai** bằng kỹ thuật ghi đè `OnClickListener` của `BUTTON_POSITIVE` sau khi gọi `dialog.show()`.
5. **Toast & Snackbar Hoàn tác (Undo):**
   * Dùng `Toast` cho các thông báo ngắn gọn (đã thêm, đã sửa, đã sắp xếp).
   * Dùng `Snackbar` kèm nút **HOÀN TÁC** khi xóa món ăn hoặc xóa toàn bộ thực đơn, khôi phục món ăn về **đúng vị trí cũ** (`danhSach.add(viTri, daXoa)`).

---

## 📋 2. Bảng kiểm thử 8 kịch bản

| # | Thao tác | Kết quả đúng phải thấy |
|---|----------|------------------------|
| **1** | Mở app, nhìn thanh tiêu đề | Thấy biểu tượng `+` và nút ba chấm `⋮` trên thanh tiêu đề. |
| **2** | Mở menu ba chấm | Có đủ 3 mục: *Sắp xếp theo tên*, *Sắp xếp theo giá*, *Xóa tất cả*. |
| **3** | Chọn *Sắp xếp theo giá* | Danh sách xếp lại theo giá tăng dần, `Toast` báo *"Đã sắp xếp theo giá tăng dần"*. |
| **4** | Giữ lâu một dòng | Context menu hiện lên, tiêu đề của menu là tên đúng món ăn ở dòng đó. |
| **5** | Chọn *Xóa* trong context menu | Hộp thoại `AlertDialog` hỏi xác nhận, nêu rõ tên món sắp xóa. |
| **6** | Bấm *Hủy* trong hộp thoại | Hộp thoại đóng lại, không xóa gì cả, danh sách giữ nguyên. |
| **7** | Bấm *Xóa* rồi bấm *HOÀN TÁC* | Món ăn bị xóa tạm thời rồi trở lại **đúng vị trí cũ** trong danh sách. |
| **8** | Mở dialog *Sửa*, xóa trắng ô tên rồi bấm *Lưu* | Báo lỗi `"Chưa nhập tên món"` ngay tại ô tên, hộp thoại **không bị đóng**. |

---

## 📂 3. Cấu trúc thư mục mã nguồn

```
A11_231A290127/
├── app/
│   ├── src/main/java/vn/edu/vhu/ltdd/a11dialog/
│   │   ├── MainActivity.java         # Xử lý Options Menu, Context Menu, AlertDialog, Toast, Snackbar
│   │   ├── MonAn.java                # Lớp dữ liệu món ăn & định dạng giá tiền
│   │   └── MonAnAdapter.java         # Custom BaseAdapter sử dụng ViewHolder
│   └── src/main/res/
│       ├── layout/
│       │   ├── activity_main.xml     # Giao diện chính gồm ListView và EmptyView
│       │   ├── dialog_mon_an.xml     # Giao diện hộp thoại Thêm / Sửa món ăn
│       │   └── item_mon_an.xml       # Giao diện từng dòng món ăn
│       ├── menu/
│       │   ├── menu_main.xml         # Options menu trên thanh tiêu đề
│       │   └── menu_context.xml      # Context menu khi giữ lâu dòng
│       └── values/
│           ├── strings.xml           # Tài nguyên chuỗi tiếng Việt
│           └── themes.xml            # Theme Material3 có ActionBar hiển thị Menu
└── README.md
```
