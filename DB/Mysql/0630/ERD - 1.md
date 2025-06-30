# DML 

```MYSQL

-- MEMBER
INSERT INTO MEMBER (member_id, email, password, name, phone_number, is_admin)
VALUES
('mem001', 'alice@example.com', 'pass1', 'Alice', '010-1111-1111', 'N'),
('mem002', 'bob@example.com', 'pass2', 'Bob', '010-2222-2222', 'N'),
('mem003', 'carol@example.com', 'pass3', 'Carol', '010-3333-3333', 'Y'),
('mem004', 'dave@example.com', 'pass4', 'Dave', '010-4444-4444', 'N'),
('mem005', 'eve@example.com', 'pass5', 'Eve', '010-5555-5555', 'N'),
('mem006', 'frank@example.com', 'pass6', 'Frank', '010-6666-6666', 'N'),
('mem007', 'grace@example.com', 'pass7', 'Grace', '010-7777-7777', 'N'),
('mem008', 'heidi@example.com', 'pass8', 'Heidi', '010-8888-8888', 'N'),
('mem009', 'ivan@example.com', 'pass9', 'Ivan', '010-9999-9999', 'N'),
('mem010', 'judy@example.com', 'pass10', 'Judy', '010-0000-0000', 'N');

-- CATEGORY
INSERT INTO CATEGORY (category_id, category_name, parent_id)
VALUES
('cat001', 'Software', NULL),
('cat002', 'Games', NULL),
('cat003', 'Office', 'cat001'),
('cat004', 'Security', 'cat001'),
('cat005', 'Action', 'cat002'),
('cat006', 'Puzzle', 'cat002'),
('cat007', 'Utilities', NULL),
('cat008', 'Audio', 'cat007'),
('cat009', 'Video', 'cat007'),
('cat010', 'Backup', 'cat007');

-- PRODUCT
INSERT INTO PRODUCT (product_id, category_id, name, content, price, end_day, version, first_product, last_edit_date)
VALUES
('prd001', 'cat003', 'OfficeSuite', 'Word processor', 50000, 365, 'v1.0', NOW(), NOW()),
('prd002', 'cat004', 'Antivirus', 'Security software', 30000, 365, 'v2.1', NOW(), NOW()),
('prd003', 'cat005', 'ShooterX', 'Action shooter game', 45000, 0, 'v3.2', NOW(), NOW()),
('prd004', 'cat006', 'PuzzleMaster', 'Brain puzzle game', 20000, 0, 'v1.3', NOW(), NOW()),
('prd005', 'cat008', 'AudioEditor', 'Audio editing', 60000, 365, 'v5.0', NOW(), NOW()),
('prd006', 'cat009', 'VideoConverter', 'Convert videos', 35000, 365, 'v4.2', NOW(), NOW()),
('prd007', 'cat010', 'BackupPro', 'Data backup tool', 40000, 365, 'v2.5', NOW(), NOW()),
('prd008', 'cat003', 'Spreadsheet', 'Excel alternative', 55000, 365, 'v1.1', NOW(), NOW()),
('prd009', 'cat004', 'FirewallPlus', 'Advanced firewall', 25000, 365, 'v1.0', NOW(), NOW()),
('prd010', 'cat005', 'RacingPro', 'Racing game', 48000, 0, 'v1.8', NOW(), NOW());

-- PRODUCT_IMAGE
INSERT INTO PRODUCT_IMAGE (image, product_id)
VALUES
('office1.jpg', 'prd001'), ('office2.jpg', 'prd001'),
('antivirus1.jpg', 'prd002'), ('shooterx1.jpg', 'prd003'),
('puzzle1.jpg', 'prd004'), ('audio1.jpg', 'prd005'),
('video1.jpg', 'prd006'), ('backup1.jpg', 'prd007'),
('spreadsheet1.jpg', 'prd008'), ('firewall1.jpg', 'prd009');

-- LICENSE
INSERT INTO LICENSE (product_id, member_id, expire_date)
VALUES
('prd001', 'mem001', NOW() + INTERVAL 365 DAY),
('prd002', 'mem002', NOW() + INTERVAL 365 DAY),
('prd003', 'mem003', NOW() + INTERVAL 365 DAY),
('prd004', 'mem004', NOW() + INTERVAL 365 DAY),
('prd005', 'mem005', NOW() + INTERVAL 365 DAY),
('prd006', 'mem006', NOW() + INTERVAL 365 DAY),
('prd007', 'mem007', NOW() + INTERVAL 365 DAY),
('prd008', 'mem008', NOW() + INTERVAL 365 DAY),
('prd009', 'mem009', NOW() + INTERVAL 365 DAY),
('prd010', 'mem010', NOW() + INTERVAL 365 DAY);

-- COUPON
INSERT INTO COUPON (coupon_id, issued_id, discount_price, end_day, last_edit_date)
VALUES
('cp001', 'mem001', 5000, 30, NOW()), ('cp002', 'mem002', 10000, 30, NOW()),
('cp003', 'mem003', 7000, 30, NOW()), ('cp004', 'mem004', 8000, 30, NOW()),
('cp005', 'mem005', 9000, 30, NOW()), ('cp006', 'mem006', 6000, 30, NOW()),
('cp007', 'mem007', 7500, 30, NOW()), ('cp008', 'mem008', 9500, 30, NOW()),
('cp009', 'mem009', 8500, 30, NOW()), ('cp010', 'mem010', 5000, 30, NOW());

-- MEMBER_COUPON
INSERT INTO MEMBER_COUPON (member_coupon_id, member_id, coupon_id, use_date, issued_date)
VALUES
('mc001', 'mem001', 'cp001', NULL, NOW()), ('mc002', 'mem002', 'cp002', NULL, NOW()),
('mc003', 'mem003', 'cp003', NULL, NOW()), ('mc004', 'mem004', 'cp004', NULL, NOW()),
('mc005', 'mem005', 'cp005', NULL, NOW()), ('mc006', 'mem006', 'cp006', NULL, NOW()),
('mc007', 'mem007', 'cp007', NULL, NOW()), ('mc008', 'mem008', 'cp008', NULL, NOW()),
('mc009', 'mem009', 'cp009', NULL, NOW()), ('mc010', 'mem010', 'cp010', NULL, NOW());

-- ORDERS
INSERT INTO ORDERS (order_id, member_id, member_coupon_id, order_date, last_order_price)
VALUES
('ord001', 'mem001', 'mc001', NOW(), 45000), ('ord002', 'mem002', 'mc002', NOW(), 70000),
('ord003', 'mem003', 'mc003', NOW(), 60000), ('ord004', 'mem004', 'mc004', NOW(), 35000),
('ord005', 'mem005', 'mc005', NOW(), 80000), ('ord006', 'mem006', 'mc006', NOW(), 30000),
('ord007', 'mem007', 'mc007', NOW(), 40000), ('ord008', 'mem008', 'mc008', NOW(), 55000),
('ord009', 'mem009', 'mc009', NOW(), 25000), ('ord010', 'mem010', 'mc010', NOW(), 65000);

-- ORDER_DETAIL
INSERT INTO ORDER_DETAIL (order_id, product_id, price)
VALUES
('ord001', 'prd001', 50000), ('ord002', 'prd002', 30000), ('ord003', 'prd003', 45000),
('ord004', 'prd004', 20000), ('ord005', 'prd005', 60000), ('ord006', 'prd006', 35000),
('ord007', 'prd007', 40000), ('ord008', 'prd008', 55000), ('ord009', 'prd009', 25000),
('ord010', 'prd010', 48000);

-- CART
INSERT INTO CART (member_id, product_id, cart_add_date)
VALUES
('mem001', 'prd003', NOW()), ('mem002', 'prd004', NOW()), ('mem003', 'prd005', NOW()),
('mem004', 'prd006', NOW()), ('mem005', 'prd007', NOW()), ('mem006', 'prd008', NOW()),
('mem007', 'prd009', NOW()), ('mem008', 'prd010', NOW()), ('mem009', 'prd001', NOW()),
('mem010', 'prd002', NOW());

-- WISHLIST
INSERT INTO WISHLIST (product_id, member_id, wishlist_add_date)
VALUES
('prd001', 'mem001', NOW()), ('prd002', 'mem002', NOW()), ('prd003', 'mem003', NOW()),
('prd004', 'mem004', NOW()), ('prd005', 'mem005', NOW()), ('prd006', 'mem006', NOW()),
('prd007', 'mem007', NOW()), ('prd008', 'mem008', NOW()), ('prd009', 'mem009', NOW()),
('prd010', 'mem010', NOW());

-- POINT
INSERT INTO POINT (member_id, last_point, expire_at)
VALUES
('mem001', 1000, NOW() + INTERVAL 365 DAY), ('mem002', 2000, NOW() + INTERVAL 365 DAY),
('mem003', 3000, NOW() + INTERVAL 365 DAY), ('mem004', 4000, NOW() + INTERVAL 365 DAY),
('mem005', 5000, NOW() + INTERVAL 365 DAY), ('mem006', 6000, NOW() + INTERVAL 365 DAY),
('mem007', 7000, NOW() + INTERVAL 365 DAY), ('mem008', 8000, NOW() + INTERVAL 365 DAY),
('mem009', 9000, NOW() + INTERVAL 365 DAY), ('mem010', 10000, NOW() + INTERVAL 365 DAY);

-- POINT_HISTORY
INSERT INTO POINT_HISTORY (created_at, member_id, point, plus_minus, description)
VALUES
(NOW(), 'mem001', 1000, '+', 'Signup bonus'), (NOW(), 'mem002', 1500, '+', 'First order'),
(NOW(), 'mem003', 2000, '+', 'Event reward'), (NOW(), 'mem004', 500, '-', 'Used for purchase'),
(NOW(), 'mem005', 3000, '+', 'Promotion bonus'), (NOW(), 'mem006', 700, '-', 'Purchase'),
(NOW(), 'mem007', 1000, '+', 'Referral'), (NOW(), 'mem008', 1200, '+', 'Feedback'),
(NOW(), 'mem009', 800, '-', 'Purchase'), (NOW(), 'mem010', 2500, '+', 'Promotion');

-- REVIEW
INSERT INTO REVIEW (product_id, member_id, content, rate, last_edit_date, first_review)
VALUES
('prd001', 'mem001', 'Great product!', 5, NOW(), NOW()), ('prd002', 'mem002', 'Satisfied', 4, NOW(), NOW()),
('prd003', 'mem003', 'Exciting game', 5, NOW(), NOW()), ('prd004', 'mem004', 'Challenging puzzles', 4, NOW(), NOW()),
('prd005', 'mem005', 'Professional tool', 5, NOW(), NOW()), ('prd006', 'mem006', 'Very useful', 4, NOW(), NOW()),
('prd007', 'mem007', 'Essential', 5, NOW(), NOW()), ('prd008', 'mem008', 'Good alternative', 4, NOW(), NOW()),
('prd009', 'mem009', 'Secure solution', 5, NOW(), NOW()), ('prd010', 'mem010', 'Fun racing', 5, NOW(), NOW());

-- QUESTION
INSERT INTO QUESTION (qna_id, member_id, title, content, first_question, last_edit_date)
VALUES
('qna001', 'mem001', 'How to install?', 'Steps to install product', NOW(), NOW()),
('qna002', 'mem002', 'License issue', 'License not working', NOW(), NOW()),
('qna003', 'mem003', 'Compatibility?', 'Works on Mac?', NOW(), NOW()),
('qna004', 'mem004', 'Refund?', 'How to get a refund?', NOW(), NOW()),
('qna005', 'mem005', 'Update?', 'Is update free?', NOW(), NOW()),
('qna006', 'mem006', 'Discount?', 'Available discounts?', NOW(), NOW()),
('qna007', 'mem007', 'Features?', 'What features included?', NOW(), NOW()),
('qna008', 'mem008', 'Trial?', 'Is there a free trial?', NOW(), NOW()),
('qna009', 'mem009', 'Account?', 'Change email?', NOW(), NOW()),
('qna010', 'mem010', 'Support?', 'How to contact support?', NOW(), NOW());

-- ANSWER
INSERT INTO ANSWER (qna_id, answer_member_id, status, answer_content, stauts_date, first_answer, last_edit_date)
VALUES
('qna001', 'mem003', 'Y', 'Please follow installer steps.', NOW(), NOW(), NOW()),
('qna002', 'mem004', 'Y', 'License reissued.', NOW(), NOW(), NOW()),
('qna003', 'mem005', 'Y', 'Yes, it works on Mac.', NOW(), NOW(), NOW()),
('qna004', 'mem006', 'Y', 'Refund processed.', NOW(), NOW(), NOW()),
('qna005', 'mem007', 'Y', 'Updates are free.', NOW(), NOW(), NOW()),
('qna006', 'mem008', 'Y', 'Discounts applied.', NOW(), NOW(), NOW()),
('qna007', 'mem009', 'Y', 'Features listed on site.', NOW(), NOW(), NOW()),
('qna008', 'mem010', 'Y', 'Free trial available.', NOW(), NOW(), NOW()),
('qna009', 'mem001', 'Y', 'Email changed.', NOW(), NOW(), NOW()),
('qna010', 'mem002', 'Y', 'Contact via email.', NOW(), NOW(), NOW());
```


