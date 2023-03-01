## MSquare Programing Fullstack Course
### Episode-*36* 
### Summary For `Room(1)` intermediate Class
## Build online booking App
###  Create new react app with typescript
- အရင်ဆုံး react app ဆစ်ခုကို typescript နဲ့ တည်ဆောက်ပါမယ်
- ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ လုပ်ထားတဲ့ frontend folder ကို ဖျက်လိုက်ပြီ react project ကို အသစ်ပြန်လုပ်ပါမယ်။
```properties
//terminal
Admin@MSquare MINGW64 ~/Desktop/ep31/fullstack (main)
$ npx create-react-app frontend --template typescript

```
- အသစ်လုပ်ထားတဲ့ frontend folder ထဲက src folder မှာရှိတဲ့ App.tsx ထဲက code တွေ ဖျက်ပြီး အသစ်ပြန်ရေးလိုက်ပါမယ်။
```js
//fullstack\frontend\src\App.tsx
import React from "react";
import logo from "./logo.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <h1>Online Booking App</h1>
    </div>
  );
}

export default App;

```
- npm start နဲ့ react app ကို run လိုက်တဲ့အခါ online Booking App ဆိုပြီး browser မှာ ပြပေးနေတာကို တွေ့ရမှာဖြစ်ပါတယ်။
- ဆက်လက်ပြီး DatePicker ဆိုတဲ့ component တစ်ခု လုပ်ပါမယ်
```properties
// terminal
Admin@MSquare MINGW64 ~/Desktop/ep31/fullstack/frontend (main)
$ cd src/

Admin@MSquare MINGW64 ~/Desktop/ep31/fullstack/frontend/src (main)
$ mkdir components

Admin@MSquare MINGW64 ~/Desktop/ep31/fullstack/frontend/src (main)
$ cd components/

Admin@MSquare MINGW64 ~/Desktop/ep31/fullstack/frontend/src/components (main)
$ touch DatePicker.tsx

```
- DatePicker.tsx ထဲမှာ ဘာမှ မရေးခင် လိုအပ်မယ့် node module  တွေ install လုပ်ပေးရပါမယ်။
##
## MUI 
- Tailwind , booststrap တွေကဲ့သို့ CSS framework တစ်ခုဖြစ်ပါတယ်
- လက်ရှိ project မှာ calander  တစ်ခု ထည့်သုံးမှာ မလို့ mui ကို သုံးပါမယ်
`npm install @mui/material @emotion/react @emotion/styled `
- calender ကို ပြပေးနိုင်ဖို့ လိုအပ်မယ့် component တွေကို ထပ် install လုပ်ပါမယ်။
``` properties
npm i @mui/x-date-pickers dayjs
```

- လိုအပ်တာတွေ ထည့်ပြီးပြီ ဆိုရင် DatePicker component မှာ calender တစ်ခု  လုပ်လိုက်ပြီး  DatePicker component ကို App.tsx မှာ ခေါ်သုံးလိုက်ပါမယ်။
- https://mui.com/x/react-date-pickers/getting-started/ မှာ ဖတ်ကြည့်ပြီး date picker တစ်ခု လုပ်မှာ ဖြစ်ပါတယ်
-  [Example-code](https://codesandbox.io/s/m76wln?file=/demo.tsx) တွေကို  DatePicker component မှာ copy/paste လုပ်လိုက်ပါမယ်
- ပြီးတော့ မလိုအပ်တဲ့ code တစ်ချို့ကို ဖျက်ထားလိုက်ပါတယ်.
```js
// fullstack\frontend\src\components\DatePicker.tsx
import * as React from "react";
import dayjs, { Dayjs } from "dayjs";
import Stack from "@mui/material/Stack";
import TextField from "@mui/material/TextField";
import { LocalizationProvider } from "@mui/x-date-pickers/LocalizationProvider";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { TimePicker } from "@mui/x-date-pickers/TimePicker";
import { DateTimePicker } from "@mui/x-date-pickers/DateTimePicker";
import { DesktopDatePicker } from "@mui/x-date-pickers/DesktopDatePicker";
import { MobileDatePicker } from "@mui/x-date-pickers/MobileDatePicker";

export default function DatePicker() {
  const [value, setValue] = React.useState<Dayjs | null>(
    dayjs("2014-08-18T21:11:54")
  );

  const handleChange = (newValue: Dayjs | null) => {
    setValue(newValue);
  };

  return (
    <div className="container">
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Date desktop"
            inputFormat="MM/DD/YYYY"
            value={value}
            onChange={handleChange}
            renderInput={(params) => <TextField {...params} />}
          />
        </Stack>
      </LocalizationProvider>
    </div>
  );
}

```
```js
// fullstack\frontend\src\App.tsx
import React from "react";
import logo from "./logo.svg";
import "./App.css";
import DatePicker from "./components/DatePicker";

function App() {
  return (
    <div className="App">
      <h1>Online Booking App</h1>
      <DatePicker />
    </div>
  );
}

export default App;
```
- အခုဆိုရင်  browser မှာ ဖွင့်ထားတဲ့ react app မှာ date picker တစ်ခု ကို ပြပေးနေမှာ ဖြစ်ပါတယ်။
