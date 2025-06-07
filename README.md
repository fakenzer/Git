# Git Cơ Bản Cho Developer

---

## I. Khởi tạo và Cấu hình Git

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git init` | Tạo repo Git local | Khi bắt đầu project mới |
| `git config --global user.name "Tên"` | Đặt tên commit | Lần đầu cấu hình Git |
| `git config --global user.email "email@example.com"` | Gán email cho commit | Bắt buộc để commit hiển thị đúng danh tính |

---

## II. Làm việc với Remote Repository

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git clone <url>` | Clone toàn bộ repo từ remote | Khi bắt đầu làm việc với project có sẵn |
| `git remote -v` | Hiển thị các remote | Kiểm tra repo liên kết với đâu |
| `git remote add origin <url>` | Gán remote tên `origin` | Khi repo tạo local trước rồi mới push |

---

## III. Clone một nhánh KHÔNG phải nhánh mặc định

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git clone --branch <branch-name> <url>` | Clone repo và checkout luôn nhánh mong muốn | Tiết kiệm thời gian, tải ít dữ liệu hơn |
| `git checkout <branch>` | Chuyển sang nhánh khác sau khi đã clone | Khi cần làm việc trên nhánh phụ (ví dụ `develop`) |

---

## IV.  Quản lý File và Commit

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git status` | Xem trạng thái file | Kiểm tra trước khi commit |
| `git add <file>` | Đưa file vào staged area | Chọn file cụ thể để commit |
| `git add .` | Đưa tất cả file thay đổi vào staged | Khi commit toàn bộ dự án |
| `git commit -m "msg"` | Commit với nội dung mô tả | Sau khi staging hoàn tất |
| `git commit -am "msg"` | Staging + commit nhanh file đã track | Rút gọn thao tác |

---

## V. Làm việc với Branch

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git branch` | Danh sách branch | Kiểm tra nhánh hiện có |
| `git checkout -b <branch>` | Tạo và chuyển nhánh mới | Khi bắt đầu feature mới |
| `git merge <branch>` | Gộp branch vào nhánh hiện tại | Sau khi hoàn thành tính năng |
| `git branch -d <branch>` | Xoá branch | Dọn dẹp sau khi merge xong |

---

## VI. Push & Pull

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git push origin <branch>` | Push nhánh lên remote | Đồng bộ code lên GitHub |
| `git pull origin <branch>` | Kéo code từ remote về local | Cập nhật thay đổi từ team |
| `git fetch` | Lấy thay đổi từ remote nhưng không merge | Kiểm tra thay đổi mà chưa áp dụng |

---

## VII. Lịch sử và So sánh

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git log` | Xem lịch sử commit | Debug, tra cứu code |
| `git log --oneline --graph` | Lịch sử dạng cây rút gọn | Rõ ràng khi repo có nhiều nhánh |
| `git diff` | So sánh code chưa commit | Kiểm tra thay đổi cục bộ |

---

## VIII.  Reset & Khôi phục

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git restore <file>` | Huỷ thay đổi chưa commit | Hoàn tác sửa file |
| `git reset HEAD <file>` | Bỏ file khỏi staged | Khi add nhầm |
| `git reset --hard <commit>` | Trở về trạng thái tại commit (mất dữ liệu sau) | Cực kỳ cẩn thận khi dùng! |

---

## IX. Tag (Phiên bản)

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git tag v1.0` | Gắn tag cho phiên bản | Khi release |
| `git push origin v1.0` | Đẩy tag lên remote | Chia sẻ tag với team |
| `git tag` | Liệt kê tag | Xem các bản release |

---

## X. Stash – Lưu Tạm Thời

| Lệnh | Mô tả | Khi nào dùng |
|------|-------|--------------|
| `git stash` | Lưu thay đổi chưa commit tạm thời | Khi đang làm dở nhưng cần chuyển nhánh |
| `git stash pop` | Lấy lại stash mới nhất | Khi quay lại công việc dở dang |

---

## XI. Làm Việc Với Fork và Repo Chính (Upstream)

> Quy trình tiêu chuẩn khi bạn làm việc với một repo đã **fork từ GitHub**.

### 1. Thêm remote của repo gốc (upstream)
```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/REPO.git
```
- Dùng để: theo dõi và đồng bộ cập nhật từ repo gốc.

### 2. Lấy thay đổi mới nhất từ upstream
```bash
git fetch upstream
```
- Dùng để: lấy các commit mới từ repo gốc về máy local.

### 3. Gộp thay đổi từ upstream vào nhánh chính của bạn
```bash
git checkout main
git merge upstream/main
```
- Dùng để: cập nhật fork theo repo gốc.

### 4. Push cập nhật từ fork local lên GitHub
```bash
git push origin main
```
- Dùng để: cập nhật repo fork cá nhân sau khi merge.

### 5. Kiểm tra remote hiện tại
```bash
git remote -v
```

#### Kết quả mong muốn:
```bash
origin    https://github.com/BAN_THAN/forked-repo.git
upstream  https://github.com/TAC_GIA/original-repo.git
```
> [!TIP]
> 
> - Tạo pull request từ origin/feature-x sang upstream/main để đóng góp code.
> 
> - Dùng _.gitignore_ để bỏ qua các file không cần track (node_modules, v.v.).
> 
> - Luôn pull/update upstream thường xuyên để tránh xung đột.










