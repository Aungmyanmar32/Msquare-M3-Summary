## MSquare Programing Fullstack Course
### Episode-*37* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>
### multiple file upload
### formdata
### multer
အကြောင်း လေ့လာသွားပါမယ်။
##
အရင် သင်ခန်းစာမှာတော့ file တစ်ခုကို server  ဆီ upload လုပ်တဲ့အကြောင်း လေ့လာခဲ့ပြီးပါပြီး
- ဒီနေ့ သင်ခန်းစာမှာတော့ ဖိုင် နှစ်ခုကို upload လုပ်တဲ့ အကြောင်း လေ့လာကြရအောင်
- index.html က  file input မှာ multiple attribute ကို ထည့်ပေးလိုက်ပါမယ်။
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD"
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="style.css" />
    <title>Express file Upload</title>
  </head>
  <body>
    <div class="container">
      <h1>Express file Upload</h1>
      <input class="form-control" type="file" id="formFile" multiple />
      <button class="btn btn-primary m-3" onclick="uploadFile()">Upload</button>
    </div>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
      crossorigin="anonymous"
    ></script>
    <script src="script.js"></script>
  </body>
</html>

```
- script.js မှာ route အသစ်နဲ့ file input ထဲ ဖိုင်တွေကို server ဆီ request လုပ်ပါမယ်.
```js
const fileInput = document.getElementById("formFile");

const uploadFile = async () => {
  const formData = new FormData();
  formData.append("files", fileInput.files[0]);
  formData.append("files", fileInput.files[1]);
  const response = await fetch("http://localhost:3000/upload-multiple", {
    method: "POST",
    body: formData,
  });
  const data = await response.json();
  console.log(data);
};

```
`const formData =  new  FormData();`
- formData အသစ်တစ်ခု လုပ်လိုက်ပါတယ်
``` js
formData.append("files", fileInput.files[0]);
formData.append("files", fileInput.files[1]);
  ```
- formData ထဲကို input files list ထဲက first item နဲ့ second item ကို files ဆိုတဲ့ key (name) ထဲ append လုပ်လိုက်တာပါ။
```js
const response = await fetch("http://localhost:3000/upload-multiple",{ 
method:  "POST", 
body: formData,  
});
```
- `/upload-multiple` ဆိုတဲ့ route ကို POST method နဲ့ request လုပ်လိုက်ပြီး formData ကိုပါ လှမ်းပို့လိုက်ပါတယ်။
- client က ပို့လာတဲ့ request နဲ့  data တွေကို server မှာ လက်ခံပါမယ်
- client u ပို့လာတဲ့ data ( files) တွေကို လက်ခံဖို့ multer ဆိုတဲ့ node module တစ်ခုကို အသုံးပြုပါမယ်
## multer
- Syntax 1

 ```
multer({ key : value})
```
example
```js

const upload = multer({ dest: 'uploads/' })
// client က ၀င်လာတဲ့ file ကို uploads ဆိုတဲ့ folder မှာ သိမ်းမယ်ဆိုတာ သတ်မှတ်လိုက်တာပါ
```

##
- Syntax 2
```javascript
multer.middleware({ key: function(req,file,cb){...} })
```
Example
```javascript
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "uploads/");
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + "-" + file.originalname);
  },
});
// destination မှာ file ဘယ်မှာသိမ်းမလဲ သတ်မှတ်လိုက်ပြီး
// filename ကတော့ သိမ်းမယ့်ဖိုင် နာမည် သတ်မှတ်ပေးလိုက်တာဖြစ်ပါတယ်။
```
- install multer to project
`npm i multer`

- multer ကို  install လုပ်ပြီးပြီးဆိုရင် server.js မှာ require နဲ့ ထည့်ပြီး အသုံးပြုလို့ရပါပြီး
```js
const  multer = require("multer");
```
- multer ကို သုံးပြီး သိမ်းမယ့်နေရာနဲ့ ဖိုင်နာမည်ကို  server.js မှာ သတ်မှတ်ပါမယ်
```js
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "uploads/");
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + "-" + file.originalname);
  },
});
```
`const storage = multer.diskStorage`
- multerထဲက diskStorage middlewareကို အသုံးပြုလိုက်ပြီး ရလာတဲ့ result ကို storage မှာ သိမ်းလိုက်ပါတယ်
``` 
  destination: function (req, file, cb) {
    cb(null, "uploads/");
  },
  ```
-  destination key မှာတော့ file ကို uploads folderထဲသိမ်းရန် သတ်မှတ်လိုက်ပြီး
```
filename: function (req, file, cb) {
    cb(null, Date.now() + "-" + file.originalname);
  },
