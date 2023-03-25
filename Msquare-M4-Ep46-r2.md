## MSquare Programing Fullstack Course
### Episode-*46* 
### Summary For `Room(2)` 
##
### React 
- React ဆိုတာ UI တွေ ထည်ဆောက်တဲ့နေရာမှာ သုံးတဲ့ JavaScript library တစ်ခုဖြစ်ပါတယ် 
- Declarative အနေနဲ့ အသုံးပြုလို့ရပါတယ်
- React က **component base**  JavaScript library လည်း ဖြစ်ပါတယ်
- component မှာ class component  နှင့် functional component ဆိုပြီး နှစ်မျိုးရှိပါတယ်
-  functional component က stable ဖြစ်တဲ့အတွက် functional componentကိုပဲ အသုံးပြုပါမယ်
- React ထဲမှာ html ကော js ပါ တစ်ခါတည်း တွဲရေးလို့ပါတယ်။ **jsx**  လို့ ခေါ်ကြပါတယ်။
- React က page တစ်ခုထဲမှာပဲ  ပြချင်အရာတွေကို render လုပ်ပေးတာမလို့ SPA (single page application) လို့လဲ သတ်မှတ်ကြပါတယ်။
##
## Installation
### Create react project
- github repo တစ်ခုကို readme နဲ့ create လုပ်ပါ
- ထို repo ကို local ထဲ clone လိုက်ပါ.
- ရလာတဲ့ folder ထဲ မှာ react ကို ထည့်ပါမယ်
- ရလာတဲ့ folderကို vs cdoe မှာ ဖွင့်ထားပါ။
- new terminal ကို ဖွင်ပြီး 
```properties
npx create-react-app my-app
```
- ရိုက်ထည့်ပေးပါ
- my-app ဆိုတဲ့ နေရာမှာ မိမိစိတ်ကြိုက် project နာမည် ထည့်လို့ရပါတယ်
- အချိန်အနည်းငယ် စောင့်ပြီးပါက react ကို ထည့်လို့ပြီးပါပြီး။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/react1.png)
- react ကို browser ပေါ်မှာ ဖွင့်ရန်အတွက်  my-app folder ထဲ  သွားပါမယ်
```properties
cd my-app
```
- npm start ကို ထည့်ပြီး enter ခေါက်ပေးလိုက်ပါ။
```properties
npm start
```
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/react2.png)
- browser က auto ပွင့်လာပြီး react logo ပြပေးနေပါက react project တစ်ခု စတင်တာ ပြီးပါပြီး။
##
## File structure
### react project တစ်ခု တည်ဆောက်လိုက်တာနဲ့ project folder  ထဲမှာ react ကနေ File structure တစ်ခါတည်း တည်ဆောက်ပေးလိုက်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/react3.png)

### public  folder ထဲမှာ icon တစ်ခုရယ်၊ react logo ပုံ နှစ်ခုရယ်၊txt ဖိုင်တစ်ခုရယ်၊ index.html ဖိုင် စတာတွေပါ ပါတယ်။
- vanilla javascript နဲ့ html ကို အသုံးပြုပြီး website တွေ လုပ်တဲ့အခါ page တွေကို html  file တွေ တစ်ခုချင်းဆီ ရေးပေးရလေ့ရှိပါတယ်။
- react က SPA ဖြစ်တာမလို့ html file တစ်ခုထဲမှာပဲ လိုအပ်တဲ့ page တွေကို render လုပ်ပေးနိုင်ပါတယ်။
- inedx.html  ထဲမှာ id root ပေးထားတဲ့ div တစ်ခုပဲ ရှိတာကို မြင်ရမှာပါ။
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
   
    <title>React App</title>
  </head>
  
  <body>
    <div id="root"></div>
  </body>
  
