## MSquare Programing Fullstack Course

### Episode-35

### Summary For  `Room(1)`  intermediate Class

##
### React todo list app ( setup )
- အရင်ဆုံး react project ထဲမှာ bootstrap ကို install လုပ်ပေးပါ။
```properties
Aungmyanr@MSquare MINGW64 ~/Desktop/ep31/fullstack/frontend (main)
$ npm i bootstrap
```
- react မှာ bootstrap ကို အသုံးပြုနိုင်ရန် import လုပ်ပေးရပါမယ်
```js
import  "bootstrap/dist/css/bootstrap.min.css";

import  "bootstrap/dist/js/bootstrap.bundle.min";
```
- bootstrap input တစ်ခုကို App.js ထဲ မှာ လုပ်ပါမယ်
```js
import "./App.css";
import User from "./components/User";
import config from "./config";
import { useEffect, useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.bundle.min";

function App() {
  

  return (
    <div className="App container bg-dark text-white">
     
      <div className="p-3">
        <input
          type="text"
          className="form-control w-50 m-auto"
          placeholder="Todo"
          onKeyUp={handleKeyUp}
        />
        <div className="">press Enter to Add</div>
      </div>

    </div>
  );
}

export default App;
```
- App.css ထဲမှာလဲ App div ကို height 100vh ပေးလိုက်ပါမယ်။
```css
.App {
 text-align:center;
 height:100vh;
}
```
- npm start နဲ့ react app ကို run လိုက်တဲ့အခါ ခုလိုပြပေးနေမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/retodo1.png)
> မှတ်ချက် ။   ။
> styling ကို မိမိစိတ်ကြိုက် လုပ်လို့ရပါတယ်။ ခု က bootstrap နဲ့ နမူနာ လုပ်ပြခြင်းသာ။
> react မှာ **html class attribute တွေ ထည့်ချင်ရင် className attribute ကို အသုံးပြုရ**တာကို သတိပြုပါ။
##
### Get value from input and using useState hook
- ဆက်လက်ပြီး todo app အတွက် setup လုပ်ကြရအောင်
- App.js မှာ useState hook ကို သတ်မှတ်ပေးပါမယ်
```js
const [todos, setTodo] = useState([]);
```
- initialstate ရဲ့ တန်ဖိုးကို empty array တစ်ခု အနေနဲ့ သတ်မှတ်ထားလိုက်ပါတယ်
- ဆိုလိုတဲ့ သဘောက `todos` ဟာ array တစ်ခု ဖြစ်ပါတယ်လို့ လုပ်လိုက်တာဖြစ်ပါတယ်
- retrun လုပ်ထားတဲ့ input tag မှာ keyup event ဖမ်းပြီး handleKeyUp function ကို သတ်မှတ်ပါမယ်
```js

function App() {
 const [todos, setTodo] = useState([]);

 const handleKeyUp = (e) => {
    if (e.key === "Enter") {
      let inputText = e.target.value;
      setTodo([...todos, inputText]);
      e.target.value = "";
    }
  };

  return (
    <div className="App container bg-dark">
      <div className="p-3">
        <input
          type="text"
          className="form-control w-50 m-auto"
          placeholder="Todo"
          onKeyUp={handleKeyUp}
        />

        <div className="">press Enter to Add</div>
      </div>
    </div>
  );
}

export default App;
```
> code explain
```js
 const handleKeyUp = (e) => {
    if (e.key === "Enter") {
      let inputText = e.target.value;
      setTodo([...todos, inputText]);
      e.target.value = "";
    }
  };
```
- ဖမ်းထားတဲ့  event မှာ enter ခေါက်လိုက်တယ်ဆိုရင် အထဲက code တွေ run ခိုင်းထားပါတယ်။
`let inputText = e.target.value;`
- enter ခေါက်လိုက်ချိန်မှာ input tag ထဲက value တွေ လှမ်းယူလိုက်ပါတယ်
` setTodo([...todos, inputText]);`
- useState ရဲ့ set function ( setTodo) ကို သုံးပြီး initialstate ရဲ့ တန်ဖိုးကို copy လုပ်၊ inputText ကို ထပ်ထည့်ပေးလိုက်ကာ todos array ကို update လုပ်ပေးလိုက်တာဖြစ်ပါတယ်။
`e.target.value = ""`
- နောက်ဆုံးမှာတော့ input tag ရဲ့ value ကို empty လုပ်လိုက်တာဖြစ်ပါတယ်
##
### နောက်တစ်ဆင့်အနေနဲ့ ရိုက်ထည့်ပေးလိုက်တဲ့ text တွေကို todo list အနေနဲ့ UI မှာ ပြကြည့်ပါမယ်။
- App.js ထဲက return လုပ်တဲ့ div  ထဲမှာ နောက် div တစ်ခု ထပ်ထည့်ပါမယ်
```js
 <div>
  {todos.map((todo) => {
  return (
     <h4 className="border-bottom w-50 m-auto p-2" key={todo}> {todo} </h4>
      );
      })
      }
</div>
```
- useState ထဲက todos array ကို map လုပ်လိုက်ပါတယ်
- ရလာတဲ့ array အသစ်ထဲက todo item တစ်ခုချင်းစီကို h4 tag ထဲမှာ ထည့်ပေးလိုက်တာဖြစ်ပါတယ်။
- ခု  react app ကို start လုပ်ပြီး input tag ထဲမှာ test ဆိုပြီး ရိုက်ထည့်ပြီး enter ခေါက်ကြည့်လိုက်ပါက အောက်မှာ todo list အနေနဲ့ test ဆိုပြီးလာပေါ်နေမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/retodo2.png)
##
## useRef hook (မိတ်ဆက်)
### #Does Not Cause Re-renders
- useRef hook ကို သုံးတဲ့အခါ react မှာ render ထပ်လုပ်ပေးခြင်းမရှိပါဘူး
- useState ကို သုံးပြီး state တစ်ခါ update ဖြစ်တိုင်း re-render လုပ်ပေးနေတာကို re-render မဖြစ်စေလိုတဲ့အခါuseRefကို သုံးလေ့ရှိပါတယ်။
### # Accessing DOM Elements
- react မှာ useRef hook ကိုသုံးပြီး `ref` attribute နဲ့ reference လုပ်ကာ DOM ထဲက element တွေကို ခေါ်ယူသုံးလို့ရပါတယ်။
### # Tracking State Changes
- state ပြောင်းလဲမှုတွေကိုလဲ useRef နဲ့ track လုပ်လို့ရပါတယ်။
- ဆိုလိုတာက state တစ်ခု update  မဖြစ်ခင်က previous state values ကို useRef နဲ့ track လုပ်နိုင်တယ်တာ ဖြစ်ပါတယ်။

## [Read more about of useRef hook with example](https://www.w3schools.com/react/react_useref.asp)
