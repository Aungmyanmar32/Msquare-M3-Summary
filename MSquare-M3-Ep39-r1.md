## MSquare Programing Fullstack Course
### Episode-*39* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part4)
### send data as Props and type this Props
##
- ဆာဗာက data တွေကို props အနေ့နဲ့ မပို့ခင်မှာ နမူနာ array တစ်ခုနဲ့ type အရင်လုပ်ကြည့်ပါမယ်။
- App.tsx မှာ ဆာဗာက လာမယ့် array ပုံစံအတိုင်း နမူနာ array တစ်ခု လုပ်ပါမယ်
- အဲ့ဒီ နမူနာ array ကို props အနေနဲ့ Timepicker componenet ဆီ ပို့လိုက်ပါမယ်
```js
// App.tsx

import React from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker from "./components/TimePicker/TimePicker";

function App() {
    const slots = [
    { time: "09:00", total: 100, booked: 80, availableSlot: 20 },
    { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
    { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
    { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
    { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
  ];

  return (
    <div className="App">
      <DatePicker />
      <TimePicker slots={slots} />
    </div>
  );
}

```
- slot array တစ်ခု လုပ်ထားပြီး TimePicker componentဆီ props အနေ့နဲ့ ထည့်ပေးလိုက်ပါတယ်။
-  လောလောဆယ်တော့ error ပြနေပါလိမ့်မယ်
- ဘာလို့လဲ ဆိုရင် TimePicker componentမှာ props ကို လက်မခံရသေးတဲ့အပြင် props အနေနဲ့ ၀င်လာမယ့် slot array ကို type မလုပ်ရသေးလို့ ဖြစ်ပါတယ်။
- ဒါကြောင့်မလို့  TimePicker componentမှာ props ကို လက်ခံပြီး  props အနေနဲ့ ၀င်လာမယ့် slot array ကို type လုပ်ပေးပါမယ်။
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

// define type of Props
interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}
interface Props {
  slots: Slot[];
}

//recive props from parent component and type this as Props interface
export default function TimePicker({ slots }: Props) {
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
- ခုဆိုရင် type သတ်မှတ်ပြီးပြီမလို့ error တွေပျောက်သွားပါမယ်။
- ဆက်လက်ပြီး props အနေနဲ့ ၀င်လာတဲ့ slot array ကို map လုပ်ပြီး radio group မှာ ပြကြည့်ပါမယ်။
```js
// Timepicker.tsx
import React from "react";
import "./Timepicker.css";
import {
  FormControl,
  FormLabel,
  RadioGroup,
  FormControlLabel,
  Radio,
} from "@mui/material";

interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}
interface Props {
  slots: Slot[];
}
export default function TimePicker({ slots }: Props) {
  return (
    <div className="container">
      <FormControl>
        <FormLabel id="demo-radio-buttons-group-label">Choose Time</FormLabel>
        <RadioGroup
          aria-labelledby="demo-radio-buttons-group-label"
          name="radio-buttons-group"
        >
{/* mapping slots array and show time */}
          {slots.map((slot) => {
            return (
              <FormControlLabel value={slot.time} control={<Radio />} label={slot.time}/>
            );
          })}
        </RadioGroup>
      </FormControl>
    </div>
  );
}

```
- အခု ဆိုရင် reacr app ( localhost:3000) မှာ radio group နဲ့ time တွေ ပြပေးနေတာကို တွေ့ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/mmpass1.png)

##
### fetch data from server 
- ခု နမူနာ array နဲ့ မလုပ်တော့ပဲ serverက လာမယ့် data (slots arry) ကို အသုံးပြုပါမယ်။
- အရင်နေ့ သင်ခန်းစာမှာ server က data တွေကို DatePicker component မှာ fetch လုပ်ခဲ့ပါတယ်။
- ခု အဲ့ဒီ fetch လုပ်တဲ့ function ကို  DatePicker component ကို ထိန်းထားတဲ့ parent ဖြစ်တဲ့ App.tsx မှာ ပြန်သတ်မှတ်ပါမယ်။
-  DatePicker component ကို ခေါ်တဲ့အခါမှာလည်း props နှစ်ခုထည့်ပေးလိုက်ပါတယ်
- TimePicker component ကို ခန ပိတ်ထားလိုက်ပါမယ်
```js
// App.tsx
import React from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";

function App() {
  const [value, setValue] = React.useState<Dayjs | null>(dayjs());

  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");
    const url = `http://localhost:5000/available?date=${choosenDate}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };

 
  return (
    <div className="App">
      <DatePicker value={value} hnadleDateChange={setValue} />
      {/* <TimePicker slots={slots} /> */}
    </div>
  );
}

