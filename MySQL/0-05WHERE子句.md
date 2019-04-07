# 过滤数据

## 使用WHERE子句

- 只检索所需数据需指定搜索条件，搜索条件也称过滤条件
- `SELECT prod_name, prod_price FROM products WHERE prod_price = 2.50;`

## WHERE子句操作符

- =, <>, !=, <, <=, >, >=, BETWEEN。

## 检查单个值

- `SELECT prod_name, prod_price FROM products WHERE prod_name = 'fuses';`
- 不匹配检查：`SELECT vend_id, prod_name FROM products WHERE vend_id <> 1003;`
  - `SELECT vend_id, prod_name FROM products WHERE vend_id != 1003;`
- `SELECT prod_name, prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;`
- 空值检查：`SELECT prod_name FROM products WHERE prod_price IS NULL`
  - `SELECT cust_id FROM customers WHERE cust_email IS NULL;`