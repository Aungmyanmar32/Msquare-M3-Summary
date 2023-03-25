## MSquare Programing Fullstack Course
### Episode-*45* 
### Summary For `Room(2)` 
## Express with Typescript
### အရင်က file upload လုပ်တဲ့ PROJECT ကို typescript နဲ့ ပြန်ရေးကြည့်ပါမယ်
- github repo တစ်ခုလုပ်ပြီး clone ထားပါ
- clone လို့ ရလာတဲ့ folder ထဲမှာ npm init လုပ်ပါ။
-  server.ts နဲ့ .gitignore ဖိုင်နှစ်ခုလုပ်ပါ။
- လိုအပ်မယ့် module တွေကို install လုပ်ပေးပါ။
```console
npm init -y
touch server.ts .gitignore
npm i express aws-sdk @aws-sdk/client-s3 multer multer-s3@2.10.0
npm i -D nodemon ts-node
```
-  ပြီးရင် package.json မှာ start script တစ် ထည့်ပါမယ်
`"start": "nodemon server.ts"`
```js
//package.json

{
  "name": "express-doc-fileupload-ts",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon server.ts"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/Aungmyanmar32/express-doc-fileupload-ts.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/Aungmyanmar32/express-doc-fileupload-ts/issues"
  },
  "homepage": "https://github.com/Aungmyanmar32/express-doc-fileupload-ts#readme",
  "dependencies": {
    "@aws-sdk/client-s3": "^3.299.0",
    "aws-sdk": "^2.1343.0",
    "express": "^4.18.2",
    "multer": "^1.4.5-lts.1",
    "multer-s3": "^2.10.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.22",
    "ts-node": "^10.9.1"
  }
}

```
- server.ts မှာ express server တစ်ခုကို typescript( ts ) နဲ့ တည်ဆောက်ပါမယ်။
```js
//server.js

import express from "express";
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});
app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
- node module တွေရဲ့ သတ်မှတ်ပြီးသား typescript type တွေကို @types/module-name နဲ့ install လုပ်ပြီး အသုံးပြုနိုင်ပါတယ်
- ခု express အတွက် typeတွေကို install လုပ်ပြီး ထည့်ပါမယ်
`npm i @types/express`
- ပြီးရင် အရင် project ထဲက public folder, libs folder နဲ့ server.js ထဲက file upload လုပ်တဲ့ code တွေကို ခု project ထဲ ကူးထည့်ပါမယ်
```js
// server.js

import express from "express";
import multer from "multer";
import aws from "aws-sdk";
import multerS3 from "multer-s3";
import {run} from "./libs/fileMananger"


const app = express();
const port = 3000;

app.use(express.static("public"));


// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint("sgp1.digitaloceanspaces.com");
const s3 = new aws.S3({
  endpoint: spacesEndpoint,
});


const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: "msquarefdc",
    acl: "public-read",
    key: function (request, file, cb) {
      console.log(file);
      cb(null, "aung-myanmar/" + file.originalname);
    },
  }),
}).array("files", 1);

app.post("/cloudUpload", (request, response, next)=> {
  upload(request, response, async(error)=> {
    if (error) {
      console.log(error);
      return response.send({ message: "file upload error" });
    }
    console.log("File uploaded successfully.");
    const contentData  = await run();
    console.log(contentData);
   const fileContents = contentData.Contents
    response.send({ message: "file upload successful", fileContents});
  });
});


app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});


```
- copy လုပ်တဲ့ အထဲမှာ aws-sdk , multer , multer-s3 စတဲ့ node module တွေ ပါလာတာမလို့ ထို module တွေ အတွက် typescript type တွေကို install လုပ်ပါမယ်။
`npm i @types/aws-sdk @types/multer @types/multer-s3`
- install လုပ်ပြီးရင် error ပြနေတဲ့ နေရာတွကို type လုပ်ပါမယ်
- ပထမဆုံး upload function ထဲက s3 မှာ error ပြနေတာကို ဖြေရှင်းပါမယ်။
- လောလောဆယ် ကျနော်တို့ project မှာ s3ကို npm package ကနေ type တွေ ထည့်ပေး ထားသော်လည်း သူရဲ့ type ကို typescript က မသိပဲ error ပြနေပါတယ်
- အ့လိုမျိုး error ကို ထို type မသိဖြစ်နေတဲ့  code ကို typescript အား ignore လုပ်ခိုင်းလိုက်ခြင်းနဲ့ ဖြေရှင်းနိုင်ပါတယ်
```js
const upload = multer({
  storage: multerS3({
    //@ts-ignore
    s3: s3,
    bucket: "msquarefdc",
    acl: "public-read",
    key: function (request, file, cb) {
      console.log(file);
      cb(null, "aung-myanmar/" + file.originalname);
    },
  }),
}).array("files", 1);
```
- //@ts-ignore ဆိုတာက သူ့အောက်က ကုဒ် တစ်ကြောင်းကို typescript အား လစ်လျူရှုခိုင်းလိုက်တာပါ။
- ဆက်ပြီးတော့ error ပြနေတဲ့ post middleware ထဲက error နဲ့ contentData တွေရဲ့ type ကို လတ်တလော any type လုပ်ပြီး ဖြေရှင်းလိုက်ပါမယ်။
```js
app.post("/cloudUpload", (request, response, next) => {
  upload(request, response, async (error: any) => {
    if (error) {
      console.log(error);
      return response.send({ message: "file upload error" });
    }
    console.log("File uploaded successfully.");
    const contentData: any = await run();
    console.log(contentData);
    const fileContents = contentData.Contents;
    response.send({ message: "file upload successful", fileContents });
  });
});

```
- libs folder ထဲက filemanager.js ဖိုင်ကို  filemanager.ts ဆိုပြီး typescript ပြောင်းလိုက်ပါမယ်။
- ခု server ကို npm start နဲ့ run ကြည့်ပါမယ်။
- ပုံတစ်ပုံ တင်စမ်းကြည့်တဲ့ အခါမှာ အရင် project  အဟောင်းတုန်းကလိုပဲ အလုပ်လုပ်နေတာကို မြင်ရမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-25%20220733.png)
