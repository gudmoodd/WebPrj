# Car Selling E-commerce Web Application

A full-stack car selling web application built with **Node.js**, **Express.js**, **EJS**, and **MySQL**. The project provides two main modules: a customer-facing shopping website and an admin dashboard for managing products, users, orders, inventory, and sales statistics.

## Features

### Customer Module

- Browse car products by category and origin.
- Search products by keyword.
- View product details and related products.
- Register, log in, and change password.
- Add products to cart, update cart quantity, and remove cart items.
- Place orders from the shopping cart.
- View current orders, order details, and order history.
- Cancel pending orders.

### Admin Module

- Admin login with session-based access control.
- Manage car products with create, update, delete, show, and hide actions.
- Manage product categories and product origins.
- Manage customer accounts, including lock and unlock actions.
- View customer purchase history and receipt details.
- Manage invoices and update order status.
- View sales statistics by product and date range.

## Core Workflow: Cart to Order

The main business flow of this project is the **cart-to-order workflow**. It solves the problem of connecting customer purchases with inventory and order tracking.

1. A customer selects a car product and adds it to the cart.
2. If the product already exists in the cart, the system updates the quantity instead of creating a duplicate item.
3. The product stock quantity is updated in the database when cart quantity changes.
4. During checkout, cart items are converted into an invoice and invoice-detail records.
5. After the order is created, the customer can track it through current orders and order history.
6. The admin can review the invoice, view order details, and confirm or cancel the order.

This workflow makes the application more than a simple CRUD website because it includes inventory control, order creation, customer tracking, and admin order management.

## Tech Stack

- **Backend:** Node.js, Express.js
- **Frontend:** EJS, HTML, CSS, Bootstrap, JavaScript
- **Database:** MySQL
- **Template Engine:** EJS with express-ejs-layouts
- **Authentication State:** Express Session and Cookie Parser
- **File Upload:** express-fileupload

## Project Structure

```text
WebPrj-main/
├── create_database_script.txt
├── data_create.sql
├── nodejs/
│   ├── index.js
│   ├── connectDB.js
│   ├── controller/
│   │   ├── admin/
│   │   └── customer/
│   ├── model/
│   │   ├── admin/
│   │   └── customer/
│   ├── route/
│   │   ├── admin/
│   │   └── customer/
│   ├── views/
│   │   ├── admin/
│   │   └── customer/
│   ├── public/
│   └── hinh oto/
```

## Database Tables

The MySQL database includes tables for:

- `sanpham` - product information
- `loaisanpham` - product categories
- `xuatxu` - product origins
- `giohang` - shopping cart items
- `hoadon` - invoices/orders
- `cthoadon` - invoice details
- `taikhoan_kh` - customer accounts
- `taikhoan_admin` - admin accounts
- `trangthai` - order statuses
- `lichsusanpham` - product history

## Installation and Setup

### 1. Clone or download the project

```bash
git clone <repository-url>
cd WebPrj-main/nodejs
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create and import the MySQL database

Import the SQL file into MySQL:

```bash
mysql -u root -p < ../data_create.sql
```

The default database name is:

```text
car_selling_nodejs
```

### 4. Configure database connection

Update the MySQL credentials in `nodejs/connectDB.js` if needed:

```js
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '12345',
  database: 'car_selling_nodejs',
  multipleStatements: true
});
```

### 5. Run the application

```bash
npm start
```

The application will run at:

```text
http://localhost:3000/customer/home
```

Admin page:

```text
http://localhost:3000/admin/login
```

## Main Routes

### Customer Routes

- `/customer/home` - Customer home page
- `/customer/login` - Customer login
- `/customer/signup` - Customer registration
- `/customer/san-pham/loai-san-pham/:idLsp` - Products by category
- `/customer/san-pham/xuat-xu/:idXx` - Products by origin
- `/customer/san-pham/chi-tiet/:idLsp/:idSP` - Product detail
- `/customer/cart` - Shopping cart
- `/customer/don-hang` - Current orders
- `/customer/don-hang/lich-su` - Order history

### Admin Routes

- `/admin/login` - Admin login
- `/admin/` - Admin dashboard
- `/admin/san-pham` - Product management
- `/admin/loai-san-pham` - Category management
- `/admin/xuat-xu-san-pham` - Origin management
- `/admin/user` - Customer account management
- `/admin/hoa-don` - Invoice/order management
- `/admin/thong-ke` - Sales statistics

## What I Learned

- Building a full-stack web application with Express.js and EJS.
- Structuring a project using routes, controllers, models, and views.
- Designing a MySQL database for products, carts, invoices, and users.
- Implementing a real e-commerce flow from product browsing to checkout.
- Handling inventory updates during cart and order operations.
- Creating admin-side management features and sales reports with SQL aggregation.

## Notes

This project was developed for learning and academic purposes. For production use, several improvements should be added, such as password hashing, input validation, role-based authorization, transaction handling for checkout, and better error handling.
