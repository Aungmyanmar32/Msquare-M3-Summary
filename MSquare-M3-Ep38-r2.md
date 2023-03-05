## MSquare Programing Fullstack Course
### Episode-*38* 
### Summary For `Room(2)` 
##
### Upload file on Digital ocean
##
### Agriculture
- အပြင် လက်တွေ့မှာ project တစ်ခုကို web ပေါ်တင်တဲ့ အခါ
- - server တစ်ခုထဲမှာပဲ code တွေ file(image/video/music etc...) အကုန်လုံးကို စုပြုံတင်လေ့မရှိပဲ text  ( code/link etc..) သီးသန့် ကို server တစ်ခု ၊ file သီးသန့်ကို server တစ်ခု ခွဲတင်လေ့ရှိပါတယ်။
-  ခုလို ခွဲတင်လိုက်ခြင်းအားဖြင့် မိမိရေးလိုက်တဲ့ web app/site ကို ပိုမိုမြန်ဆန်စွာ manage လုပ်နိုင်ပြီး user များ အဆင်ပြေပြေ အသုံး'ပြုနိုင်မှာ ဖြစ်ပါတယ်
- file သီသန်းတင်တဲ့ server မှာ file တစ်ခုကို တင်လိုက်တာနဲ့ ထိုဖိုင်အတွက် link တစ်ခုကို ပြန်ထုတ်ပေးတာကြောင့် code သီးသန့် တင်တဲ့ ဆာဗာမှာ text အနေနဲ့ ထိုဖိုင်ကို ထည့်သွင်းအသုံးပြုနိုင်တာမလို့ loading time ကို သိသိသာသာ မြန်ဆန်စေမှာ ဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/digitaloce1.png)

##
### Using digital ocean space ( file upload server )
-  digital ocean space ဆိုတာ file upload service ပေးတဲ့ server တွေထဲက တစ်ခု ဖြစ်ပါတယ်။
- free ရတဲ့ service မဟုတ်ပဲ paid service တစ်ခုဖြစ်ပါတယ်
- အောက်က link က tutorial ကို ဖတ်ကြည့်ပြီး file upload အတွက် ကိုယ်တိုင်ရေးသားကြည့်ကြပါမယ်။
https://www.digitalocean.com/community/tutorials/how-to-upload-a-file-to-object-storage-with-node-js

### Introduction (မိတ်ဆက်)

