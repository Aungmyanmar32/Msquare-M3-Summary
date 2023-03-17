## MSquare Programing Fullstack Course
### Episode-*41* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>

###  digital ocean space server ဆီ ပုံတစ်ပုံ တင်ပြီးတာနဲ့ သူ့အထဲမှာ ရှိတဲ့ Contents တွေကို တစ်ခါတည်း ရယူပြီး UI မှာပြပေးတာ ဆက်လုပ်ပါမယ်

##
### ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ project အသစ်တစ်ခုလုပ်ပြီး DOC space ဆီ request လုပ်ကာ ရလာတဲ့ data ကို server မှာပဲ log ထုတ်ကြည့်ခဲ့ပါတယ်
- ခု သင်ခန်းစာမှာတော့ **အရင် သင်ခန်းစာ projcet(Episode 40) အဟောင်း**မှာပဲ DOC ဆီကို ပုံလဲတင် request လဲ လုပ်ပြီး ရလာတဲ့ data တွေကို browser  console မှာ log ထုတ်ပြနိုင်အောင် လေ့လာသွားကြပါမယ်။
- အရင် ဆုံး require နဲ့ module တွေ လှမ်းယူထားတာကို import နဲ့ ပြောင်းရေးကြပါမယ်။
-  import ကို သုံးချင်ရင် package.json မှာ `"type":"module"`  ဆိုတာလေး ထည့်ပေးရပါမယ်
```js
// package.json

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
  "type": "module",
  "dependencies": {
    "@aws-sdk/client-s3": "^3.282.0",
    "aws-sdk": "^2.1328.0",
    "express": "^4.18.2",
    "multer": "^1.4.5-lts.1",
    "multer-s3": "^2.10.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.20"
  }
}
```
- ပြီးရင် server.js မှာ require နဲ့ လုပ်ထားတာတွေကို  import ပြောင်းရေးပါမယ်။
```js
// server.js

import express from "express";
import multer from "multer";
import aws from "aws-sdk";
import multerS3 from "multer-s3";
```
- ဆက်ပြီး DOC space bucket ဆီ request send ဖို့အတွက်ပြင်ဆင်ပါမယ်။
- အရင်ဆုံး project အောက်မှာ libs folder တစ်ခုလုပ်ပြီး အထဲမှာ fileMananger.js ဖိုင်တစ်လုပ်ပေးပါ။
- -ပြီးရင် @aws-sdk/client-s3 module ကို install လုပ်ပေးပါ
```console
// terminal


aungm@MSquare MINGW64 ~/Desktop/fileupload
$ mkdir libs && cd libs/

aungm@MSquare MINGW64 ~/Desktop/fileupload/libs
$ touch fileMananger.js

aungm@MSquare MINGW64 ~/Desktop/fileupload/libs
$ cd ..

aungm@MSquare MINGW64 ~/Desktop/fileupload
$ npm i @aws-sdk/client-s3
```
- fileMananger.js ထဲမှာ ပြီးခဲ့တဲ့ သင်ခန်းစာက code တွေ ကူးထည့်ပြီး အနည်းငယ် ပြင်ရေးပါမယ်
```js
//fileMananger.js

import { S3 } from "@aws-sdk/client-s3";
import { ListObjectsCommand } from "@aws-sdk/client-s3";


const s3Client = new S3({
    endpoint: "https://sgp1.digitaloceanspaces.com/",
    region: "asia",
    credentials: {
      accessKeyId: "DO00AKAWLRVPT3XBKMQC",
      secretAccessKey: "Sz9cmmtb0csW6MccES3kTAqxwWZJ8hMqdE42xg19OiA",
    },
  });
  



const bucketParams = { Bucket: "msquarefdc" };

export const run = async () => {
  try {
    const data = await s3Client.send(new ListObjectsCommand(bucketParams));
    console.log("Success", data);
    return data;
  } catch (err) {
    console.log("Error", err);
  }
};
```
> ရှင်းလင်းချက်

    import { S3 } from "@aws-sdk/client-s3";
    import { ListObjectsCommand } from "@aws-sdk/client-s3";
 
   - လိုအပ်တဲ့ S3 နဲ့  ListObjectsCommand ကို @aws-sdk/client-s3 ကနေ import လုပ်ထားပါတယ်။
   ```js
   const s3Client = new S3({
    endpoint: "https://sgp1.digitaloceanspaces.com/",
    region: "asia",
    credentials: {
      accessKeyId: "DO00AKAWLRVPT3XBKMQC",
      secretAccessKey: "Sz9cmmtb0csW6MccES3kTAqxwWZJ8hMqdE42xg19OiA",
    },
  });
```
- import  လုပ်ထားတဲ့ S3ကို သုံးပြီး s3Client တစ်ခု လုပ်လိုက်ပါတယ်။

