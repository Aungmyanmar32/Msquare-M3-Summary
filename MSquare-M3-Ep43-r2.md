## MSquare Programing Fullstack Course
### Episode-*43* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>

###  digital ocean space server ဆီ ပုံတစ်ပုံ တင်ပြီးတာနဲ့ သူ့အထဲမှာ ရှိတဲ့ Contents တွေကို တစ်ခါတည်း ရယူပြီး UI မှာပြပေးတာ ဆက်လုပ်ပါမယ်

##
### ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ project အသစ်တစ်ခုလုပ်ပြီး DOC space ဆီ request လုပ်ကာ ရလာတဲ့ data ကိုclient မှာ log ထုတ်ကြည့်ခဲ့ပါတယ်
- ခု သင်ခန်းစာမှာတော့  DOC ဆီကို ပုံလဲတင် request လဲ လုပ်ပြီး ရလာတဲ့ data တွေကို ကိုယ်တင်လိုက်တဲ့ folder name နဲ့ filter စစ်ထုတ်ပြီး UI မှာထုတ်ပြနိုင်အောင် လေ့လာသွားကြပါမယ်။
##
- အရင်ဆုံး Upload ခလုတ်ကို နှိပ်လိုက်တဲ့အခါ file upload လုပ်နေကြောင်းကို ပြပေးနိုင်ဖို့  Upload ခလုတ်ထဲက text တွေကို အသေမထားပဲ အလုပ်လုပ်နေတဲ့ လုပ်ဆောင်ချက်အလိုက် ပြပေးအောင် လုပ်ပါမယ်။
- ဒါမှပဲ အသုံးပြုတွေက file upload လုပ်နေတာလား ပြီးသွားပြီလား စသည်ဖြင့် သိနိုင်မှာ ဖြစ်ပါတယ်။
-  script.js မှာ  Upload ခလုတ်ကို နှိပ်လိုက်တဲ့အခါ ဖမ်းထားတဲ့ function ကို သွားပါမယ်
```js
//script.js

const fileInput = document.getElementById("formFile");
const imgFileTag = document.querySelector(".imgFile")
const uploadBtn = document.querySelector(".uploadBtn")

const uploadFile = async () => {

//change button to loading
uploadBtn.innerHTML = `
<span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
Uploading...
`


  const filesList = fileInput.files;
  const fileArray = [...filesList];
  console.log(fileArray);

  const formData = new FormData();

  fileArray.forEach((file) => formData.append("files", file));

  const response = await fetch("http://localhost:3000/cloudUpload", {
    method: "POST",
    body: formData,
  });

  //change bottuon to upload
  uploadBtn.innerHTML ="Upload"


  const data = await response.json();
  console.log(data);
};

```
>ရှင်းလင်းချက်
>

    const uploadBtn = document.querySelector(".uploadBtn")
   - upload button ကို လှမ်းယူထားပါတယ်။

