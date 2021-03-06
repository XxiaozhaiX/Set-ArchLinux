## 1.安裝MySQL:
```java
sudo pacman -S mysql --noconfirm
```
初始化MySQL:
```java
sudo mysqld --initialize --user=mysql
```

然後會出現默認密碼(比如)：
```java
2021-11-25T13:52:01.788772Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: (uznCYhYI10h
                                                                                                               『   這一段    』
```

給權限：
```java
chown -R mysql:mysql /var/lib/mysql
```
啟動並登入：
```java
sudo systemctl start mysqld
mysql -u root -p
```
然後輸入密碼

修改密碼：
```java
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '新密碼';
```

查看mysqld的默認配置
```java
mysqld --verbose --help
```
默認配置文件:/etc/mysql/my.cnf
默認數據庫文件:/var/lib/mysql/

## 2.解決錯誤：

缺少icu63: mysqld: error while loading shared libraries: libicuuc.so.63: cannot open shared object file: No such file or directory
(確保arch安裝了yay)
```java
1.yay -S icu63 --noconfirm
```

資料夾被佔用：mysql: Cant create directory '/var/lib/mysql/' (OS errno 17 - File exists)
```java
1.sudo rm -rf /var/lib/mysql
```

报错：ERROR 1045 (28000): Access denied for user 'root'@'localhost' 解决方法
```java
1.在/etc/mysql/my.cnf中[mysqld] 添加：skip-grant-tables
2.重起MySQL
```

解决MySQL修改密码：ERROR 1290 (HY000): The MySQL server is running with the --skip-grant-tables option
```java
1.找不到初始密码可以在/etc/mysql/my.cnf中[mysqld] 添加：skip-grant-tables
2.先执行：flush privileges;
3.再修改密碼
```