```js
const bucketParams = { Bucket: "msquarefdc" };

export const run = async () => {
  try {
    const data = await s3Client.send(new ListObjectsCommand(bucketParams));
    console.log("Success", data);
    return data;
  } catch (err) {
    console.log("Error", err);
  }
```
- bucketParams တစ်ခု သတ်မှတ်ထားပါတယ်
- s3Client + bucketParams ကိုသုံးပြီး import  လုပ်ထားတဲ့ ListObjectsCommand နဲ့  DOC server ဆီ request လုပ်ထားတာဖြစ်ပါတယ်
- request လုပ်ထားတဲ့ function ကို run ဆိုတဲ့ variable ထဲ သိမ်းထားပြီး export လုပ်ထားပါတယ်။  
- run ဆိုတဲ့ variable ဟာ function တစ်ခု ဖြစ်ပြီး DOC server ဆီ က response ပြန်လာတဲ့ data ကို return လုပ်ပါတယ်။
- run ဆိုတဲ့ function ကို export လုပ်ထားတာမလို့ server.js မှာ import လုပ်ပြီး အသုံးပြုလို့ ရပါပြီး။
```js
//server.js

import express from "express";
import multer from "multer";
import aws from "aws-sdk";
import multerS3 from "multer-s3";
import {run} from "./libs/fileMananger.js"

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
    const data = await run();
    const fileContents = data.Contents
    response.send({ message: "file upload successful",fileContents });
  });
});


app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});

```

    import {run} from "./libs/fileMananger.js"
- run function ကို fileMananger.js ကနေ import လုပ် ခေါ်သုံးလိုက်တာဖြစ်ပါတယ်။

```js
app.post("/cloudUpload", (request, response, next)=> {
  upload(request, response, async(error)=> {
    if (error) {
      console.log(error);
      return response.send({ message: "file upload error" });
    }
    console.log("File uploaded successfully.");
    const contentData = await run();
    const fileContents = contentData.Contents
    response.send({ message: "file upload successful",fileContents });
  });
});

```
- file upload လုပ်ထားတဲ့ post middleware အထဲမှာပဲ run function ကို ခေါ်ထားပြီး return ပြန်လာတဲ့ data ကို contentData variable  ထဲမှာ သိမ်းလိုက်ပါတယ်
- contentData ထဲက Contents array ကိုပဲ လိုချင်တာမလို့ 
```
    const fileContents = contentData.Contents
```

- ဆိုပြီး ထပ်လုပ်ထားပါတယ်။
- နောက်ဆုံးရလာတဲ့ array ကို response.send method နဲ့ response ပြန်တဲ့ object အထဲမှာ ထည့်ပြီး client ဆီ ပို့ပေးလိုက်ပါတယ်။
- ခု npm start လုပ်ပြီး ပုံတစ်ပုံ တင်ကြည့်ပါက fileUpload successful ဆိုတဲ့ message အပြင် fileContents ဆိုတဲ့ array တစ်ခုပါ console log ထုတ်ပြပေးတာကို တွေ့ရမှာပါ။
##
### ရလာတဲ့ array ကို ကိုယ့် folder နာမည်နဲ့ filter လုပ်ပြီး log  ထုတ်ကြည့်ပါ။
