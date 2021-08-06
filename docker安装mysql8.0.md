## docker pull mysql

#### docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=zsh123 --restart=always  -d mysql

#### 或者run的时候忘记加参数 docker update --restart=always mysql

#### mysql -uroot -p

#### use mysql

#### select * from user \G

#### ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

#### FLUSH PRIVILEGES;



