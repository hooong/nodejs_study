# multer

- 컴퓨터의 파일을 업로드를 가능하게 해주는 모듈

```javascript
var multer = require('multer');   //파일업로드 모듈
var _storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, 'uploads/')

    //callback사용
    //if(파일의 형식이 이미지면)
    // cb(null, 'uploads/images')
    //else if(텍스트이면)
    // cb(nulll, 'uploads/texts')
  },
  filename: function (req, file, cb) {
    cb(null, file.originalname)
  }
})      //dest대신 storage를 사용, 파일명도 설정가능해짐. var upload = multer({ dest: 'uploads/' })
var upload = multer({ storage: _storage })

app.post('/upload', upload.single('userfile') , function(req,res){    //미들웨어
  res.send('uploaded : '+req.file.filename);
})											//파일업로드하기.

app.use('/user', express.static('uploads'));  //주소창에서 uploads폴더안의 파일에 접근가능.
```

