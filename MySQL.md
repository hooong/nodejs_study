# MySQL

- 연동을 위한 설치모듈
  - Nom install --save mysql;

```javascript
var mysql = require('mysql');

var con = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : 'password',
  port : '3306',
  database : 'db_name'
});
con.connect();    //연결
con.end();		  //연결 끊기
```

- query문 사용하기

```javascript
//SELECT
var sql = 'SELECT * FROM topic';
con.query(sql, function(err, rows, columns){
  if(err){
    console.log(err);
  } else {
    for(var i=0; i<rows.length; i++){
      console.log(rows[i].title);
    }
  }
})

//INSERT
var sql = 'INSERT INTO topic (title, description, author) VALUES(?, ?, ?)';
var params = ['Supervisor', 'Watcher', 'hong'];
con.query(sql, params, function(err, rows, fields){
  if(err){
    console.log(err);
  } else {
    console.log(rows.insertId);
  }
})

//UPDATE
var sql = 'UPDATE topic SET title=?, author=? WHERE id=?';
var params = ['NPM', 'hong', '1'];
con.query(sql, params, function(err, rows, fields){
  if(err){
    console.log(err);
  } else {
    console.log(rows);
  }
})

//DELETE
var sql = 'DELETE FROM topic WHERE id=?';
var params = [2];
con.query(sql, params, function(err, rows, fields){
  if(err){
    console.log(err);
  } else {
    console.log(rows);
  }
})
```

- 경험함 Error

  - Error: Connection lost: The server closed the connection. 

  - => mysql.createConnection에 port : '3306'를 추가해준다.

  - 

  - Error: ER_HOST_NOT_PRIVILEGED: Host '127.0.0.1' is not allowed to connect to this MySQL server 

  - => ./mysql -uroot -p

  - ```mysql
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
    CREATE USER 'root'@'%' IDENTIFIED BY 'password';	//password를 설정해줌.
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
    ```