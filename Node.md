# Node.js

- JavaScript언어를 사용하여 서버 사이드 개발에 사용되는 소프트웨어 플랫폼



- npm(Node Package Manager)
  - 모듈 관리자라 할 수 있으며 남이 만들어 놓은 모듈들도 가져다 쓸 수 있다.
  - Rails에 비교하면 gem과 비슷하다.
  - node계의 앱스토어라 할 수 있다. 
    - uglify-js : 코드용량을 줄여주는 모듈	
      - 사용법 : uglifyjs [파일명] -m, uglifyjs [파일명] -o [생성파일명] -m

**Pug**

- Template engine으로 파일명을 예로 들면 view.pug이다

- pug는 들여쓰기가 중요.

- rails에 비교하면 view.html.erb와 비슷하다.

  - app.js에서 사용하는 법

    ```javascript
    app.set('views', './views_file');   //원래는 /views가 초기값
    app.set('view engine', 'pug');
    
    app.locals.pretty = true;		//템플릿에서 html으로 render 되면서 잘 정리해줌.
    
    res.render(file[, {topics:files}]);    //file을 render해줌. (topics라는 이름으로 files들을 담는다.)
    ```



**Express**

- Nodejs에서 사용되는 웹개발 프레임웍이다.

  ```javascript
  var express = require('express');
  var app = express();
  app.listen(Port, function(){
  	res.send('connected!');
  })
  ```



**Get방식**

```javascript
app.get(path, function(req,res){
	res.send(‘hello’);		//hello를 출력.
})

// GET /search?q=tobi+ferret
req.query.q
// => "tobi ferret"

app.get([‘/topic’, ‘/topic/:id’], function(req,res){
	var id = req.params.id
	if(id){
		————		//‘/topic/:id’로 들어온 경우 실행
	} else {
		————		//‘/topic’으로 들어온 경우 실행
	}
})
```



**Post 방식**

```javascript
var bodyParser = require('body-parser');
app.use(bodyParser.urlencoded({ extended: false }));		//post방식을 사용하기 위해서는 body-parser가 필요.

app.post(path, function(req,res){
	var title = req.body.title;		//post는 body로 받는다.
})

-readdir

fs.readdir('data', function(err, files){	//‘data’폴더에 있는 파일들을 files에 담음.
    if(err){							//에러 잡아내기.
      console.log(err);
      res.status(500).send('Internal Server Error');
    }
    res.render('new', {topics:files});
 })								//require(‘fs’);가 필요함.
```



**readFile**

- data폴더 안에 있는 파일들을 읽어주는 기능

```javascript
fs.readFile('data/'+id, 'utf-8', function(err,data){	//‘data’폴더에서 id라는 이름의 파일 내용을 data에 담는다.
 	if(err){
		console.log(err);
		res.status(500).send('Internal Server Error');
	}
	 res.render('view', {title:id, topics:files, description:data});
})
```



**WriteFile**

- data폴더 안에 form으로 받은 내용들을 파일로 저장해주는 기능

```javascript
fs.writeFile('data/'+title, description, function(err){	//data폴더안에 title이라는 이름으로 description내용을 넣어서 생성함
	if(err){
		console.log(err);
		res.status(500).send('Internal Server Error');
	}
	res.redirect('/topic/'+title);					//‘/topic/title’로 리다이렉트
});
```

