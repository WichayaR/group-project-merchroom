# 🚀 JSD13 Group Project Checklist

เอกสารนี้รวบรวม Requirement และ Rubric การประเมินผลสำหรับ MERN Stack E-Commerce Group Project (Sprint 1 - 3 และ Sprint Retrospective) 
---

## 📌 Project Overview & General Constraints
- **Architecture:** MERN Stack (MongoDB, Express, React, Node.js)[cite: 1]
- **Scope:** E-Commerce Business Application (ไม่ใช่ Marketplace)[cite: 1]
- **Payment:** ไม่ต้องเชื่อมต่อระบบชำระเงินจริง (จำลองการชำระเงินได้)[cite: 1]
- **Deployment:** ทั้ง Frontend (React) และ Backend (Express API) ต้อง Deploy ขึ้น Public URL[cite: 1]

---

## 🗓️ Sprint 1: Architecture & UI/UX Wireframes

### 1. Database & System Design Requirements
- [ ] **Business Model Canvas:** ออกแบบโมเดลธุรกิจของแอพ[cite: 1]
- [ ] **Use Case Diagram & ER Diagram:** ออกแบบให้ครอบคลุมทุก Input Field ของระบบ[cite: 1]
- [ ] **MongoDB Schema Design:** ออกแบบ Schema ที่สอดคล้องกับ ER Diagram[cite: 1]

### 2. Wireframe / UI Layout Requirements
- [ ] **Product Card Components:**
  - Product Name[cite: 1]
  - Description[cite: 1]
  - Price[cite: 1]
  - Quantity & Button "Add-to shopping cart"[cite: 1]
  - Product Tags[cite: 1]
- [ ] **Landing Page:** แสดงรายการสินค้าทั้งหมดในระบบ[cite: 1]
- [ ] **Product List Layout:** แสดงผล Product Card อย่างน้อย 3 ชนิด พร้อม 3 Tags ที่แตกต่างกัน[cite: 1]
- [ ] **Shopping Cart & Checkout Page:** หน้ารถเข็น และหน้ายืนยันคำสั่งซื้อ (ต้องมี Purchase Date/Time)[cite: 1]
- [ ] **Authentication Layouts:**
  - Registration Form (Email, First Name, Last Name, Password, Password Confirmation)[cite: 1]
  - Login Form (Email & Password)[cite: 1]
  - Forget Password Form[cite: 1]
- [ ] **Dashboards (Data Visualization Charts อย่างน้อย 2 ชนิด):**
  - **User UI:** Profile, Order Status, Order History[cite: 1]
  - **Admin UI:** Revenue Chart, Average Order Chart, Inventory Management[cite: 1]

---

## 💻 Sprint 2: Frontend & API Mocking

### 1. React Component & Form Validation
- [ ] **Form Validation (Client-Side):** ตรวจสอบข้อมูลก่อนส่งฟอร์ม (Name, Description, Price, Quantity, Date, Tag)[cite: 1]
- [ ] **Error Handling:** แสดงข้อความ Error ที่ชัดเจนเมื่อข้อมูลไม่ถูกต้อง[cite: 1]
- [ ] **React Components:** แยก Component ให้ชัดเจนสำหรับ Product, Product List, Cart, Checkout[cite: 1]

### 2. Frontend Cart Management Methods
- [ ] **READ (GET):** ดึงรายการสินค้าใน cart ของ User (`/products/:user_id` หรือ `/cart`)[cite: 1]
- [ ] **CREATE (POST):** เพิ่มสินค้าเข้า cart[cite: 1]
- [ ] **UPDATE (PUT):** อัปเดตจำนวนสินค้าใน cart[cite: 1]
- [ ] **DELETE (DELETE):** ลบสินค้าออกจาก cart[cite: 1]

### 3. Admin Features (Product Management)
- [ ] **Fetch (GET):** ดึงรายการสินค้าทั้งหมดมาแสดงผล[cite: 1]
- [ ] **Create (POST):** เพิ่มสินค้าใหม่เข้าสู่ระบบ[cite: 1]
- [ ] **Update (PUT):** แก้ไขข้อมูลสินค้าในระบบ[cite: 1]
- [ ] **Delete (DELETE):** ลบสินค้าออกจากระบบ[cite: 1]

### 4. Database Setup
- [ ] ติดตั้ง Mongoose และตั้งค่าการเชื่อมต่อ MongoDB โดยไม่มี Error[cite: 1]

---

## ⚙️ Sprint 3: Full-Stack Integration & Deployment

### 1. Database Operations (Mongoose Integration)
- [ ] เชื่อมต่อ CRUD Operations ของสินค้าใน Database (READ, CREATE, UPDATE, DELETE)[cite: 1]
- [ ] เชื่อมต่อ CRUD Operations ของ Cart/Basket/Order ใน Database[cite: 1]

### 2. RESTful API Standards
- [ ] **POST:** สร้างข้อมูลใหม่ (Create)[cite: 1]
- [ ] **GET:** อ่าน/ดึงข้อมูล (Read)[cite: 1]
- [ ] **PUT / PATCH:** แก้ไขข้อมูล (Update)[cite: 1]
- [ ] **DELETE:** ลบข้อมูล (Delete)[cite: 1]

### 3. Deployment
- [ ] **React Application:** Deploy และเข้าถึงผ่าน Public URL ได้[cite: 1]
- [ ] **Express API:** Deploy และเข้าถึงผ่าน Public URL ได้[cite: 1]
- [ ] **Integration Test:** React และ Express สื่อสารข้อมูลกันได้อย่างถูกต้องบนระบบ Production[cite: 1]

---

## 🧠 Sprint Retrospective: Behavioral & Mindsets (Self-Check)

### Mindsets Checklist
- [ ] **Personal Responsibility:** ตรงต่อเวลา ส่งงานครบ ถือโอกาสเรียนรู้อย่างเต็มที่[cite: 1]
- [ ] **Growth Mindset:** กล้าลองสิ่งใหม่ รับและเปิดใจฟัง Feedback เพื่อนำมาพัฒนา[cite: 1]
- [ ] **Future Orientation:** ตั้งเป้าหมาย SMART Goals เชื่อมโยงสิ่งที่เรียนกับอาชีพในอนาคต[cite: 1]
- [ ] **Persistence:** สู้ไม่ถอยเมื่อเจอ Bug หรือปัญหาทาง Technical[cite: 1]

### Behavioral Skills Checklist
- [ ] **Time Management:** บริหารเวลาและจัดลำดับความสำคัญของงานได้ดี[cite: 1]
- [ ] **Teamwork:** ฟังและสื่อสารกับเพื่อนในทีมอย่างมีประสิทธิภาพ[cite: 1]
- [ ] **Proactiveness:** ริเริ่มช่วยงานหรือแก้ไขปัญหาโดยไม่ต้องรอสั่ง[cite: 1]
- [ ] **Orientation to Detail:** ตรวจสอบโค้ด ละเอียดใส่ใจในการแก้อีกเล็กๆ น้อยๆ[cite: 1]

---
