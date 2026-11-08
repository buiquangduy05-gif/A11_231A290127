# Báo Cáo Thực Hành Lab A11: Dialog, Toast & Menu

> **Sinh viên:** Bùi Quang Duy - **MSSV:** 231A290127  
> **Package:** `vn.edu.vhu.ltdd.a11dialog`

---

## Các bài nâng cao đã thực hiện

### 🌟 Bài nâng cao NC1: Thêm SearchView vào Options Menu để tìm kiếm món ăn theo thời gian thực
- **Mục tiêu:** Cho phép người dùng tìm kiếm món ăn nhanh chóng khi đang gõ từ khóa.
- **Thực hiện:**
  - Bổ sung `<item android:id="@+id/action_tim_kiem" app:actionViewClass="androidx.appcompat.widget.SearchView" app:showAsAction="always|collapseActionView" />` vào `menu_main.xml`.
  - Trong `MainActivity.java`, lắng nghe sự kiện qua `searchView.setOnQueryTextListener`:
    - `onQueryTextChange(String newText)`: Lọc danh sách món ăn theo thời gian thực (real-time) dựa trên chuỗi tên món không phân biệt hoa thường.
    - Cập nhật đồng bộ giữa danh sách gốc và danh sách hiển thị khi thêm, sửa, xóa hoặc hoàn tác.
