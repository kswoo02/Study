use shopdb;
show tables;

create table tb_order(
	id int auto_increment primary key,
    order_date date,
    order_datetime datetime
);

desc tb_order;
insert into tb_order values(0,curdate(),curtime());

select * from tb_order;

-- ★
-- data를 string으로 변환 ★
select date_format(order_date, '%m일/%d월/%y년') from tb_order;

-- order_date에는 '2024-09-12' 입력되게 insert문을 구현하시오
-- string을 date 타입으로 변환 ★
insert into tb_order values(0, str_to_date('09-12-2024','%m-%d-%Y'), curtime());
select from tb_order; 