```
- // filename မှာကတော့ သိမ်းမယ့်ဖိုင် နာမည် ကို လက်ရှိအချိန်-မူလဖိုင်နာမည် ဆိုပြီးသတ်မှတ်ပေးလိုက်တာဖြစ်ပါတယ်။
- - ဥပမာ ။  ။ dog.jpg ဆိုတဲ့ ပုံတစ်ခု upload  လိုက်ရင် multer က server မှာ 1677679697893-dog.jpg ဆိုပြီး uploads folder ထဲမှာ သွားသိမ်းပေးဖို့ သတ်မှတ်ထားတာ ဖြစ်ပါတယ်။
- ဆက်ပြီးတော့ အထက်က ရလဒ်တွေကို သိမ်းထားတဲ့ storage variable ကို server မှာရှိတဲ့ /upload-multiple ဆို  route က request လက်ခံတဲ့နေရာမှာ သုံးနိုင်အောင် လုပ်ပါမယ်။
```js
const upload = multer({storage: stroge});
//or
const upload = multer({ storage });
// JS က object မှာ key နဲ့ value က စာလုံးတူနေရင် တစ်ခုပဲ ရေးလို့ရပါတယ်
```
- အခုဆိုရင် express မှာ client က ၀င်လာတဲ့ request ကို လက်ခံပြီး response လုပ်ပါမယ်။
```js
app.post("/upload-multiple", upload.array("files"), (request, response) => {
  console.log(request.files);
  response.send({ message: "file uploaded successfully" });
});
```
- express post middleware မှာ parameter သုံးခုလက်ခံထားပါတယ်
- ပထမ parameter က request ၀င်လာမယ့် route ဖြစ်ပါတယ်
- ဒုတိယ parameter က multer က လုပ်ထားတဲ့ upload ဖြစ်ပြီး သူ့အထဲမှာ request က ပါလာတဲ့ formData က files တွေကို လက်ခံထားပါတယ်
- တတိယ parameter ကတော့ callback function ဖြစ်ပြီး client ဆီ response ပြန်လုပ်ထားပါတယ်
- ---
- upload လုပ်လာတဲ့ files တွေသိမ်းဖို့ uploads folder ကို project folder ထဲမှာ လုပ်ပေးရပါမယ်
```console
// terminal
Admin@MSquare MINGW64 ~/Desktop/exercises/fileupload (main)
$ mkdir uploads
```
- အခုဆိုရင် ဖိုင်နှစ်ခု တစ်ပြိုင်ထဲ upload လုပ်နိုင်ဖို့ ပြင်ဆင်ပြီးပါပြီး
- npm start နဲ့ server run လိုက်ပြီး browser က file input မှာ file နှစ်ရွေးပြီး upload လုပ်ကြည့်ပါက project အောက်က uploads folder ထဲမှာ သိမ်းထားပေးတာကို တွေ့ရမှာဖြစ်ပါတယ်။
### All code in this project
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD"
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="style.css" />
    <title>Express file Upload</title>
  </head>
  <body>
    <div class="container">
      <h1>Express file Upload</h1>
      <input class="form-control" type="file" id="formFile" multiple />
      <button class="btn btn-primary m-3" onclick="uploadFile()">Upload</button>
    </div>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
      crossorigin="anonymous"
    ></script>
    <script src="script.js"></script>
  </body>
</html>

```
```js
// script.js

const fileInput = document.getElementById("formFile");

const uploadFile = async () => {
  const formData = new FormData();
  formData.append("files", fileInput.files[0]);
  formData.append("files", fileInput.files[1]);
  const response = await fetch("http://localhost:3000/upload-multiple", {
    method: "POST",
    body: formData,
  });
  const data = await response.json();
  console.log(data);
};

```
```js
// server.js

const express = require("express");
const fs = require("fs");
const multer = require("multer");
const app = express();
const port = 3000;

app.use(express.static("public"));

const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "uploads/");
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + "-" + file.originalname);
  },
});

const upload = multer({ storage });

app.post("/upload", (req, res) => {
  const fileStream = fs.createWriteStream(`image.jpg`);
  req.pipe(fileStream);
  res.send({ message: "Upload successful" });
});

app.post("/upload-multiple", upload.array("files"), (request, response) => {
  console.log(request.files);
  response.send({ message: "file uploaded successfully" });
});
app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});

```