</html>
```
##
### render *react app* in *html*
- src folder ထဲက index.js ကို ၀င်ကြည့်ပါမယ်။
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```
- React နဲ့ ReactDOM ကို react မှ import လှမ်းယူထားပါတယ်။
- index.css နဲ့ App component ကို src folder ထဲမှ လှမ်းယူထားပါတယ်။
- reportWebVitals.js  ကို src folder ထဲမှ လှမ်းယူထားပါတယ်။

`const root = ReactDOM.createRoot(document.getElementById('root'));`
- ReactDOM နဲ့ root တစ်ခု create လုပ်ပြီး index.html ထဲက id root ပေးထားတဲ့ div ကို ခေါ်ပြီး ထည့်ထားပေးပါတယ်။
```
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
- root ထဲမှာ JSX ကို သုံးပြီး App ကို render  လုပ်ပေးထားပါတယ်
-  App.js ထဲမှာ ရေးထားတာတွေကို index.html ထဲက id root ပေးထားတဲ့ div ထဲမှာ သွားပြခိုင်းထားလို့ မှတ်ယူလို့ရပါတယ်။
##
### App.js
```js
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```
- logo ပုံ နဲ့ App.css ကို import လုပ်ထားပြီး App ဆိုတဲ့ function တစ်ခု တည်ဆောက်ထားပါတယ်
- အောက်ဆုံးမှာတော့ ထို App function ( App component) ကို အခြားနေရာက ခေါ်သုံးလို့ရအောင် export လုပ်ထားပါတယ်။
- App function ထဲမှာတော့ div တစ်ခု return ပြန်ထားပါတယ်
- react component တစ်ခုမှာ return က တစ်ခုပဲ  လုပ်ပေးလို့ရမှာဖြစ်ပါတယ်
- ဆိုလိုတဲ့ သဘောက html element   တွေ အများကြီး return လုပ်ချင်တယ်ဆိုရင် div တစ်ခုထဲမှာ ဖြစ်ဖြစ် section တစ်ခုထဲမှာ ဖြစ်ဖြစ် အကုန်စုထည့်ပြီး return တစ်ခုပဲ ဖြစ်အောင် လုပ်ပေးရမှာဖြစ်ပါတယ်
- ဒါကို warp လုပ်တယ်လို့လဲ ခေါ်ကြပါတယ်။
##
### Component
- react  ဟာ  component-based ဖြစ်တယ်ဆိုတာ အထက်မှာ ပြောခဲ့ပါတယ်။
- ဒီသင်ခန်းစာမှာတော့  functional component ကို အသုံးပြုပါမယ်။
-  react component ဆိုတာ react app မှာ ပါ၀င်တဲ့ လုပ်ဆောင်ချက်တွေကို တစ်ခုချင်းစီ သက်သက် လုပ်ထားပြီး လိုအပ်တဲ့အခါမှ ခေါ်ယူအသုံးပြုနိုင်အောင် ဖန်တီးထားတာလို့ အကြမ်းဖျင်း မှတ်ယူနိုင်ပါတယ်။

- - ဥပမာ ။   ။ အထက်မှာ ရှင်းပြခဲ့သလို App,js မှာ App component ကို export လုပ်ထားတဲ့အတွက်
index.js  က ယူသုံးပြီး index.html မှာ ပြပေးသလိုမျိုးပါ။
- component တစ်ခုကို ယူသုံးချင်ရင်  import အရင်လုပ်ပေးရမှာဖြစ်ပြီး အသုံးပြုတဲ့အခါ JSXနဲ့ ပြန်ခေါ်သုံးရမှာဖြစ်ပါတယ်။
- component Name တွေရဲ့ အစ စာလုံးကို အကြီးနဲ့ ပေးလေ့ရှိပါတယ်။
### syntax
`import component-name from 'componenet-file-location';`
`<component-name />`

### example

    import App from './App.js';
    
    function test(){
     return (
       <div>
        <App />
       </div>
      )
     }
- component တွေ တည်ဆောက်ဖို့အတွက် src folder အောက်မှာ  components folder တစ်ခု တည်ဆောက်ပေးပါ။
- ထို component folder အောက်မှာ User.js file တစ်ခု လုပ်ပေးပါ။
- User.js ဖိုင်မှာ  User component တစ်ခု တည်ဆောက်ပါမယ်။
```jsx
const User = () => {
  return <h1>Hello from User component</h1>;
};