export default App;

```
- useState ထဲ value တန်ဖိုး နဲ့  setValue function ကို props အနေနဲ့ DatePicker ဆီ ပို့လိုက်တာဖြစ်ပါတယ်
- DatePicker မှာ Props တွေ လက်ခံပြီး type လုပ်ပါမယ်
- ပြီးရင် on change event မှာ App.tsx က ထည့်ပေးလိုက်တဲ့ setValue function( handleDateChange) ကို ခေါ်ပေးလိုက်ပါမယ်။
- DatePicker မှာ တစ်ခုခုပြောင်းလိုက်တာနဲ့ App component မှာ value ရဲ့ state က update ဖြစ်ပြီး render တစ်ခါပြန်လုပ်ပေးမှာဖြစ်ပါတယ်။
```js
// DatePicker.tsx
import * as React from "react";
import dayjs, { Dayjs } from "dayjs";
import Stack from "@mui/material/Stack";
import TextField from "@mui/material/TextField";
import { LocalizationProvider } from "@mui/x-date-pickers/LocalizationProvider";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { DesktopDatePicker } from "@mui/x-date-pickers/DesktopDatePicker";

// define Props type
interface Props {
  value: Dayjs | null;
  handleDateChange: (value: Dayjs | null) => void;
}

export default function DatePicker({ value, handleDateChange }: Props) {
  return (
    <div className="container">
      <h2>Choose available Date</h2>
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Choose Date"
            inputFormat="DD/MM/YYYY"
            value={value}//use first prop
            onChange={(value) => handleDateChange(value)}//use second prop
            renderInput={(params) => <TextField {...params} />}
          />
        </Stack>
      </LocalizationProvider>
    </div>
  );
}
```
- Datepicker နဲ့ App component တွေကြား props ကို သုံးပြီး dataတွေ state တွေ ချိတ်ဆက်ပြီးပါပြီး။
- အခု Timepicker componenet မှာ App componentမှတဆင့်  server ဆီက fetch လုပ်ပြီး ရလာတဲ့ data တွေကို ပြပေးနိုင်ဖို့ ဆက်လုပ်ပါမယ်။
```js
// App.tsx
import React, { useEffect, useState } from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker, { Slot } from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";

