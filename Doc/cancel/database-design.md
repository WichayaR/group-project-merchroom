# 🗄️ Database Design - Merchroom

MERN Stack E-Commerce (ขายเอง ไม่ใช่ Marketplace) · MongoDB + Mongoose
Diagram: `database-er-diagram.excalidraw`

---

## 📖 คำศัพท์ที่ใช้ในเอกสารนี้ (อ่านก่อน)

- **PK** (Primary Key = คีย์หลัก) — ค่าที่ไม่ซ้ำกัน ใช้ระบุเอกสารแต่ละตัว เช่น `_id`
- **FK** (Foreign Key = คีย์ต่างประเทศ) — ค่าที่อ้างอิงไปยัง `_id` ของอีก collection เพื่อเชื่อมความสัมพันธ์
- **String** (สตริง = ข้อความ) — ชนิดข้อมูลข้อความ เช่น ชื่อ, อีเมล
- **Number** (ตัวเลข) — ชนิดข้อมูลตัวเลข เช่น ราคา, จำนวน
- **[String]** (อาร์เรย์ของข้อความ) — เก็บได้หลายค่าที่เป็นข้อความใน field เดียว เช่น รายการ tags
- **ObjectId** (รหัสเอกสาร) — ชนิดรหัสประจำตัวของ MongoDB เก็บใน `_id`
- **Date** (วันที่/เวลา) — ชนิดข้อมูลวันเวลา
- **required** (จำเป็น/บังคับ) — ต้องมีค่านี้เสมอ ห้ามว่าง/ไม่มี
- **unique** (ไม่ซ้ำ) — ห้ามมีค่าซ้ำกันใน collection นี้ เช่น email
- **hashed** (เข้ารหัส) — ผ่านการ hash (BCrypt) แล้ว ไม่เก็บรหัสผ่านแบบข้อความตรงๆ
- **embedded** (ฝังอยู่) — ข้อมูลย่อยที่ฝังในเอกสารเดียวกัน ไม่ได้แยกเป็น collection
- **snapshot** (ภาพจำลองตอนนั้น) — เก็บค่าตอนบันทึกไว้ เพื่อกันข้อมูลเปลี่ยนภายหลัง

---

## 👥 ระบบบทบาท (Role)

แยกเป็น **2 Collection** ตามบทบาท:

| Collection | บทบาท | สิทธิ์ |
|------------|--------|-------|
| **CUSTOMER** | ผู้ซื้อ (buyer) | ดูสินค้า, ตะกร้า, สั่งซื้อ, ชำระเงิน mock, รีวิว, ดูประวัติของตัวเอง |
| **ADMIN** | ผู้ดูแลระบบ | จัดการ PRODUCT/CATEGORY (CRUD), ดู ORDER ทั้งหมด, อัปเดตสถานะ, ดู Dashboard |

---

## 📦 Collections & Fields

### CUSTOMER
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `email` | String (ข้อความ) | unique (ไม่ซ้ำ), required (จำเป็น) |
| `firstName` | String (ข้อความ) | required (จำเป็น) |
| `lastName` | String (ข้อความ) | required (จำเป็น) |
| `phone` | String (ข้อความ) | |
| `interests` | [String] (อาร์เรย์ข้อความ) | |
| `address` | String (ข้อความ) | |
| `paymentMethods` | [String] (อาร์เรย์ข้อความ) | |
| `profilePicture` | String (ข้อความ) | URL รูปโปรไฟล์ |
| `socialAccounts` | [String] (อาร์เรย์ข้อความ) | |
| `password` | String (ข้อความ) | hashed (เข้ารหัสด้วย BCrypt), required (จำเป็น) |

### ADMIN
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `email` | String (ข้อความ) | unique (ไม่ซ้ำ), required (จำเป็น) |
| `firstName` | String (ข้อความ) | required (จำเป็น) |
| `lastName` | String (ข้อความ) | required (จำเป็น) |
| `password` | String (ข้อความ) | hashed (เข้ารหัสด้วย BCrypt), required (จำเป็น) |
| `role` | String (ข้อความ) | `"admin"` |

### CART
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `customerId` | ObjectId | FK (คีย์ต่างประเทศ) → CUSTOMER, required (จำเป็น) |
| `items` | [Object] (อาร์เรย์ของ object) | embedded (ฝังอยู่ในเอกสารนี้) |
| `items.productId` | ObjectId | FK (คีย์ต่างประเทศ) → PRODUCT |
| `items.quantity` | Number (ตัวเลข) | จำนวนชิ้นในตะกร้า |

### ORDER
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `customerId` | ObjectId | FK (คีย์ต่างประเทศ) → CUSTOMER, required (จำเป็น) |
| `totalAmount` | Number (ตัวเลข) | ยอดรวม, required (จำเป็น) |
| `status` | String (ข้อความ) | `payment \| pending \| shipping \| success`, required (จำเป็น) |
| `shippingProvider` | String (ข้อความ) | บริษัทขนส่ง |
| `shippingAddress` | String (ข้อความ) | mock (จำลอง) |
| `purchaseDate` | Date (วันที่/เวลา) | วันที่สั่งซื้อ, required (จำเป็น) |

### ORDER_ITEM
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `orderId` | ObjectId | FK (คีย์ต่างประเทศ) → ORDER, required (จำเป็น) |
| `productId` | ObjectId | FK (คีย์ต่างประเทศ) → PRODUCT, required (จำเป็น) |
| `name` | String (ข้อความ) | snapshot (ภาพจำลองตอนสั่งซื้อ), required (จำเป็น) |
| `price` | Number (ตัวเลข) | snapshot (ภาพจำลองตอนสั่งซื้อ), required (จำเป็น) |
| `quantity` | Number (ตัวเลข) | จำนวนที่สั่ง, required (จำเป็น) |

