# 🎨 1Pixel Management System

**Hệ thống quản lý công việc tập trung** với 7 modules chuyên nghiệp

---

## 🌟 Tính năng

### 📊 **Dashboard**
- Tổng quan doanh thu theo tháng
- Thống kê tasks, customers, invoices
- Biểu đồ doanh thu theo ngày

### 🌐 **Hosting Management**
- Quản lý danh sách hosting
- Theo dõi ngày hết hạn
- Tính toán tổng chi phí

### 🔐 **Password Manager**
- Lưu trữ passwords an toàn
- Tìm kiếm nhanh
- Copy to clipboard

### 💻 **CodeX (Code Repository)**
- Quản lý code snippets
- Syntax highlighting
- Lọc theo ngôn ngữ

### 👥 **Client Management**
- Quản lý danh sách khách hàng
- Lịch sử projects
- Contact tracking

### 📋 **Tasks**
- Todo list với priority
- Status tracking
- Deadline management

### 📄 **Invoices**
- Tạo hóa đơn
- Theo dõi thanh toán
- Tính tổng doanh thu

---

## 🎨 Design System

**Màu chủ đạo:**
- **Teal:** `#4DBFAD` - Primary actions
- **Blue:** `#2563B4` - Links & secondary

**Typography:**
- Font: System font stack (SF Pro, Segoe UI, etc.)
- Sizing: Tailwind default scale

**Ngày tháng:** `dd/mm/yyyy` (VN format)

**Tiền tệ:** `VNĐ` with thousands separator

---

## 🛠️ Tech Stack

### **Frontend**
- ⚛️ React 18 + TypeScript
- 🎨 Tailwind CSS v4
- 🧭 React Router v7
- 📊 Recharts (charts)
- 🎭 Motion (animations)
- 🍞 Sonner (toast notifications)

### **Backend**
- 🟢 Node.js + Express
- 🗄️ MySQL Database
- 🔐 bcrypt (password hashing)
- 📁 File-based sessions

---

## 📦 Cài đặt

### **Development**

```bash
# Install dependencies
npm install

# Run dev server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### **Environment Variables**

**Development (`.env`):**
```env
VITE_API_URL=http://localhost:5000/api
```

**Production (`.env.production`):**
```env
VITE_API_URL=https://yourdomain.com/api
```

---

## 🚀 Deployment

### **Auto-deployment via GitHub Actions**

Xem chi tiết: [DEPLOYMENT.md](./DEPLOYMENT.md)

**Workflow:**
```
Figma Make → GitHub → Build → FTP Deploy → Live! ✅
```

**Requirements:**
- GitHub repository
- FTP hosting với Node.js
- 4 GitHub Secrets configured

---

## 🔐 Authentication

**Default Admin:**
```
Username: quydev
Password: Spencil@123
```

⚠️ **LƯU Ý:** Đổi password sau lần đầu đăng nhập!

---

## 📁 Project Structure

```
1pixel-management-system/
├── backend/              # Node.js API
│   ├── routes/          # API endpoints
│   ├── db/              # MySQL connection
│   └── server.js        # Express server
├── components/          # React components
├── styles/             # Global CSS + Tailwind
├── utils/              # API client & helpers
├── App.tsx             # Main component
├── main.tsx            # Entry point
└── vite.config.ts      # Build config
```

---

## 🐛 Troubleshooting

### **Build errors?**
```bash
npm install
npm run build
```

### **API connection failed?**
- Check `.env.production` URL
- Verify backend is running
- Check CORS settings

### **Login không hoạt động?**
- Check backend `/api/auth/login` endpoint
- Verify MySQL database connected
- Check browser console for errors

---

## 📝 License

© 2025 1Pixel - All rights reserved

---

## 👨‍💻 Developer

**quydev** - Full Stack Developer

📧 Contact: [Your email]

🌐 Website: [Your website]

---

**Version:** 2.0.0 (MySQL Migration)

**Last updated:** 18/03/2026
