## MSquare Programing Fullstack Course
### Episode-*40* Summary for (group 2) 

ဒီနေ့သင်တန်းမှာတော့ <br>
### digital ocean space server ဆီ တင်လိုက်တဲ့ပုံကို UI မှာ ပြခြင်း
### Postman ကို အသုံးပြုပြီး digital ocean space server ဆီ request send ခြင်း


စတာတွေ လေ့လာသွားပါမယ်။
##
### အရင်ဆုံး ပုံတစ်ပုံကို digital ocean space(DOC)ဆီ တင်လိုက်ပါမယ်.
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/2ep401.png)

- တင်လိုက်တဲ့ ပုံ ကို UI မှာ ပြန်ပြဖို့အတွက် index.html မှာ img tag တစ်ခု လုပ်ပါမယ်
- img tag ရဲ့ src မှာ ခုလိုထည့်ပေးရပါမယ်။
```html
https://sgp1.digitaloceanspaces.com/msquarefdc/your-folder-name/your-uploaded-image
```
eg.. `https://sgp1.digitaloceanspaces.com/ msquarefdc/aung-myanmar/image.png`
- index.html မှာ image div တစ်ခုကို ထည့်ပါမယ်
```html
  <div>
     <img src="https://sgp1.digitaloceanspaces.com/msquarefdc/aung-myanmar/image.png" width="200px"/>
 </div>

```
- server ကို start လုပ်ပြီး laocalhost:3000 ကို သွားလိုက်တဲ့အခါ file input နဲ့အတူ မိမိတို့ တင်လိုက်တဲ့ပုံကို တွေ့ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/2ep402.png)

##
### Get content from DOC sapce api (using  POSTMAN)
- postman ကနေ DOC space api ကို get နဲ့ request လုပ်ကြည့်ပါမယ်
- request လုပ်ရမယ့် url က 
`{bucket-name}.{region}.digitaloceanspaces.com`  ဖြစ်ပါတယ်
- method က "GET" ဖြစ်ပါမယ်။
- request လုပ်ကြည့်တဲ့အခါ 


 ```xml
 <?xml version="1.0" encoding="UTF-8"?>
<Error>
    <Code>AccessDenied</Code>
    <BucketName>msquarefdc</BucketName>
    <RequestId>tx00000000000001a045584-006409942b-28e5bd98-sgp1b</RequestId>
    <HostId>28e5bd98-sgp1b-sgp1-zg02</HostId>
</Error>
```
ဆို ပြီး response လုပ်လာတာတွေ့ရမှာပါ။
- ဆိုလိုတဲ့ သဘောက ၀င်ခွင့်မရှိဘူး လို့ DOC space api က အကြောင်းပြန်လိုက်တာ ဖြစ်ပါတယ်။
- ၀င်ခွင့်ရဖို့အတွက် Authorization ( ၀င်ခွင့်ရှိသူဖြစ်ကြောင်း ) ဖြစ်တဲ့ အကြောင်း request လုပ်တဲ့ အခါ တစ်ပါတည်းထည့်ပေးရပါမယ်။
- ကျနော်တို့ ပုံတွေတင်တုန်းက သုံးခဲ့တဲ့ acss key ID နဲ့ SecretKey ကို အသုံးပြုရမှာဖြစ်ပါတယ်
1. Postman ရဲ့ request box ထဲက Authorization ထဲကို ၀င်ပါ။
2. Type ဘေးက မြားကို နှိပ်ပါ
3. AWS signature ကို ရွေးပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/2ep403.png)
- ပေါ်လာတဲ့ ဘေးက tab ထဲမှာ လိုအပ်မယ့် Authorization info တွေထည့်ပေးရပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/2ep404.png)
- ပုံပါ အတိုင်း ထည့်ပြီးပြီးဆိုရင် request send ကြည့်လိုက်ပါက postman response body မှာ xml format နဲ့ DOC space bucket မှာ တင်ထားတဲ့ ဖိုင်တွေကို ပြပေးနေတာ တွေ့ရမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/2ep405.png)
