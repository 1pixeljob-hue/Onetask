# 🔧 Hướng dẫn Setup GitHub Workflow

## 📋 BƯỚC 1: Tạo Workflow File

### ✅ Bạn ĐÃ HOÀN THÀNH bước này!

---

## 📋 BƯỚC 2: Update Workflow trên GitHub

### **Tại sao cần update?**

Workflow file cũ thiếu bước debug → build failed không rõ lỗi

### **Cách update:**

#### **Option 1: Edit trực tiếp (KHUYẾN NGHỊ)**

1. Vào GitHub repository:
   ```
   https://github.com/1pixeljob-hue/Onetask
   ```

2. Navigate to workflow file:
   ```
   .github/workflows/deploy-frontend-ftp.yml
   ```

3. Click nút **"Edit"** (icon bút chì)

4. **REPLACE TOÀN BỘ** nội dung bằng code này:

```yaml
name: 🎨 Deploy Frontend to Hosting

on:
  push:
    branches:
      - main
    paths-ignore:
      - 'backend/**'
      - '**.md'
      - '.gitignore'
  workflow_dispatch:

jobs:
  deploy:
    name: 🚀 Build & Deploy Frontend
    runs-on: ubuntu-latest
    
    steps:
      - name: 📥 Checkout code
        uses: actions/checkout@v4

      - name: ⚙️ Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: 📦 Install dependencies
        run: npm install

      - name: 🏗️ Build production
        run: npm run build
        env:
          NODE_ENV: production

      - name: 🔍 Debug - List build output
        run: |
          echo "=== Checking build output ==="
          ls -la
          if [ -d "dist" ]; then
            echo "✅ dist/ folder exists"
            ls -la dist/
          else
            echo "❌ dist/ folder NOT found!"
            exit 1
          fi

      - name: 📤 Deploy to FTP
        uses: SamKirkland/FTP-Deploy-Action@v4.3.5
        with:
          server: ${{ secrets.FTP_SERVER }}
          username: ${{ secrets.FTP_USERNAME }}
          password: ${{ secrets.FTP_PASSWORD }}
          server-dir: ${{ secrets.FTP_SERVER_DIR }}
          local-dir: ./dist/
          dangerous-clean-slate: false
          exclude: |
            **/.git*
            **/.git*/**
            **/node_modules/**
            **/.env*
```

5. **Commit changes:**
   - Message: `Fix workflow - add debug step and config files`
   - Click **"Commit changes"**

---

#### **Option 2: Push từ Figma Make (SAU KHI ĐỌC GUIDE NÀY)**

**Cách này tự động update khi bạn push từ Figma Make!**

---

## 📋 BƯỚC 3: Verify Files mới

### **Files đã được thêm:**

✅ `tsconfig.node.json` - TypeScript config cho Vite
✅ `.env.example` - Template cho env vars
✅ `.env.production` - Production env vars
✅ `.gitignore` - Ignore build folders
✅ `.npmrc` - NPM config
✅ `DEPLOYMENT.md` - Deployment guide
✅ `README.md` - Project documentation

### **Files đã được update:**

✅ `tsconfig.json` - Thêm references
✅ `github-workflows-deploy-frontend-ftp.yml` - Thêm debug step

---

## 📋 BƯỚC 4: Push Changes từ Figma Make

### **Sau khi đọc xong guide này:**

1. **Từ Figma Make**, push code lên GitHub:
   ```
   All changes pushed to GitHub! ✅
   ```

2. **Workflow sẽ tự động chạy** do có changes trong files

3. **Monitor workflow:**
   ```
   GitHub → Actions → Latest run
   ```

---

## 📋 BƯỚC 5: Test lại Workflow

### **1. Vào Actions:**

```
https://github.com/1pixeljob-hue/Onetask/actions
```

### **2. Check latest run:**

Nếu workflow đang chạy từ push auto:
- ✅ **Chờ kết quả**
- Xem logs để verify

