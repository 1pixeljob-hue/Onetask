# 🚀 Hướng dẫn Deployment

## 📋 Yêu cầu

- ✅ GitHub repository
- ✅ FTP hosting với Node.js support
- ✅ GitHub Secrets đã config

---

## 🔧 Setup lần đầu

### 1️⃣ Tạo Workflow File trên GitHub

**Path:** `.github/workflows/deploy-frontend-ftp.yml`

**Nội dung:** Copy từ file `/github-workflows-deploy-frontend-ftp.yml`

### 2️⃣ Add GitHub Secrets

Vào: `Settings → Secrets and variables → Actions`

**4 secrets cần thêm:**

```
FTP_SERVER      = ftp.yourdomain.com
FTP_USERNAME    = user@yourdomain.com
FTP_PASSWORD    = your-password
FTP_SERVER_DIR  = /public_html/
```

⚠️ **LƯU Ý:** `FTP_SERVER_DIR` PHẢI CÓ `/` Ở CUỐI!

### 3️⃣ Update Production URL

Sửa file `.env.production`:

```env
VITE_API_URL=https://yourdomain.com/api
```

Thay `yourdomain.com` bằng domain thực của bạn.

---

## 🎯 Workflow tự động

### Trigger khi nào?

✅ **Tự động chạy khi:**
- Push code lên branch `main`
- Files thay đổi KHÔNG phải `backend/**` hoặc `*.md`

✅ **Manual trigger:**
- Vào `Actions → 🎨 Deploy Frontend to Hosting`
- Click `Run workflow`

### Các bước workflow

```
1. Checkout code              (~10s)
2. Setup Node.js v18           (~10s)
3. Install dependencies        (~60-90s)
4. Build production            (~90-120s)
5. Debug - List build output   (~5s)
6. Deploy to FTP               (~60-180s)
```

**Tổng thời gian:** ~5-7 phút

---

## 🐛 Troubleshooting

### Build failed?

**Lỗi:** `Error: Cannot find module 'xxx'`

**Giải pháp:**
```bash
# Local test:
npm install
npm run build
```

---

### Deploy failed - ENOENT dist/?

**Lỗi:** `ENOENT: no such file or directory, scandir './dist/'`

**Nguyên nhân:** Build không tạo folder `dist/`

**Giải pháp:**
- Check logs bước "Debug - List build output"
- Verify `vite.config.ts` có `outDir: 'dist'`
- Check `index.html` có đúng entry point `/main.tsx`

---

### FTP connection failed?

**Lỗi:** `Error: Connection timeout` hoặc `Authentication failed`

**Giải pháp:**
- Verify 4 GitHub Secrets
- Test FTP credentials bằng FileZilla
- Check `FTP_SERVER_DIR` có `/` cuối
- Check hosting có bật FTP access

---

## 📊 Verify Deployment

### 1. Check workflow logs

```
Actions → Latest workflow run → View logs
```

### 2. Check website

```
https://yourdomain.com
```

Hard refresh: `Ctrl + Shift + R` (Win) hoặc `Cmd + Shift + R` (Mac)

### 3. Check backend connection

Open Browser DevTools → Console

Xem có lỗi API call không:
```
Failed to fetch: https://yourdomain.com/api/...
```

Nếu có → Update `.env.production` với URL đúng

---

## ✅ Success Checklist

- [ ] Workflow file đã tạo trên GitHub
- [ ] 4 GitHub Secrets đã add
- [ ] `.env.production` đã update URL
- [ ] Workflow chạy thành công (✅ Complete)
- [ ] Website accessible qua domain
- [ ] No console errors
- [ ] Backend API connected

---

## 🔄 Quy trình hàng ngày

**Từ Figma Make:**

```
1. Code changes in Figma Make
2. Push to GitHub (automatic)
3. GitHub Actions auto-trigger
4. Build + Deploy (5-7 mins)
5. Website updated! ✅
```

**ZERO manual work!** 🎉

---

## 📞 Support

Nếu gặp lỗi, check:

1. **Workflow logs** - Chi tiết lỗi ở đâu
2. **GitHub Secrets** - Có đúng không?
3. **FTP credentials** - Test bằng FileZilla
4. **Build local** - `npm run build` có OK không?

---

**Last updated:** 2025-03-18