export default User;
```
- User  ဆိုတဲ့ function တစ်ခု လုပ်ထားပြီး head tag    တစ်ခု return လုပ်ထားပါတယ်
- User component ကို export လုပ်ထားပါတယ်
- ထို User component ကို App component အထဲမှာ ခေါ်သုံးကြည့်ပါမယ်။
- app.js  ထဲ ရှိသမျှ အကုန်ဖျက်လိုက်ပြီး အောက်က ကုဒ်တွေ ထည့်ပေးလိုက်ပါ။
### App.js
```jsx
import  User  from  "./components/User";

function  App() {
 return  <User  />;
}

export  default  App;
```
 - User component ကို components/User ကနေ import လုပ်ထားပြီး App function ထဲမှာ User component ကို  ခေါ်သုံးကာ return လုပ်ထားပါတယ်။
 - ပြီးတော့ App component ကို export လုပ်လိုက်ပါတယ်။
 - ခု npm start လုပ်လိုက်တဲ့အချိန်မှာတော့ User,js ထဲမှာ return  လုပ်ထားတဲ့ head tag ကို ပြပေးမှာဖြစ်ပါတယ်။
 
 ![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/react4.png)
 ##
 ### props
 - component တစ်ခုကို ခေါ်သုံးတဲ့ အခါ data တွေ ပို့ပေးချင်ရင် props တွေ ထဲ ထည့်ပြီးပို့လေ့ရှိပါတယ်
 - -
 ## နမူနာ
 ### App.js
```jsx
import User from "./components/User";

function App() {
  return <User userName="user1" email="user1@gmial.com" />;
}

export default App;
```
- User component ကို ခေါ်သုံးလိုက်တဲ့အခါ userName နဲ့ email ဆိုတဲ့ props နှစ်ခု ထည့်ပြီး ခေါ်ထားပါတယ်။
- ထို props တွေကို User component  ထဲက function မှာ parameter အဖြစ်လက်ခံပြီး အသုံးပြုလို့ ရပါတယ်။
### User.js
```jsx
const User = (props) => {
  return (
    <div>
      <h1>User name is {props.userName}</h1>
      <h1>email is {props.email}</h1>
    </div>
  );
};

export default User;
```
- အခြား component မှာ User component ကို props  တွေ ထည့်ပြီး ခေါ်သုံးထာတာမလို့  ထို props တွေကို parameter အဖြစ် လက်ခံလိုက်တာပါ။
- props က object အနေနဲ့ ၀င်လာတာမလို့ username နဲ့ email ကို လှမ်းယူ အသုံးပြုလိုက်တာဖြစ်ပါတယ်
- JSX မှာ javascript ကို သုံးချင်ရင် { } ထဲ ထည့်ရေးပေးရပါမယ်
- ဖိုင်ကို save  လိုက်တာနဲ့ browser မှာ ခုလိုပြပေးနေမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-fullstack-m2/main/react5.png)
### Props ကို လက်ခံတဲ့ အခါ တစ်ခါတည်း Destructure လုပ်ပြီး လက်ခံလို့ရပါတယ်။
```jsx
//User.jsx
const User = ({userName,email}) => {
  return (
    <div>
      <h1>User name is {userName}</h1>
      <h1>email is {email}</h1>
    </div>
  );
};

export default User;
```
- ဒီလိုဆိုရင်လဲ ခနကလိုပဲ result ကို react app မှာပြပေးနေတာ မြင်ရမှာပါ။ 