### PAYMENT
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `orderId` | ObjectId | FK (คีย์ต่างประเทศ) → ORDER, required (จำเป็น) |
| `amount` | Number (ตัวเลข) | จำนวนเงิน, required (จำเป็น) |
| `method` | String (ข้อความ) | mock (จำลอง) |
| `status` | String (ข้อความ) | `unpaid \| paid \| failed` |

### REVIEW
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `customerId` | ObjectId | FK (คีย์ต่างประเทศ) → CUSTOMER, required (จำเป็น) |
| `productId` | ObjectId | FK (คีย์ต่างประเทศ) → PRODUCT, required (จำเป็น) |
| `rating` | Number (ตัวเลข) | 1-5, required (จำเป็น) |
| `comment` | String (ข้อความ) | |

### PRODUCT
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `name` | String (ข้อความ) | required (จำเป็น) |
| `description` | String (ข้อความ) | required (จำเป็น) |
| `price` | Number (ตัวเลข) | ราคา, required (จำเป็น) |
| `quantity` | Number (ตัวเลข) | สต็อก, required (จำเป็น) |
| `date` | Date (วันที่/เวลา) | |
| `tags` | [String] (อาร์เรย์ข้อความ) | สำหรับค้นหา/กรอง |
| `category` | ObjectId | FK (คีย์ต่างประเทศ) → CATEGORY |
| `artist` | String (ข้อความ) | ชื่อศิลปิน |
| `imageUrl` | String (ข้อความ) | URL รูปสินค้า |

### CATEGORY
| Field | Type | หมายเหตุ |
|-------|------|----------|
| `_id` | ObjectId | PK (คีย์หลัก = รหัสเอกสาร) |
| `name` | String (ข้อความ) | required (จำเป็น) |
| `slug` | String (ข้อความ) | ชื่อย่อสำหรับ URL |

---

## 🔗 ความสัมพันธ์ (Relationships)

| ความสัมพันธ์ | ประเภท | อ่านเป็นภาษาไทย |
|--------------|--------|-----------------|
| CUSTOMER → CART | 1 : 1 | ลูกค้า 1 คน มีตะกร้า 1 ใบ |
| CUSTOMER → ORDER | 1 : N | ลูกค้า 1 คน สั่งซื้อได้หลายครั้ง |
| CUSTOMER → REVIEW | 1 : N | ลูกค้า 1 คน รีวิวสินค้าได้หลายรายการ |
| CART → PRODUCT | M : N | ตะกร้าใส่สินค้าได้หลายชิ้น (ผ่าน items) |
| PRODUCT → CATEGORY | N : 1 | สินค้าหลายตัว อยู่ในหมวดหมู่เดียว |
| PRODUCT → REVIEW | 1 : N | สินค้า 1 ตัว มีรีวิวได้หลายรายการ |
| PRODUCT → ORDER_ITEM | 1 : N | สินค้า 1 ตัว ถูกสั่งซื้อได้หลายครั้ง |
| ORDER → ORDER_ITEM | 1 : N | ออเดอร์ 1 ใบ มีรายการสินค้าหลายบรรทัด |
| ORDER → PAYMENT | 1 : 1 | ออเดอร์ 1 ใบ มีการชำระเงิน 1 ครั้ง |
| ADMIN → PRODUCT | 1 : N (จัดการ) | แอดมินจัดการสินค้าได้หลายตัว |
| ADMIN → CATEGORY | 1 : N (จัดการ) | แอดมินจัดการหมวดหมู่ได้หลายหมวด |

> หมายเหตุ: เส้นทึบ = ความสัมพันธ์ข้อมูล (FK) · เส้นประ = การจัดการของ ADMIN (ไม่ใช่ FK)

---

## 🛡️ สิทธิ์การเข้าถึง (Access Control)

### ADMIN เข้าถึงได้
- PRODUCT, CATEGORY: CRUD เต็ม (เพิ่ม/แก้ไข/ลบ/ดู)
- ORDER: ดูทั้งหมด + อัปเดตสถานะ
- REVIEW: ดูทุกรายการ
- Dashboard: Revenue / Average Order / Inventory (aggregate จาก `ORDER.totalAmount` + `PRODUCT.quantity`)
- ไม่มี CART / ไม่ชำระเงิน

### CUSTOMER เข้าถึงได้
- ดูสินค้า + ค้นหา/กรองตาม tags (`GET /products`)
- CART ของตัวเอง: เพิ่ม/ดู/แก้/ลบ (`POST`/`GET`/`PUT`/`DELETE`)
- สั่งซื้อ (ORDER) + ชำระเงิน mock (PAYMENT)
- รีวิวสินค้าที่ซื้อ (REVIEW)
- ดูสถานะ + ประวัติคำสั่งซื้อของตัวเองเท่านั้น

---

## 📝 หมายเหตุเพิ่มเติม
- Payment และ Shipping เป็น mock (demo) ไม่เชื่อมต่อระบบจริง
- CART เก็บ `items` แบบ embedded (ฝังในเอกสาร) ไม่แยก collection
- ORDER_ITEM เก็บ name/price snapshot (ภาพจำลองตอนสั่งซื้อ) เพื่อกันข้อมูลเปลี่ยนตามสินค้า
- บทบาทแยก collection: CUSTOMER ใช้ login ปกติ, ADMIN ใช้ ADMIN collection