function App() {
  const [value, setValue] = useState<Dayjs | null>(dayjs());

//use Slots interface from Timepicker
  const [slots, setSlots] = useState<Slot[]>();
  
// to avoid re-render
  useEffect(() => {
    fetchData(value);
  }, [value]);

  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");
    const url = `http://localhost:5000/available?date=${choosenDate}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    setSlots(data);// Update slots stage
  };

  return (
    <div className="App">
      <DatePicker value={value} handleDateChange={setValue} />
      <TimePicker slots={slots} />
    </div>
  );
}

export default App;
```
> ရှင်းလင်းချက်

- React component မှာ type လုပ်ထားတဲ့ interface တစ်ခုကို exportလုပ်ထားပေးရင် တစ်ခြား component က နေ ခေါ်သုံးလို့ရပါတယ်။
`import TimePicker, { Slot } from "./components/TimePicker/TimePicker";`
- TimePicker component မှာ type လုပ်ထားတဲ့ Slot interface ကို import လုပ်ထားပါတယ်။
`const [slots, setSlots] = useState<Slot[]>();`
- server  ကနေ fetch လုပ်ပြီး ရလာမယ့် data ကို slots အနေနဲ့ သိမ်းပြီး TimePicker component  ဆီကို props အနေနဲ့ ပို့ချင်တာမလို့ သတ်မှတ်လိုက်တာပါ။
- `useState<Slot[]>()`slots ရဲ့ type ကိုလဲ import လုပ်ထားတဲ့ Slot interface ဖြစ်ကြောင်း သတ်မှတ်ပေးထားပြီး array တစ်ခု ဖြစ်ကြောင်းပါ type လုပ်ထားပေးလိုက်တာဖြစ်ပါတယ်

```js
 useEffect(() => {
    fetchData(value);
  }, [value]);
  
  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");
    const url = `http://localhost:5000/available?date=${choosenDate}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    setSlots(data);// Update slots stage
  };
  ```
  - fetchData function မှာ server ဆီ request လုပ်ပြီး ရလာတဲ့ data ကို slots မှာ ထည့်သိမ်းလိုက်တာပါ။
  - fetchData function ကို ဒီအတိုင်း အလွတ်ခေါ်မယ်ဆိုရင် slots ရဲ့ တန်ဖိုးပြောင်းပါမယ်( stage change)
  - react မှာ ( stage change)  ချိန်းတိုင်း re-render  လုပ်ပေးတာမလို့ fetchData function ကို ဒီအတိုင်း အလွတ်ခေါ်မယ်ဆိုရင် ( stage change)  ချိန်းတိုင်း re-render  လုပ်ပေးတာက ဆက်တိုက်ဖြစ်လာပြီး မလိုလားအပ်တဲ့ error တွေ ဖြစ်လာနိုင်ပါတယ်
  - ဒါကြောင့်မလို့ useEffect Hook ကို သုံးပြီး re-render ပြဿနာကို ဖြေရှင်းလိုက်တာ ဖြစ်ပါတယ်
  - useEffect Hook ဟာ render အားလုံးလုပ်ပြီးတဲ့အချိန်မှ run လေ့ရှိပါတယ်။
  - သူ့အထဲက callback function မှာ state ဘယ်ေလာက်ချိန်းချိန်း re- render မဖြစ်အောင် ထိန်းချုပ်ထားပါတယ်
  - DependencyList မှာ ထည့်ပေးထားတဲ့ value ရဲ့ stage change မှသာ re- render လုပ်ပေးတာမလို့   fetchData function ကို useEffect Hook ထဲ မှာ ခေါ်ပေးလိုက်တာဖြစ်ပါတယ်။
  `<TimePicker slots={slots} />`
  - အခု App component မှာ TimePicker component ဆီ props အနေနဲ့ ပို့မယ့် data အတွက် ပြင်ဆင်ပြီးပြီးမလို့ TimePicker component ကို return ထဲ ထည့်ခေါ်လိုက်ပါတယ်
  - TimePicker component က Slot interface ကို  App component မှာimport ယူသုံးထားတာမလို့ `TimePicker .tsx` မှာ Slot interface ကို export လုပ်ပေးရပါမယ်
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

// export Slot interface for use in another componenet
export interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}
interface Props {
  slots?: Slot[];
}
export default function TimePicker({ slots }: Props) {
  if (!slots) {
    return null;
  }
  return (
    <div className="container">
      <FormControl>
        <FormLabel id="demo-radio-buttons-group-label">Choose Time</FormLabel>
        <RadioGroup
          aria-labelledby="demo-radio-buttons-group-label"
          name="radio-buttons-group"
        >
          {/* mapping slots array and show time */}
          {slots.map((slot) => {
            return (
              <FormControlLabel
                value={slot.time}
                control={<Radio />}
                label={slot.time}
              />
            );
          })}
        </RadioGroup>
      </FormControl>
    </div>
  );
}

```
- အခု ဆိုရင် error ပြနေတာတွေ အဆင်ပြေသွားပြီမလို့ react app ကို run  ပြီး server က data .jsထဲမှာ သိမ်းထားတဲ့ ရက် တစ်ရက် ကိုရွေးစမ်းကြည့်ပါက radio group မှာ time တွေပြပေးတာကို မြင်ရမှာဖြစ်ပါတယ်
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/mmpass1.png)
