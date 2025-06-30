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