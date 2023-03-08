## MSquare Programing Fullstack Course
### Episode-*38* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part3)
### 1. join components with *Props*
- ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ date တစ်ခု ရွေးလိုက်ရင် server ဆီ request လုပ်လိုက်ပြီး ပြန်လာတဲ့ response ကို log ထုတ်ကြည့်ထားပါတယ်
- အခု အဲ့ဒီ ရလာတဲ့ response ထဲက data ကို တခြား component တစ်ခု ဆီ ပို့ကြပါမယ်။
- အရင်ဆုံး componets folder အောက်မှာ Timepicker folder တစ်ခုဆောက်ပြီး အထဲမှာ Timepicker.tsx နဲ့ Timepicker.css ဖိုင်နှစ်ခု လုပ်ပါမယ်
 ```console
 cd src/components/
```
 ```console
 mkdir TimePicker && cd TimePicker && touch TimePicker.tsx Timepicker.css
```
- Timepicker.tsx မှာ  react functional component တစ်ခု လုပ်ပါမယ်။
- ပြီးရင် Timepicker.css ကို import လုပ်ပါမယ်
- ထပ်ပြီးတော့ mui radio group တစ်ခု ထည့်လိုက်ပါမယ်။
```js
// TimePicker.tsx

import React from "react";
import "./Timepicker.css";
import {
  FormControl,
  FormLabel,
  RadioGroup,
  FormControlLabel,
  Radio,
} from "@mui/material";

export default function TimePicker() {
  return (
    <div className="container">
      <FormControl>
        <FormLabel id="demo-radio-buttons-group-label">Gender</FormLabel>
        <RadioGroup
          aria-labelledby="demo-radio-buttons-group-label"
          defaultValue="female"
          name="radio-buttons-group"
        >
          <FormControlLabel value="female" control={<Radio />} label="Female" />
          <FormControlLabel value="male" control={<Radio />} label="Male" />
          <FormControlLabel value="other" control={<Radio />} label="Other" />
        </RadioGroup>
      </FormControl>
    </div>
  );
}

```
- TimePicker component ကို App component ထဲ ခေါ်သုံးပါမယ်
```js
// App.tsx
import React from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker from "./components/TimePicker/TimePicker";

function App() {
  return (
    <div className="App">
      <DatePicker />
      <TimePicker />
    </div>
  );
}

export default App;

```
- အခုဆိုရင် react app ( localhost:3000) မှာ သွားကြည့်လိုက်ရင် date picker တစ်ခုနဲ့ radio group တစ်ခု ကို ပြပေးနေတာတွေ့ရမှာပါ။
-  radio group က itemတစ်ခုကို select လုပ်လိုက်တဲ့အခါ alert တစ်ခု ပြနိုင်အောင် လုပ်ပေးကြည့်ပါ
- radio group မှာ server ကနေ response ပြန်လာတဲ့ slot array ထဲက time တွေ ပြပေးနိုင်အောင် Pros ကို သုံးပြီးလုပ်ကြည့်ကြပါ။