```js

uploadBtn.innerHTML = `
<span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
Uploading...
`
```
- upload လုပ်လိုက်တဲ့ အချိန်မှာ upload button ထဲက Upload ဆိုတဲ့ text အစား bootstrap spinner တစ်ခုနဲ့ Uploading...  ဆိုတဲ့ text ကို အစားထိုးပြပေးလိုက်တာပါ
```js
 const filesList = fileInput.files;
  const fileArray = [...filesList];
  console.log(fileArray);

  const formData = new FormData();

  fileArray.forEach((file) => formData.append("files", file));

  const response = await fetch("http://localhost:3000/cloudUpload", {
    method: "POST",
    body: formData,
  });

  //change bottuon to upload
  uploadBtn.innerHTML ="Upload"
```
- တင်လိုက်တဲ့ ဖိုင်ကို ဆာဗာဆီလှမ်းပို့ လိုက်ပြီး uplaod botton ကို မူလ text ဖြစ်တဲ့ Upload ကို ပြန်ထားပေးလိုက်တာဖြစ်ပါတယ်။
- ခု ပုံတစ်ပုံကို ရွေးပြီး upload လုပ်ကြည့်လိုက်ပါက upload လုပ်နေစဥ်အတွင်းspinner တစ်ခုနဲ့ Uploading...  ဆိုတဲ့ text ကို ခလုတ်မှာ ပြပေးနေမှာ ဖြစ်ပြီး upload ပြီးသွားပါက Upload ဆိုပြီး ပြန်ပြောင်းသွားမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep43r21.png)
##
### ဆက်ပြီးတော့ server က response ပြန်လာတဲ့ object ထဲက array ကို script.js မှာ filter လုပ်ပါမယ်
```js
//script.js

const fileInput = document.getElementById("formFile");
const imgFileTag = document.querySelector(".imgFile")
const uploadBtn = document.querySelector(".uploadBtn")

const uploadFile = async () => {
//change button to loading
uploadBtn.innerHTML = `
<span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
Uploading...
`


  const filesList = fileInput.files;
  const fileArray = [...filesList];
  console.log(fileArray);

  const formData = new FormData();

  fileArray.forEach((file) => formData.append("files", file));

  const response = await fetch("http://localhost:3000/cloudUpload", {
    method: "POST",
    body: formData,
  });

  //change bottuon to upload
  uploadBtn.innerHTML ="Upload"


  const data = await response.json();
  console.log(data);
  //{message: "file uploaded successful!",fileContents : [.......]}

  // filter Contents with folder-name
  const myFilesList = data.fileContents.filter(file => file.Key.includes("aung-myanmar"))
  console.log(myFilesList);

 
};

```
`
const myFilesList = data.fileContents.filter(file => file.Key.includes("aung-myanmar")) console.log(myFilesList);
`
- response ပြန်လာတဲ့ data ထဲက fileContents ကို ကျနော့ folder name ပါတဲ့ contents တွေကို ပဲ filter လုပ်ပြီး စစ်ထုတ်လိုက်ပါတယ်
- စစ်ထုတ်ပြီး ရလာတဲ့ array ကို log ထုတ်ကြည့်လိုက်တဲ့အခါ browser console မှာ အောက်ပါအတိုင်း ပြပေးနေမှာဖြစ်ပါတယ်။
```js
// console output

 (13) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]

1.  0: {Key:  'aung-myanmar/525861-dark-greenery.jpg',  LastModified:  '2023-03-17T18:27:11.330Z',  ETag:  '"8c599e1ef4a6d3a3e2c19b5f84b06853"',  Size:  90219,  StorageClass:  'STANDARD', …}
2.  1: {Key:  'aung-myanmar/582c5a4f767c8d1dc1ea2b24ca1755ed.jpg',  LastModified:  '2023-03-17T01:57:01.848Z',  ETag:  '"5ff2d27fef0cdf93af74eafd499e492b"',  Size:  784098,  StorageClass:  'STANDARD', …}
3.  2: {Key:  'aung-myanmar/digitaloce1.png',  LastModified:  '2023-03-07T05:49:12.527Z',  ETag:  '"8377de7048236fd57317079f580276ab"',  Size:  49522,  StorageClass:  'STANDARD', …}
4.  3: {Key:  'aung-myanmar/dodtoken.png',  LastModified:  '2023-03-07T06:20:35.444Z',  ETag:  '"4df7873392b96a161f94bb2ab863b11c"',  Size:  173993,  StorageClass:  'STANDARD', …}
5.  4: {Key:  'aung-myanmar/download.jpg',  LastModified:  '2023-03-16T13:36:31.673Z',  ETag:  '"a72050ce8d18c5e341ce539e923c77a0"',  Size:  5495,  StorageClass:  'STANDARD', …}
6.  5: {Key:  'aung-myanmar/ep43r21.png',  LastModified:  '2023-03-19T06:03:07.579Z',  ETag:  '"f38ae591ee9319e066d6bf60a248d95d"',  Size:  151615,  StorageClass:  'STANDARD', …}
7.  6: {Key:  'aung-myanmar/image.png',  LastModified:  '2023-03-09T06:57:10.528Z',  ETag:  '"145ea8f55a6b5d4f991ec70e6497ed55"',  Size:  134907,  StorageClass:  'STANDARD', …}
8.  7: {Key:  'aung-myanmar/images.jpg',  LastModified:  '2023-03-16T13:23:56.777Z',  ETag:  '"2dc9279e35b49c81287b845c919e92d1"',  Size:  13957,  StorageClass:  'STANDARD', …}
9.  8: {Key:  'ko-aung-myanmar/blackpink.jpeg',  LastModified:  '2023-03-18T03:28:38.727Z',  ETag:  '"05666c86946e8d3d7923c0e4444ae4be"',  Size:  37603,  StorageClass:  'STANDARD', …}
10.  9: {Key:  'ko-aung-myanmar/dog-kopi.jpg',  LastModified:  '2023-03-18T03:31:17.339Z',  ETag:  '"f42212e781ca68032ce257e5fea2f506"',  Size:  4190558,  StorageClass:  'STANDARD', …}
11.  10: {Key:  'ko-aung-myanmar/dog12345.jpg',  LastModified:  '2023-03-08T12:32:47.822Z',  ETag:  '"f42212e781ca68032ce257e5fea2f506"',  Size:  4190558,  StorageClass:  'STANDARD', …}
12.  11: {Key:  'ko-aung-myanmar/dog_test.jpg',  LastModified:  '2023-03-18T03:31:07.078Z',  ETag:  '"f42212e781ca68032ce257e5fea2f506"',  Size:  4190558,  StorageClass:  'STANDARD', …}
13.  12: {Key:  'ko-aung-myanmardog12345.jpg',  LastModified:  '2023-03-08T12:27:20.351Z',  ETag:  '"f42212e781ca68032ce257e5fea2f506"',  Size:  4190558,  StorageClass:  'STANDARD', …}
14.  length: 13
15.  [[Prototype]]: Array(0)
```
- filter လုပ်ပြီး ရလာတဲ့ myFilesList array ထဲက Key  ကို အသုံးပြုပြီး image တွေကို UI မှာ ပြပါမယ်။
```js
// script.js

const fileInput = document.getElementById("formFile");
const imgFileTag = document.querySelector(".imgFile")
const uploadBtn = document.querySelector(".uploadBtn")

const uploadFile = async () => {
//change button to loading
uploadBtn.innerHTML = `
<span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
Uploading...
`


  const filesList = fileInput.files;
  const fileArray = [...filesList];
  console.log(fileArray);

  const formData = new FormData();

  fileArray.forEach((file) => formData.append("files", file));

  const response = await fetch("http://localhost:3000/cloudUpload", {
    method: "POST",
    body: formData,
  });

  //change bottuon to upload
  uploadBtn.innerHTML ="Upload"


  const data = await response.json();
  console.log(data);
  //{message: "file uploaded successful!",fileContents : [.......]}

  // filter Contents with folder-name
  const myFilesList = data.fileContents.filter(file => file.Key.includes("aung-myanmar"))
  console.log(myFilesList);

  //Show all img in filtered array (myFilesList)
  for (let i = 0; i < myFilesList.length; i++) {
    const imgSrc = encodeURIComponent(myFilesList[i].Key)
    const fileDiv = document.createElement("div")
    fileDiv.innerHTML =`
    <img src="https://msquarefdc.sgp1.digitaloceanspaces.com/${imgSrc}" width="200px" class="p-2"/>
    `
    imgFileTag.append(fileDiv)
  }
};

```
```
  for (let i = 0; i < myFilesList.length; i++) {
    const imgSrc = encodeURIComponent(myFilesList[i].Key)
    const fileDiv = document.createElement("div")
    fileDiv.innerHTML =`
    <img src="https://msquarefdc.sgp1.digitaloceanspaces.com/${imgSrc}" width="200px" class="p-2"/>
    `
    imgFileTag.append(fileDiv)
  }
  ```
  - filter လုပ်ပြီး ရလာတဲ့ myFilesList array ကို loop လုပ်လိုက်တာပါ။
  - myFilesList arrayထဲက Key ကို url မှာ ထည့်ပြီး သုံးမှာမလို့ encode အရင်လုပ်လိုက်ပါတယ်။
  - div တစ်ခု လုပ်လိုက်ပြီး သူ့အထဲမှာ img tag တစ်ခု ထပ်လုပ်ပါတယ်
  - img ရဲ့ source ကို DOC space ရဲ့ url နဲ့ encode လုပ်ထားတဲ့ imgSrc နှစ်ခု ပေါင်းပြီး  ထည့်ပေးလိုက်ပါတယ်
  - fileDiv ကို html မှာ ပြမယ့် div ထဲ append လုပ်လိုက်ပါတယ်
  - ခု ပုံတစ်ပုံတင်ကြည့်လိုက်ပါက မိမိ folder နာမည်နဲ့ upload လုပ်ထားတဲ့ ပုံတွေကို အောက်မှာ ပြပေးမှာ ဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep43r22.png)
