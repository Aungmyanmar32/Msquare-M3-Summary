## MSquare Programing Fullstack Course
### Episode-*35* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>
### File upload (express)

အကြောင်း လေ့လာသွားပါမယ်။
##
### ပြင်ဆင်ခြင်း
- express-file-upload ဆိုပြီး project folderတစ်ခု ဆောက်ပါ။
- project folder ထဲမှာ **`npm init`** လုပ်ပေးပါ။
- project folder အောက်မှာ server.js ဖိုင်တစ်ခုလုပ်ပါ။
- express ကို install လုပ်ပြီး server.js မှာ express app တစ်ခုလုပ်ထားပေးပါ။
```js
// server.js
const express = require("express");
const app = express();
const port = 3000;

app.use(express.static("public"));



app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});


```
- project folder အောက်မှာ  public folder တစ်ခု ထပ်လုပ်ပါ။
- public folder ထဲမှာ index.html script.js style,css ဖိုင်တွေထပ်လုပ်ပေးပါ။
- index.html ထဲမှာ  **bootstrap CDN** /**style.css**  /**script.js** ကို ချိတ်ထားပေးပါ။
- index.html ထဲမှာ bootstrap ကို သုံးပြီး file input တစ်ခုနဲ့ upload button တစ်ခု ထည့်ပေးထားပါမယ်။
- upload button ကိုလည်း click event ဖမ်းထားပြီး uploadFile ဆိုတဲ့ function ကို ခေါ်ထားပါမယ်။
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
      <input class="form-control" type="file" id="formFile" />
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
- nodemon module ကို Dev dependency အနေနဲ့ install လုပ်ပြီး package.json မှာ nodemon နဲ့ server start ဖို့ script တစ်ခု ထည့်ပေးပါမယ်။
```json
//package.json

{
  "name": "fileupload",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "start": "nodemon server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^2.0.20"
  }
}
```
- npm start နဲ့ serve  ကို run လိုက်တဲ့ အခါ  ခုလိုပြပေးနေမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep35r21.png)

##
### Upload npm project to GitHub
- GitHub မှာ npm project တွေ တင်တဲ့အခါ node_modules folder က file size များတဲ့အတွက် GitHubကို တင်လေ့မရှိပါဘူး။
- git add/commit လုပ်တဲ့အချိန် မှာ မပါစေချင်တဲ့ file/folder တွေကို .gitignore file ထဲမှာ ရေးထားပေးရပါမယ်။
- project folder အောက်မှာ **`.gitignore`** file တစ်ခုလုပ်ပါ။ ဖိုင်နာမည်ရဲ့ အစမှာ **`.`** ပါတာကို သတိပြုပါ။
- node_modules folder ကို မပါစေချင်တဲ့အတွက် **`.gitignore`**  ဖိုင်ထဲမှာ ထည့်ပေးရပါမယ်။
```js
# .gitignore file
node_modules/
```
- GitHub မှာ repo အသစ်တစ်ခုဆောက်ပြီး ခု project နဲ့ ချိတ်ပေးလိုက်ပါ။
##
### Script.js မှာ ဆာဗာဆီ file upload အတွက် ပြင်ဆင်ပါမယ်။
```js
//script.js

const fileInput = document.getElementById("formFile");

const uploadFile = async () => {
  const fileToUpload = fileInput.files[0];
  console.log(fileToUpload);
  const response = await fetch("http://localhost:3000/upload", {
    method: "POST",
    body: fileToUpload,
  });
  const data = await response.json();
  console.log(data);
};
```
`const fileInput = document.getElementById("formFile");`
- file input tag ကို လှမ်းယူထားတာပါ

`const uploadFile = async () => {}`
- upload ခလုတ်ကို နှိပ်ချိန်မှာ ခေါ်ထားတဲ့ function ကို သတ်မှတ်လိုက်တာဖြစ်ပါတယ်

`const fileToUpload = fileInput.files[0];`
`console.log(fileToUpload);`
- file input tag မှာ file  တစ်ခုခု ထည့်လိုက်ချိန်မှာ files list တစ်ခုကို ထုတ်ပေးပါတယ်။
- ထို files list ထဲက ပထဆုံး item ကို ယူလိုက်ပြီး fileToUpload ဆိုတဲ့ variable ထဲ သိမ်းလိုက်ပြီး log ထုတ်ကြည့်ထားပါတယ်။
```js
const response = await fetch("http://localhost:3000/upload", {
    method: "POST",
    body: fileToUpload,
  });
  const data = await response.json();
  console.log(data);
```
- fecth နဲ့ server ဆီ /upload route ကနေတစ်ဆင့် post method ကို သုံးကာ files list ထဲက ပထဆုံး item ကို body ထဲ ထည့်ပြီး request လုပ်လိုက်တာဖြစ်ပါတယ်
- response ပြန်လာတဲ့ data  ကို လည်း log ထုတ်ကြည့်ထားပါတယ်။
##
### express server မှာ /upload route နဲ့ ၀င်လာတဲ့ request ကို post middlewareသုံးပြီး ဖမ်းပါမယ်
```js
//server.js
const express = require("express");
const app = express();
const port = 3000;

app.use(express.static("public"));

app.post("/upload", (req, res) => {
  res.send({ message: "Upload successful" });
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
- static middlewareကို သုံပြီး public folder ထဲက ဖိုင်တွေကို read/response လုပ်ထားပါတယ်
```js
app.post("/upload", (req, res) => {
  res.send({ message: "Upload successful" });
});
```
- /upload route ကနေ post method နဲ့  ၀င်လာတဲ့ request  ကို ဖမ်းလိုက်ပြီး object တစ်ခုပဲ response ပြန်ပေးလိုက်ပါတယ်။
- browser မှာ localhost:3000 ကို သွားပြီး file input မှာ ဖိုင်တစ်ခု ရွေးပေးပြီး upload button ကိုနှိပ်ကြည့်ပါက
- - script.js မှာ log ထုတ်ထားတဲ့ fileToUpload နဲ့ ဆာဗာက ပြန်လာတဲ့ object ကိုconsole ထဲမှာ ပြပေးနေမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep35r22.png)

- ခုသင်ခန်းစာမှာတော့ front-end ကို ပို့လိုက်တဲ့ ဖိုင်ကို လက်မခံသေးပဲ ပြင်ဆင်ထားရုံပဲ လုပ်ထားပါတယ်။
- ဆက်လက်ပြီး REQUEST  ၀င်လာတဲ့ ဖိုင်ကို လက်ခံပြီး cloud server ပေါ်မှာ တင်နည်းကို နောက်သင်ခန်းစာမှာ လေ့လာကြပါမယ်။

