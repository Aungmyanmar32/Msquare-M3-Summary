
## MSquare Programing Fullstack Course
### Episode-*39* 
### Summary For `Room(2)` 
##
### Upload file on Digital ocean
##
### အရင်နေ့က သင်ခန်းစာကိုပဲ ဒီနေ့မှာ ပြန်လေ့ကျင့်သွားမှာဖြစ်ပါတယ်
- အရင်ဆုံး projcet အသစ်တစ်ခုလုပ်ပါမယ်
- terminal ကို ဖွင့်ပါ 
```console
//terminal
Admin@MSquare MINGW64 ~/Documents/projects/ep38-project
$ cd

Admin@MSquare MINGW64 ~
$ cd Documents/

Admin@MSquare MINGW64 ~/Documents
$ cd projects/

Admin@MSquare MINGW64 ~/Documents/projects
$ mkdir dc-file-upload

Admin@MSquare MINGW64 ~/Documents/projects
$ cd dc-file-upload/

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload
$ git init
Initialized empty Git repository in C:/Users/Admin/Documents/projects/dc-file-upload/.git/

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload (master)
$ touch .gitignore server.js

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload (master)
$ mkdir public

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload (master)
$ cd public

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload/public (master)
$ touch index.html script.js style.css

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload/public (master)
$ cd ..

Admin@MSquare MINGW64 ~/Documents/projects/dc-file-upload (master)
$ code .

```
- အပေါ်က ကုဒ်တွေကို terminal ထဲမှာ တစ်ကြောင်းခြင်းစီ ရိုက်ထည့်ပေးလိုက်တာနဲ့ dc-file-upload ဆိုတဲ့ project folder အသစ် တစ်ခု လုပ်ပေးပြီး လိုအပ်မယ့်ဖိုင်တွေပါ တစ်ခါတည်း လုပ်ပေးကာ vs code အသစ်မှာ ဖွင့်ပေးလာပါမယ်။
- အသစ်လုပ်ထားတဲ့ project အထဲမှာ npm ကို ထည့်ပြီး လိုအပ်မယ့် module တွေပါ တစ်ပါတည်း install လုပ်ပါမယ်။
 ### Termianl
```properties

 npm init -y

```
```properties

 npm i express aws-sdk multer multer-s3@2.10.0

```
```properties

 npm i -D nodemon

```
- package.json မှာလည်း script  object မှာ အနည်းငယ် ပြင်ပါမယ်။
```properties
// package.json

{
  "name": "dc-file-upload",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "aws-sdk": "^2.1329.0",
    "express": "^4.18.2",
    "multer": "^1.4.5-lts.1",
    "multer-s3": "^2.10.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.21"
  }
}
```
- `index. html` `script.js` မှာ အရင် သင်ခန်းစာက  code တွေ ပြန်ရေးထည့်ပါမယ်။
```html
<!-- public/index.html -->
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
// public/script.js
const fileInput = document.getElementById("formFile");

const uploadFile = async () => {
  const filesList = fileInput.files;
 
  console.log(fileArray);

  const formData = new FormData();
  formData.append(fileList[0])
  formData.append(fileList[1])

  const response = await fetch("http://localhost:3000/cloudUpload", {
    method: "POST",
    body: formData,
  });
  const data = await response.json();
  console.log(data);
};

```

- server.js မှာ လိုအပ်တဲ့ module တွေကို requireလုပ်ပြီး epxress server တစ်ခု လုပ်ပါမယ်။
```js

// server.js


const express = require("express");
const fs = require("fs");
const multer = require("multer");
const aws = require("aws-sdk");
const multerS3 = require("multer-s3");

const app = express();
const port = 3000;

app.use(express.static("public"));


app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
- Digital Ocean bucket မှာ file upload လုပ်ဖို့ စပါမယ်
### Step -1
- အရင် သင်ခန်းစာမှာ **လုပ်ထားပြီးသူများ *Step -1* ကို ထပ်လုပ်ပေးစရာ မလိုပါ**
- user directory ထဲကို cd နဲ့ သွားပြီး .aws folder တစ်ခုလုပ် ၊ credentials ဖိုင်တစ်ခုလုပ်လိုက်ပါ။
- credentials ဖိုင်ထဲမှာ အောက်က ကုဒ်တွေ ထည့်းပေးရမှာ ပါ။

```properties
[default]
aws_access_key_id=your_access_key
aws_secret_access_key=your_secret_key

```
> မှတ်ချက် ။  ။ access_key နှင့် secret_key ကို ဆရာ (သို့) အောင်မြန်မာ ဆီမှာ ရယူပါ။

### Step -2
- aws sapce endpoint တစ်ခုကို server.js မှာ လုပ်ပါမယ်
```js
// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint('sgp1.digitaloceanspaces.com');
const s3 = new aws.S3({
  endpoint: spacesEndpoint
});
```
### Step -3
- multer-s3 နဲ့ multerကို သုံးပြီး storage  တစ်ခုကို server.js မှာ လုပ်ပါမယ်
 ```js


// make multer storage
const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: 'msquarefdc',
    acl: 'public-read',
    key: function (request, file, cb) {
      console.log(file);
      cb(null, file.originalname);
    }
  })
}).array('files', 1);

```

### Step -4
- script.js ကနေ request လုပ်လာမယ့် route ကို အသုံးပြုပြီး   digital ocean spaceမှာ files upload အတွက် server.js မှာ ပြင်ဆင်ပါမယ်
```js
app.post("/cloudUpload", function (request, response, next) {
  upload(request, response, function (error) {
    if (error) {
      console.log(error);
      return response.send({ message: "file upload error" });
    }
    console.log("File uploaded successfully.");
    response.send({ message: "file upload successful" });
  });
});
```
- အခုဆိုရင် digital ocean spaceမှာ files upload လုပ်လို့ရပါပြီး။
##
### Upload file in Folder
- ကျနော်တို့ တင်လိုက်တဲ့ ဖိုင်တွေကို digital ocean space မှာ folder တစ်ခုနဲ့ သိမ်းထားလို့ရပါတယ်။
- multer storage လုပ်တဲ့ code မှာ အနည်းငယ် ပြင်ပေးရမှာ ဖြစ်ပါတယ်
 ```js


// make multer storage
const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: 'msquarefdc',
    acl: 'public-read',
    key: function (request, file, cb) {
      console.log(file);
      cb(null, " သင့်folderအမည်/"+ file.originalname);
      //replace folder name in string
    }
  })
}).array('files', 1);

```
### All code in Server.js
```js
const express = require("express");
const fs = require("fs");
const multer = require("multer");
const aws = require("aws-sdk");
const multerS3 = require("multer-s3");

const app = express();
const port = 3000;

app.use(express.static("public"));

// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint("sgp1.digitaloceanspaces.com");
const s3 = new aws.S3({
  endpoint: spacesEndpoint,
});

// Change bucket property to your Space name
const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: "msquarefdc",
    acl: "public-read",
    key: function (request, file, cb) {
      console.log(file);
      cb(null,"aung-myanmar/"+ file.originalname);
      //replace your folder name in string
    },
  }),
}).array("files", 1);

app.post("/cloudUpload", function (request, response, next) {
  upload(request, response, function (error) {
    if (error) {
      console.log(error);
      return response.send({ message: "file upload error" });
    }
    console.log("File uploaded successfully.");
    response.send({ message: "file upload successful" });
  });
});


app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
