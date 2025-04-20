### 1. 完成mysql数据库、界面客户端的安装

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420191122863.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420191221303.png)

### 2. 使用命令提示符窗口进行新建表、熟悉表数据的增删改查操作

```
CREATE DATABASE myfirst_database #创建一个数据库

SHOW DATABASES; #可以看到有哪些数据库
```

增：

```
USE `myfirst_database`;
CREATE TABLE `student`(
	`student_id` INT PRIMARY key,
    `name` VARCHAR(20),
    `major` VARCHAR(20)
);
DESCRIBE `student`;描述表格

ALTER TABLE `student` ADD gpa DECIMAL(3,2); #增加
INSERT INTO `student`(`name`,`student_id`,`major`,'gpa') VALUES(‘杨林’,8，‘金融科技’，5);
```

删：

```
ALTER TABLE `student`  DROP COLUMN gpa; #删除gpa

DELETE FROM `student`
WHERE `student_id` = 5;
```

改：

```
UPDATE `student`
SET `major` = '金融科技学科'
WHERE `student_id` = 5;
```

查：

```
SELECT * 
FROM `student`
ORDER BY `score`,'student_id';
```

### 3. 使用两种方式分别来完成sql脚本（employee.sql、studen.sql）的导入；

直接用记事本方式打开然后全选执行。

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420205058516.png)

第二种，直接run:

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420205218875.png)

### 4. 新建表：country表，并插入数据：

```
CREATE TABLE `country`(
	`cid` INT AUTO_INCREMENT,
    `country` VARCHAR(16),
    `population` VARCHAR(20),
    PRIMARY KEY(`cid`)
);

INSERT INTO `country` (`country`, `population`) VALUES
('中国', '1400'),
('美国', '320'),
('印度', '1300'),
('印度尼西亚', '250'),
('巴西', '210'),
('巴基斯坦', '200'),
('俄罗斯', '150'),
('日本', '130'),
('德国', '85'),
('英国', '66'),
('法国', '65'),
('阿根廷', '45'),
('加拿大', '35'),
('南非', '60'),
('埃及', '100'),
('澳大利亚', '25'),
('新西兰', '5'),
('韩国', '50');
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420203027735.png)

### 5. 完成employee表、student表、country表的导出（含表结构、数据）

打开cmd，执行:

```
mysqldump -u root -p test student > C:\Users\thinkpad\Desktop\student.sql
```

```
mysqldump -u root -p employee employees > C:\Users\thinkpad\Desktop\employees.sql
```

```
mysqldump -u root -p myfirst_database country > C:\Users\thinkpad\Desktop\country.sql
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420210710519.png)

### 6. 新建数据库：employees

```
CREATE DATABASE employees;
```

### 7. 使用python程序连接mysql数据库，在控制台打印输出country的全部数据

```
import pymysql

# 数据库连接配置（根据实际情况修改）
config = {
    "host": "localhost",
    "user": "root",
    "password": "admin123",        # 若未设置密码，留空
    "database": "myfirst_database"   # 替换为实际的数据库名（如employees或原数据库）
}

# 连接数据库
connection = pymysql.connect(**config)
cursor = connection.cursor()

# 执行SQL查询
cursor.execute("SELECT * FROM country")
rows = cursor.fetchall()

# 获取列名（表头）
columns = [desc[0] for desc in cursor.description]
print("列名：", columns)

# 打印数据
print("数据：")
for row in rows:
    print(row)

# 关闭连接
cursor.close()
connection.close()
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420214135748.png)

### 8. 尝试导出当前数据库的全部数据（含表结构）

```
mysqldump -u root -p employee > C:\Users\thinkpad\Desktop\full.sql
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250420214822234.png)