---

# DDL

```MYSQL

USE SHOP;
DROP TABLE IF EXISTS MEMBER_COUPON, COUPON, POINT, POINT_HISTORY, ANSWER, QUESTION, ORDER_DETAIL, ORDERS, REVIEW, LICENSE, CATEGORY, PRODUCT_IMAGE, PRODUCT, CART, WISHLIST, MEMBER;

CREATE TABLE MEMBER (
    member_id VARCHAR(20) PRIMARY KEY,
    email VARCHAR(40) NOT NULL,
    password VARCHAR(100) NOT NULL,
    name VARCHAR(20) NOT NULL,
    phone_number VARCHAR(20) NOT NULL,
    is_admin VARCHAR(1) NOT NULL,
    register_date DATETIME NOT NULL
);

CREATE TABLE CATEGORY (
    category_id VARCHAR(20) PRIMARY KEY,
    category_name VARCHAR(20) NOT NULL,
    parent_id VARCHAR(20),
    FOREIGN KEY (parent_id) REFERENCES CATEGORY(category_id)
);

CREATE TABLE PRODUCT (
    product_id VARCHAR(20) PRIMARY KEY,
    category_id VARCHAR(20) NOT NULL,
    name VARCHAR(20) NOT NULL,
    content TEXT NOT NULL,
    price INT NOT NULL,
    end_day INT NOT NULL,
    version VARCHAR(10) NOT NULL,
    first_product DATETIME NOT NULL,
    last_edit_date DATETIME NOT NULL,
    FOREIGN KEY (category_id) REFERENCES CATEGORY(category_id)
);

CREATE TABLE PRODUCT_IMAGE (
    image VARCHAR(20) NOT NULL,
    product_id VARCHAR(20) NOT NULL,
    PRIMARY KEY (image, product_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

CREATE TABLE LICENSE (
    product_id VARCHAR(20) NOT NULL,
    member_id VARCHAR(20) NOT NULL,
    expire_date DATETIME NOT NULL,
    PRIMARY KEY (product_id, member_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id),
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE COUPON (
    coupon_id VARCHAR(20) PRIMARY KEY,
    issued_id VARCHAR(20) NOT NULL,
    discount_price INT NOT NULL,
    end_day INT NOT NULL,
    last_edit_date DATETIME NOT NULL,
   FOREIGN KEY (issued_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE MEMBER_COUPON (
    member_coupon_id VARCHAR(20) PRIMARY KEY,
    member_id VARCHAR(20) NOT NULL,
    coupon_id VARCHAR(20) NOT NULL,
    use_date DATETIME,
    issued_date DATETIME NOT NULL,
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id),
    FOREIGN KEY (coupon_id) REFERENCES COUPON(coupon_id)
);

CREATE TABLE ORDERS (
    order_id VARCHAR(20) PRIMARY KEY,
    member_id VARCHAR(20) NOT NULL,
    member_coupon_id VARCHAR(20) NOT NULL,
    order_date DATETIME NOT NULL,
    last_order_price INT NOT NULL,
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id),
    FOREIGN KEY (member_coupon_id) REFERENCES MEMBER_COUPON(member_coupon_id)
);

CREATE TABLE ORDER_DETAIL (
    order_id VARCHAR(20) NOT NULL,
    product_id VARCHAR(20) NOT NULL,
    price INT NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES ORDERS(order_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

CREATE TABLE CART (
    member_id VARCHAR(20) NOT NULL,
    product_id VARCHAR(20) NOT NULL,
    cart_add_date DATETIME NOT NULL,
    PRIMARY KEY (member_id, product_id),
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

CREATE TABLE WISHLIST (
    product_id VARCHAR(20) NOT NULL,
    member_id VARCHAR(20) NOT NULL,
    wishlist_add_date DATETIME NOT NULL,
    PRIMARY KEY (product_id, member_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id),
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE POINT (
    member_id VARCHAR(20) PRIMARY KEY,
    last_point INT NOT NULL,
    expire_at DATETIME NOT NULL,
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE POINT_HISTORY (
    created_at DATETIME NOT NULL,
    member_id VARCHAR(20) NOT NULL,
    point INT NOT NULL,
    plus_minus VARCHAR(1) NOT NULL CHECK (plus_minus IN ('+', '-')),
    description TEXT NOT NULL,
    PRIMARY KEY (created_at, member_id),
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE REVIEW (
    product_id VARCHAR(20) NOT NULL,
    member_id VARCHAR(20) NOT NULL,
    content TEXT,
    rate INT NOT NULL,
    last_edit_date DATETIME NOT NULL,
    first_review DATETIME NOT NULL,
    PRIMARY KEY (product_id, member_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id),
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE QUESTION (
    qna_id VARCHAR(20) PRIMARY KEY,
    member_id VARCHAR(20) NOT NULL,
    title VARCHAR(300) NOT NULL,
    content TEXT NOT NULL,
    first_question DATETIME NOT NULL,
    last_edit_date DATETIME NOT NULL,
    FOREIGN KEY (member_id) REFERENCES MEMBER(member_id)
);

CREATE TABLE ANSWER (
    qna_id VARCHAR(20) PRIMARY KEY,
    answer_member_id VARCHAR(20) NOT NULL,
    status VARCHAR(1) NOT NULL,
    answer_content TEXT,
    stauts_date DATETIME,
    first_answer DATETIME NOT NULL,
    last_edit_date DATETIME NOT NULL,
    FOREIGN KEY (qna_id) REFERENCES QUESTION(qna_id),
    FOREIGN KEY (answer_member_id) REFERENCES MEMBER(member_id)
);

ALTER TABLE MEMBER MODIFY register_date DATETIME DEFAULT NOW();
ALTER TABLE QUESTION MODIFY last_edit_date DATETIME DEFAULT NOW();
ALTER TABLE QUESTION MODIFY first_question DATETIME DEFAULT NOW();
ALTER TABLE COUPON MODIFY last_edit_date DATETIME DEFAULT NOW();
ALTER TABLE MEMBER_COUPON ADD CONSTRAINT UNIQUE(member_id, coupon_id);
ALTER TABLE MEMBER_COUPON MODIFY issued_date DATETIME DEFAULT NOW();
ALTER TABLE POINT_HISTORY MODIFY created_at DATETIME DEFAULT NOW();
ALTER TABLE ANSWER MODIFY first_answer DATETIME DEFAULT NOW();
ALTER TABLE ANSWER MODIFY last_edit_date DATETIME DEFAULT NOW();
ALTER TABLE CART MODIFY cart_add_date DATETIME DEFAULT NOW();
ALTER TABLE WISHLIST MODIFY wishlist_add_date DATETIME DEFAULT NOW();
ALTER TABLE PRODUCT MODIFY first_product DATETIME DEFAULT NOW();
ALTER TABLE PRODUCT MODIFY last_edit_date DATETIME DEFAULT NOW();
ALTER TABLE REVIEW MODIFY first_review DATETIME DEFAULT NOW();
ALTER TABLE REVIEW MODIFY last_edit_date DATETIME DEFAULT NOW();



```

