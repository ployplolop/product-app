# Product App

แอปแสดงรายการสินค้า พัฒนาด้วย Vue 3 + Vite  
ดึงข้อมูลสินค้าจาก n8n Webhook แล้วแสดงเป็นตาราง

## ฟีเจอร์หลัก

- แสดงรายการสินค้า (รหัส, ชื่อ, จำนวน, ราคา) ในรูปแบบตาราง
- ดึงข้อมูลจาก API ผ่าน n8n Webhook
- มีสถานะ Loading / Error / ไม่พบข้อมูล

## วิธีใช้งาน

```bash
npm install
npm run dev
```

เปิดเบราว์เซอร์ไปที่ http://localhost:5173

## เทคโนโลยีที่ใช้

- Vue 3 (Composition API)
- Vite
- n8n Webhook (Backend API)
