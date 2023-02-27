## MSquare Programing Fullstack Course
### Episode-*36* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>
### single file upload
### formdata
### multer
အကြောင်း လေ့လာသွားပါမယ်။
##
### ပြီးခဲ့တဲ့ သင်ခန်းစာမှာတော့ file upload အတွက် ပြင်ဆင်ပြီး server ဆီ file နဲ့အတူ request လှမ်းပို့ခဲ့ပြီးပါပြီ
- ခု သင်ခန်းစာမှာတော့ request နဲ့ အတူ ပါလာတဲ့ file ကို ဆာဗာမှာ လက်ခံပြီး သိမ်းလို့ရအောင် လေ့လာကြပါမယ်။
```js
// server.js
const express = require("express");
const fs = require("fs");
const app = express();
const port = 3000;

app.use(express.static("public"));

app.post("/upload", (req, res) => {
  const fileStream = fs.createWriteStream("image.jpg");
  req.pipe(fileStream);
  res.send({ message: "Upload successful" });
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
> ရှင်းလင်းချက်

    app.post("/upload", (req, res) => {
      const fileStream = fs.createWriteStream("image.jpg");
      req.pipe(fileStream);
      res.send({ message: "Upload successful" });
    });
- အရင် သင်ခန်းစာတွေတုန်းက request ပို့လိုက်တဲ့ data တွေကို variable တစ်ခု အသစ်ဆောက်/ res.on တွေ chunk တွေ လုပ်ပြီး ယူခဲ့ကြတာ မှတ်မိမယ် ထင်ပါတယ်။
- အပေါ်က ကုဒ်တွေကလဲ ထိုနည်းတူစွာပါပဲ။
- writeStream ဆိုတဲ့ variable ထဲမှာ request က ပို့လိုက်တဲ့ data တွေကို file တစ်ခု write လုပ်ပြီး သိမ်းလိုက်တာဖြစ်ပါတယ်
- ထို writeStream ဆိုတဲ့ variable ကို req.pipe() သုံးပြီး ဆာဗာမှာ image.jpg ဆိုပြီးသိမ်းလိုက်တာပါ။
- ခု ဆာဗာ ကို စတင်လိုက်ပြီး ပုံတစ်ပုံ upload လုပ်ကြည့်ပါက image.jpg  ဖိုင်တစ်ခု project folder အောက်မှာ ပေါ်လာတာကို တွေ့ရမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep3621.png)
- upload လုပ်လိုက်တဲ့ ပုံက တခြား မည်သည့်နာမည် ဖြစ်ဖြစ် serverမှာ သတ်မှတ်ပေးထားတဲ့ အတိုင်း image.jpg ဆိုပြီး သိမ်းလိုက်တာကို သတိပြုပါ။
- ဆာဗာမှာ image.jpg ဆိုပြီး သိမ်းတာမလို့ file upload လုပ်တဲ့အခါ mp4 ဖိုင် pdf ဖိုင် အမျိုးအစား စတဲ့ image မဟုတ်တဲ့ file တစ်ခုခု တင်စမ်းကြည့်ပါက ဆာဗာမှာ သိမ်းလို့ရသော်လည်း ပြန်ဖွင့်ကြည့်ပါက image ဖိုင်တွေလို မပြပေးပဲ error  ဖြစ်တာကို မြင်ရမှာဖြစ်ပါတယ်။ 
- upload လုပ်လိုက်တဲ့ ဖိုင် အမျိုးအစားနဲ့ server မှာ လက်ခံပြီး သိမ်းလိုက်တဲ့ ဖိုင်အမျိုးအစား မတူတာကြောင့် error ဖြစ်ရတာပါ။
- နောက်ပြီး file input  မှာ multiple ကို သုံးပြီး image သုံးလေးခု တင်ကြည့်ပါက အထက်ပါ error ကဲ့သို့ ပြနေတာကို မြင်ရမှာဖြစ်ပါတယ်။
- ထို error တွေကို ဖြေရှင်းရန် server ဆီ request ပို့တဲ့ အခါ formdata ဆိုတဲ့ method ကို အသုံးပြုနိုင်ပါတယ်။
- server မှာ လက်ခံယူပြီး သိမ်းတဲ့အခါမှာလည်း *`multer`* ဆိုတဲ့ node module တစ်ခုကို အသုံးပြုပြီး သိမ်းလို့ရပါတယ်
##
### Formdata method
- formdata ဆိုတာ JS မှာ နဂိုပါလာတဲ့ method တစ်ခုဖြစ်ပါတယ်
- သူ့ကို အသုံးပြုနိုင်ရန် အရင်ဆုံး formdata အသစ်တစ်ခုတည်ဆောက်ပေးရပါတယ်။
`const files = new FormData()`
- တည်ဆောက်ထားတဲ့ formdata ထဲ data တွေ ထည့်ချင်ရင် append ကို အသုံးပြုရပါမယ်
- formdata   ထဲက data value ကိုလိုချင်ရင်  get ကို သုံးပေးရပါမယ်။
#### syntax
`formData.append( "key", "value" )` <br>
`formData.get(data-key)`
- example
```js
// test this code in console
const files = new FormData()
files.append("fruit","apple")
files.get("fruit")

// output : "apple"
```
- formdata  တစ်ခု လုပ်လိုက်ပြီး fruit ဆိုတဲ့ key မှာ apple ဆိုတဲ့ value တစ်ခုကို သိမ်းထားလိုက်တာဖြစ်ပါတယ်။
- apple ကို လိုချင်ရင်တော့ သိမ်းထားတဲ့ key ကို get နဲ့ ခေါ်ပေးရမှာဖြစ်ပါတယ်။
- --
- နောက်ထပ် orange ဆိုတဲ့ value တစ်ထပ်ထည့်ကြည့်ပါမယ်။
`files.append("fruit","orange")`
- ဒီတစ်ခါ orange ကို လိုချင်ရင်တော့ `files.get("fruit")` ဆိုပြီး ယူလို့မရတော့ပါဘူး
- formdata ထဲက key တူတဲ့ value တွေကို လိုချင်ရင် getAll ကို အသုံးပြုရပါမယ်။
```js
files.getAll("fruit")
//output : (2) ['apple', 'orange']
```
- getAll နဲ့ယူတဲ့အခါ  file list ( array ) ပုံစံနဲ့ ရလာမလို့ " orange" ကို လိုချင်ရင် index နဲ့ ယူလို့ရပြီး ဖြစ်ပါတယ်။
```js
files.getAll("fruit")[1]
// output: 'orange'
```
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/ep3622.png)