Object storage is a popular and scalable method of storing and serving static assets such as audio, images, text, PDFs, and other types of unstructured data. Cloud providers offer object storage in addition to traditional local or block storage, which is used to store dynamic application files and databases. Read  [Object Storage vs. Block Storage](https://www.digitalocean.com/community/tutorials/object-storage-vs-block-storage-services)  to learn about the use cases and differences between the two.

[Spaces](https://www.digitalocean.com/products/object-storage/)  is a simple object storage service offered by DigitalOcean. In addition to being able to login and upload, manage, and delete stored files through a control panel, you can also access your DigitalOcean Space through the command line and the Spaces API.

In this tutorial, we will create a Node.js application that allows a user to upload a file to their DigitalOcean Space by submitting a form on the front-end of a website. 
- မိတ်ဆက်မှာတော့ DigitalOcean Space အကြောင်း ပြောပြထားပါတယ်
- ကိုယ့်ဘာကိုယ် ဖတ်ကြည့်ကြပါ။
##
### Prerequisites (ကြိုတင် လိုအပ်သောအရာများ)

To follow along with this tutorial, you will need:

-   A DigitalOcean Space, along with an access key and secret access key to your account. Read  [How To Create a DigitalOcean Space and API Key](https://www.digitalocean.com/community/tutorials/how-to-create-a-digitalocean-space-and-api-key)  to get up and running with a DigitalOcean account, create a Space, and set up an API key and secret.
-   Node.js and npm installed on your computer. You can visit the  [Node.js Downloads](https://nodejs.org/en/download/)  to install the correct version for your operating system.

You should now have a DigitalOcean account, a Space with access key, and Node.js and npm installed on your computer.
- ဘာမှမလုပ်ခင် access key and secret access key  နှစ်ခု အရင်ရှိထားရပါမယ်။
- access key and secret access key တွေကို ဆရာ (သို့) အောင်မြန်မာ ဆီ တိုက်ရိုက်ဆက်သွယ်ပြီး ရယူနိုင်ပါတယ်။
- နောက်လိုအပ်တာကတော့ NodeJS ကို စက်ထဲသွင်းထားရပါမယ်။
##
## Add Access Keys to Credentials File

DigitalOcean Spaces is compatible with the  [Amazon Simple Storage Service (S3)](https://aws.amazon.com/s3/)  API, and we will be using the  [AWS SDK for JavaScript in Node.js](https://aws.amazon.com/sdk-for-node-js/)  to connect to the Space we created.

The first step is to create a  **credentials**  file, to place the access key and secret access key you obtained when you created your DigitalOcean Space. The file will be located at  **`~/.aws/credentials`**  on Mac and Linux, or  **`C:\Users\USERNAME\.aws\credentials`**  on Windows. If you have previously saved AWS credentials, you can read about  [keeping multiple sets of credentials](https://aws.amazon.com/blogs/security/a-new-and-standardized-way-to-manage-credentials-in-the-aws-sdks/)  for further guidance.

Open your command prompt, make sure you’re in your  **Users**  directory, have access to an administrative  `sudo`  user, and create the  **`.aws`**  directory with the  **`credentials`**  file inside.
```
  sudo mkdir .aws && touch .aws/credentials
```


Open the file, and paste the following code inside, replacing  `your_access_key`  and  `your_secret_key`  with your respective keys.



```properties
[default]
aws_access_key_id=your_access_key
aws_secret_access_key=your_secret_key

```

Now your access to Spaces via the AWS SDK will be authenticated, and we can move on to creating the application.
- ရထားတဲ့ Key နှစ်ခု ကို အသုံးပြုရမှာဖြစ်ပါတယ်
- user dir.. အောက်မှာ .aws ဆိုတဲ့ folder တစ်ခု လုပ်ပြီး **`credentials`** ဆိုတဲ့ file တစ်ခုကို အထဲမှာ လုပ်ထားခိုင်းပါတယ်
- အဲ့ဒီ ဖိုင်ထဲက Key နှစ်ခု ကို  ထည့်ရေးပေးပါလို့ ပြောထားတာပါ။
```properties
// terminal (git bash)

Admin@MSquare MINGW64 ~/Desktop
$ cd

Admin@MSquare MINGW64 ~
$ mkdir .aws && touch .aws/credentials

```
- user directory ထဲကို cd နဲ့ သွားပြီး .aws folder တစ်ခုလုပ် ၊ credentials ဖိုင်တစ်ခုလုပ်လိုက်တာပါ။
- credentials ဖိုင်ထဲမှာ အောက်က ကုဒ်တွေ ထည့်းပေးရမှာ ပါ။
```properties
[default]
aws_access_key_id=your_access_key
aws_secret_access_key=your_secret_key

```
##
## Install Node.js Dependencies

To begin, create a directory in which you would like to place your Node.js application and navigate to the directory. For this demonstration, we will create our project in  **`spaces-node-app`**  in the  **`sites`**  directory.

```
  mkdir sites/spaces-node-app && cd sites/spaces-node-app
```



Create a new  **`package.json`**  file for your project. Paste the code below into the file.

package.json

```
{
  "name": "spaces-node-app",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "license": "MIT"
}

```



This is a basic  `package.json`  file listing the name, version number, and license of our application. The  `scripts`  field will allow us to run a Node.js server by typing  `npm start`  instead of  `node server.js`.

We will install all of our dependencies with the  `npm install`  command, followed by the names of the four dependencies in our project.

```
npm install aws-sdk express multer multer-s3
```



After running this command, the  `package.json`  file should be updated. These dependencies will aid us in connecting to the DigitalOcean Spaces API, creating a web server, and handling file uploads.

-   [`aws-sdk`](https://www.npmjs.com/package/aws-sdk)  — AWS SDK for JavaScript will allow us to access S3 through a JavaScript API.
-   [`express`](https://www.npmjs.com/package/express)  — Express is a web framework that will allow us to quickly and efficiently set up a server.
-   [`multer`](https://www.npmjs.com/package/multer)  — Multer is middleware that will handle file uploads.
-   [`multer-s3`](https://www.npmjs.com/package/multer-s3)  — Multer S3 extends file uploads to S3 object storage, and in our case, DigitalOcean Spaces.

Now that we have our project location and dependencies set up, we can set up the server and front-end views.
- express project  တစ်ခု လုပ်ခိုင်းတာပြီး လိုအပ်တဲ့ module တွေကို install လုပ်ခိုင်းထားတာဖြစ်ပါတယ်။
- ကျနော်တို့ အရင်သင်ခန်းစာမှာ အကုန်လုပ်ထားပြီးဖြစ်လို့ မထည့်ထားရသေးတဲ့ `aws-sdk` နဲ့  `multer-s3` ကို ပဲ ထပ်ထည့်ပေးရမှာဖြစ်ပါတယ်။
- မိမိရဲ့ project folder ကို vs code မှာ ဖွင့်ပါ။
- terminal မှာ node module တွေကို install လုပ်ပေးရပါမယ်
 ```properties
npm install aws-sdk multer-s3@2.10.0
```
##
### Create the Front End of the Application ကို လုပ်ထားပြီးသားမလို့ ကျော်လိုက်ပါမယ်
##
## Set Up an Express Server Environment
- ဒီမှာလည်း express server လုပ်ထားပြီးသားမလို့ အသစ်ထည့်ထားတဲ့ aws-sdk နဲ့ multer-s3 ကို သာ requireလုပ်ပြီး ထပ်ထည့်လိုက်ပါမယ်
```js

const aws = require('aws-sdk');

const multerS3 = require('multer-s3');


```
##
## Upload a File to a Space with Multer

Now that we have our server environment up and running properly, the last step is to integrate the form with Multer and Multer S3 to make a file upload to Spaces.

You can use  `new aws.S3()`  to connect to the Amazon S3 client. For use with DigitalOcean Spaces, we’ll need to set a new endpoint to ensure it uploads to the correct location. At the time of writing,  `nyc3`  is the only region available for Spaces.

In  `server.js`, scroll back up to the top and paste the following code below the constant declarations.

server.js

```
...
const app = express();

// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint('nyc3.digitaloceanspaces.com');
const s3 = new aws.S3({
  endpoint: spacesEndpoint
});

```

Copy

Using the example from the  [multer-s3](https://www.npmjs.com/package/multer-s3)  documentation, we will create an  `upload`  function, setting the  `bucket`  property to your unique Space name. Setting  `acl`  to  `public-read`  will ensure our file is accessible to the public; leaving this blank will default to private, making the files inaccessible from the web.

server.js

```
...

// Change bucket property to your Space name
const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: 'your-space-here',
    acl: 'public-read',
    key: function (request, file, cb) {
      console.log(file);
      cb(null, file.originalname);
    }
  })
}).array('upload', 1);

```



The  `upload`  function is complete, and our last step is to connect the upload form with code to send the file through and route the user accordingly. Scroll to the bottom of  `server.js`, and paste this code right above the  `app.listen()`  method at the end of the file.

server.js

```
...
app.post('/upload', function (request, response, next) {
  upload(request, response, function (error) {
    if (error) {
      console.log(error);
      return response.redirect("/error");
    }
    console.log('File uploaded successfully.');
    response.redirect("/success");
  });
});

```



When the user clicks submit, a POST request goes through to  `/upload`. Node is listening for this POST, and calls the  `upload()`  function. If an error is found, the conditional statement will redirect the user to the  `/error`  page. If it went through successfully, the user will be redirected to the  `/success`  page, and the file will be uploaded to your Space.








Navigate to the root of the project, select a file, and submit the form. If everything was set up properly, you will be redirected to the success page, and a public file will be available on your DigitalOcean Space.
##
```
...
const app = express();

// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint('nyc3.digitaloceanspaces.com');
const s3 = new aws.S3({
  endpoint: spacesEndpoint
});

```
- server .js မှာ aws endpoint တစ်ခု လုပ်ခိုင်းတာဖြစ်ပါတယ်။
-  new aws.Endpoint('nyc3.digitaloceanspaces.com') မှာ ကျနော်တို့ သုံးမယ့် end point ကို အစားထိုးပေးရပါမယ်။
```js

const app = express();

// Set S3 endpoint to DigitalOcean Spaces
const spacesEndpoint = new aws.Endpoint('sgp1.digitaloceanspaces.com');
const s3 = new aws.S3({
  endpoint: spacesEndpoint
});

```
##
```
...

// Change bucket property to your Space name
const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: 'your-space-here',
    acl: 'public-read',
    key: function (request, file, cb) {
      console.log(file);
      cb(null, file.originalname);
    }
  })
}).array('upload', 1);

```
- multer storage တစ်ခု လုပ်ထားခိုင်းတာပါ။
- bucket မှာ ကျနော်တို့ သုံးမယ် msquarefdc ကို ပြင်ထည့်ပေးပါမယ်
- array('upload', 1) မှာလဲ formdata က file တွေသိမ်တဲ့ key ( "files" ) ကို ပြောင်းပေးရပါမယ်။
 ```js


// Change bucket property to your Space name
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
##
```
...
app.post('/upload', function (request, response, next) {
  upload(request, response, function (error) {
    if (error) {
      console.log(error);
      return response.redirect("/error");
    }
    console.log('File uploaded successfully.');
    response.redirect("/success");
  });
});

```
- server မှာ request ကို လက်ခံခိုင်းတာပါ။
- ကျနော်တို့ လုပ်လက်စ file upload project နဲ့ ကိုက်ညီအောင် အနည်းငယ် ပြင်ရေးပါမယ်။
```js

app.post('/cloudUpload', function (request, response, next) {
  upload(request, response, function (error) {
    if (error) {
      console.log(error);
      return response.send({message: "file upload error"});
    }
    console.log('File uploaded successfully.');
    response.send({message: "file upload successful"});
  });
});

```
- request လုပ်ရမယ့် route ကို /cloudUpload အနေနဲ့ ပြင်လိုက်ပြီး
- response ကိုလဲ object တစ်ခုသာ ပြန်ပို့လိုက်ပါတယ်။
### all code in server.js
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
      cb(null, file.originalname);
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

// const storage = multer.diskStorage({
//   destination: function (req, file, cb) {
//     cb(null, "uploads/");
//   },
//   filename: function (req, file, cb) {
//     cb(null, Date.now() + "-" + file.originalname); // 177343724-dog.jpg
//   },
// });

// const upload = multer({ storage });

// app.post("/upload", (req, res) => {
//   const fileStream = fs.createWriteStream(`image.jpg`);
//   req.pipe(fileStream);
//   res.send({ message: "Upload successful" });
// });

// app.post("/upload-multiple", upload.array("files"), (req, res) => {
//   res.send({ message: "files upload ok !" });
// });
app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
> မှတ်ချက် ။   ။ command လုပ်ထားတဲ့ code တွေက အရင်သင်ခန်းစာမှ code တွေ ဖြစ်ပါတယ်။

### နောက်ဆုံးအနေနဲ့ script.js မှာ request လုပ်တဲ့ route ကို sever မှာ လက်ခံထားတဲ့ route အဖြစ် ပြင်ပေးလိုက်ရင်တော့ file upload ကို စမ်းကြည့်လို့ရပါပြီး
```js
// script.js
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
- npm start လုပ်ပြီး ပုံတစ်ပုံ တင်စမ်းကြည့်ပါက console မှာ `{ message: "file upload successful" }` ပြပေးရင် file upload လုပ်တာ အောင်မြင်ပါပြီး။
