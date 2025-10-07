game-shop/
│
├── index.php          ← หน้าแรก แสดงรายการรหัสเกมขาย
├── buy.php            ← หน้าซื้อรหัส + แนบสลิป
├── admin.php          ← หน้าผู้ดูแล เพิ่ม/ลบ/แก้ไขรหัส
├── db.php             ← เชื่อมฐานข้อมูล
├── upload/            ← เก็บรูปสลิป
└── sql/game_shop.sql  ← สร้างตารางในฐานข้อมูล
CREATE DATABASE game_shop CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE game_shop;

CREATE TABLE accounts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    game_name VARCHAR(100),
    username VARCHAR(100),
    password VARCHAR(100),
    price DECIMAL(10,2),
    status ENUM('available','sold') DEFAULT 'available'
);

CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    account_id INT,
    buyer_name VARCHAR(100),
    slip_image VARCHAR(255),
    status ENUM('pending','approved','rejected') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (account_id) REFERENCES accounts(id)
);
<?php
$host = "localhost";
$user = "root";
$pass = "";
$dbname = "game_shop";

$conn = new mysqli($host, $user, $pass, $dbname);
if ($conn->connect_error) {
    die("Database connection failed: " . $conn->connect_error);
}
?>
