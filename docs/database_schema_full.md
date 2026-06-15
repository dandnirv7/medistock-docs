# Database Schema - Full Version

## Overview

Versi full untuk aplikasi inventory apotek yang lebih siap berkembang menjadi sistem operasional.

Mencakup:

- Batch management
- Purchase Order
- Sales
- Stock Opname
- Audit Trail
- Notifications
- Settings
- Reporting

---

# Core Tables

## users

Sama seperti MVP.

---

## categories

Sama seperti MVP.

---

## suppliers

Sama seperti MVP.

---

## medicines

Master data obat.

Field tambahan:

| Field                 | Type         |
| --------------------- | ------------ |
| barcode               | varchar(100) |
| manufacturer          | varchar(150) |
| image_url             | text         |
| requires_prescription | boolean      |

---

# Batch Management

## medicine_batches

Setiap batch memiliki expired sendiri.

| Field              | Type         |
| ------------------ | ------------ |
| id                 | uuid         |
| medicine_id        | uuid FK      |
| batch_number       | varchar(100) |
| purchase_price     | decimal      |
| selling_price      | decimal      |
| quantity_received  | integer      |
| quantity_remaining | integer      |
| manufacture_date   | date         |
| expired_date       | date         |
| supplier_id        | uuid FK      |
| created_at         | timestamp    |
| updated_at         | timestamp    |

### Benefit

Mendukung:

- FEFO
- Multiple expired date
- Multiple harga beli

---

# Purchase Module

## purchase_orders

Header pembelian.

| Field         | Type         |
| ------------- | ------------ |
| id            | uuid         |
| po_number     | varchar(100) |
| supplier_id   | uuid FK      |
| order_date    | date         |
| expected_date | date         |
| status        | enum         |
| total_amount  | decimal      |
| notes         | text         |

Status:

```txt
DRAFT
ORDERED
RECEIVED
CANCELLED
```

---

## purchase_order_items

Detail pembelian.

| Field             | Type    |
| ----------------- | ------- |
| id                | uuid    |
| purchase_order_id | uuid FK |
| medicine_id       | uuid FK |
| quantity          | integer |
| purchase_price    | decimal |
| subtotal          | decimal |

---

# Sales Module

## sales

Header transaksi penjualan.

| Field            | Type      |
| ---------------- | --------- |
| id               | uuid      |
| invoice_number   | varchar   |
| transaction_date | timestamp |
| cashier_id       | uuid FK   |
| customer_name    | varchar   |
| total_amount     | decimal   |
| payment_method   | varchar   |
| notes            | text      |

---

## sale_items

Detail penjualan.

| Field       | Type    |
| ----------- | ------- |
| id          | uuid    |
| sale_id     | uuid FK |
| medicine_id | uuid FK |
| batch_id    | uuid FK |
| quantity    | integer |
| unit_price  | decimal |
| subtotal    | decimal |

---

# Inventory Module

## stock_movements

Sama seperti MVP.

Tambahan:

| Field          | Type    |
| -------------- | ------- |
| batch_id       | uuid FK |
| reference_type | varchar |
| reference_id   | uuid    |

Reference Type:

```txt
PURCHASE
SALE
ADJUSTMENT
OPNAME
RETURN
EXPIRED
```

---

## stock_opnames

Header stok opname.

| Field         | Type    |
| ------------- | ------- |
| id            | uuid    |
| opname_number | varchar |
| opname_date   | date    |
| user_id       | uuid FK |
| notes         | text    |

---

## stock_opname_items

Detail opname.

| Field           | Type    |
| --------------- | ------- |
| id              | uuid    |
| stock_opname_id | uuid FK |
| medicine_id     | uuid FK |
| system_stock    | integer |
| physical_stock  | integer |
| difference      | integer |

---

# Audit Module

## audit_logs

Mencatat seluruh aktivitas.

| Field       | Type      |
| ----------- | --------- |
| id          | uuid      |
| user_id     | uuid FK   |
| module      | varchar   |
| action      | varchar   |
| entity_type | varchar   |
| entity_id   | uuid      |
| old_values  | jsonb     |
| new_values  | jsonb     |
| ip_address  | varchar   |
| created_at  | timestamp |

Contoh:

```txt
CREATE_MEDICINE
UPDATE_MEDICINE
DELETE_MEDICINE
LOGIN
LOGOUT
```

---

# Notification Module

## notifications

| Field      | Type      |
| ---------- | --------- |
| id         | uuid      |
| title      | varchar   |
| message    | text      |
| type       | varchar   |
| is_read    | boolean   |
| user_id    | uuid FK   |
| created_at | timestamp |

Type:

```txt
LOW_STOCK
EXPIRED
SYSTEM
PURCHASE
```

---

# Settings Module

## settings

Global application settings.

| Field       | Type    |
| ----------- | ------- |
| id          | uuid    |
| key         | varchar |
| value       | text    |
| description | text    |

Examples:

```txt
LOW_STOCK_THRESHOLD
EXPIRY_ALERT_DAYS
COMPANY_NAME
COMPANY_ADDRESS
```

---

# Reporting Module

## reports

Menyimpan generated report.

| Field        | Type      |
| ------------ | --------- |
| id           | uuid      |
| report_type  | varchar   |
| file_url     | text      |
| generated_by | uuid FK   |
| generated_at | timestamp |

Examples:

```txt
STOCK_REPORT
SALES_REPORT
PURCHASE_REPORT
EXPIRY_REPORT
```

---

# Full ERD Summary

users
├── sales
├── stock_movements
├── stock_opnames
├── audit_logs
└── notifications

categories
└── medicines

suppliers
├── medicines
├── purchase_orders
└── medicine_batches

medicines
├── medicine_batches
├── sale_items
├── purchase_order_items
├── stock_movements
└── stock_opname_items

purchase_orders
└── purchase_order_items

sales
└── sale_items

stock_opnames
└── stock_opname_items

medicine_batches
├── sale_items
└── stock_movements

---

# Recommended Adoption

## Phase 1 (MVP)

Implement:

- users
- categories
- suppliers
- medicines
- stock_movements

## Phase 2

Add:

- medicine_batches
- purchase_orders
- purchase_order_items

## Phase 3

Add:

- sales
- sale_items

## Phase 4

Add:

- stock_opnames
- audit_logs
- notifications
- settings
- reports

Pendekatan ini menjaga MVP tetap kecil tetapi memungkinkan migrasi ke sistem apotek yang jauh lebih lengkap tanpa redesign database besar-besaran.