Nếu chưa chạy hoặc muốn test manual:
- Click **"Run workflow"**
- Select branch: `main`
- Click **"Run workflow"**

### **3. Monitor từng bước:**

```
✅ Set up job
✅ Checkout code
✅ Setup Node.js
✅ Install dependencies
✅ Build production
✅ Debug - List build output  ← BÁO KẾT QUẢ BƯỚC NÀY!
```

**Nếu bước Debug pass:**
```
✅ dist/ folder exists
dist/
  index.html
  assets/
    index-[hash].js
    index-[hash].css
```

→ **HOÀN HẢO!** Tiếp tục deploy

**Nếu bước Debug fail:**
```
❌ dist/ folder NOT found!
```

→ **Báo tôi ngay!** Có vấn đề với build config

---

## 🎯 Expected Results

### **Success scenario:**

```
✅ Checkout code (10s)
✅ Setup Node.js (10s)
✅ Install dependencies (60-90s)
✅ Build production (90-120s)
✅ Debug - List build output (5s)
    → ✅ dist/ folder exists
    → dist/index.html found
    → dist/assets/ found
✅ Deploy to FTP (60-180s)
✅ Complete job

🎉 Deployment successful!
```

**Time:** ~5-7 phút

**Kết quả:**
```
https://yourdomain.com → Website live! ✅
```

---

## 🐛 Troubleshooting

### **Scenario 1: Build thành công NHƯNG không có dist/**

**Logs:**
```
Build production: ✅
Debug step: ❌ dist/ folder NOT found!
```

**Nguyên nhân:**
- Vite build output vào folder khác (không phải `dist/`)
- `vite.config.ts` có `outDir` khác

**Giải pháp:**
1. Check logs bước "Build production"
2. Tìm dòng: `✓ built in XXXs`
3. Xem output folder nào
4. Báo tôi output folder name!

---

### **Scenario 2: Build failed hoàn toàn**

**Logs:**
```
Build production: ❌ Error: ...
```

**Nguyên nhân:**
- Missing dependencies
- TypeScript errors
- Missing files

**Giải pháp:**
1. Copy FULL error message
2. Báo tôi chi tiết lỗi
3. Tôi sẽ fix ngay!

---

### **Scenario 3: Deploy failed - Cannot find dist/**

**Logs:**
```
Build production: ✅
Debug step: ✅ dist/ exists
Deploy to FTP: ❌ ENOENT: no such file or directory
```

**Nguyên nhân:**
- Timing issue (dist/ bị xóa?)
- Workflow step order sai

**Giải pháp:**
- Báo tôi full logs
- Tôi sẽ adjust workflow

---

## 📞 Khi nào báo tôi?

### **✅ BÁO NGAY nếu:**

1. **Bước Debug FAILED:**
   ```
   ❌ dist/ folder NOT found!
   ```
   → Copy full logs bước Build + Debug

2. **Build lỗi:**
   ```
   Error: Cannot find module 'xxx'
   Error: TS2304: Cannot find name 'xxx'
   ```
   → Copy full error stack

3. **Deploy lỗi MẶC DÙ Debug pass:**
   ```
   Debug: ✅ dist/ exists
   Deploy: ❌ ENOENT
   ```
   → Copy logs cả 2 bước

### **✅ BÁO SUCCESS nếu:**

```
All steps: ✅
Website: LIVE tại https://yourdomain.com
```

→ **HOÀN HẢO!** Setup xong! 🎉

---

## 🎯 Next Steps sau khi Success

1. **Update Production URL:**
   - Edit `.env.production`
   - Change `VITE_API_URL` to your real domain
   - Push lại từ Figma Make

2. **Setup Backend deployment:**
   - Tạo workflow riêng cho backend
   - Auto-restart Node.js khi có changes

3. **Monitor & Optimize:**
   - Check deployment time
   - Optimize bundle size nếu cần

---

**Chúc may mắn!** 🚀🦆

---

**Created:** 18/03/2026

**Status:** ⏳ Waiting for test results
