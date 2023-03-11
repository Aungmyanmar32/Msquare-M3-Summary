## MSquare Programing Fullstack Course
### Episode-*39* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part5)
-  server က data ကို လှမ်းယူတဲ့အခါ အရင်သင်ခန်းစာမှာလို date အလိုက်မယူတော့ပဲ လ တစ်လ လုံးအလိုက် ရှိတဲ့ date တွေ အကုန် လှမ်းပြီး ယူပါမယ်။
- dayjs မှာ ရှိပြီးသားတဲ့ ဖြစ်တဲ့ .month ကို အသုံးပြုပြီး server ဆီကို လ အလိုက် request လုပ်ပါမယ်
```js
// App.tsx
import React, { useEffect, useState } from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker, { Slot } from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";

function App() {
  const [value, setValue] = useState<Dayjs | null>(dayjs());
  const [slots, setSlots] = useState<Slot[]>();

  useEffect(() => {
    fetchData(value);
  }, [value]);

  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");

    // change query param (Date to month)
    const url = `http://localhost:5000/available?month=${value?.month()}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    setSlots(data);
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
### express server က data model ကို ပြန်ချိန်းရပါမယ်
```js
// data.js

const availableSlot = [
  {
    date: "11-03-2023",
    month: "2",
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "12-03-2023",
    month: "2",
    slot: [
      { time: "09:00", total: 100, booked: 70, availableSlot: 30 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "11-04-2023",
    month: "3",
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "12-04-2023",
    month: "3",
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
];

module.exports = availableSlot;

```
- month  ဆိုတဲ့ property name တစ်ခု တိုးလိုက်ပြီး
- နောက်တစ်လအတွက်ပါ နမူနာ obj နှစ်ခု ထပ်ထည့်လိုက်တာပါ
- ---
- ထပ်ပြီး express server ကrequest ကို လက်ခံပြီး response ပြန်လုပ်တဲ့ get middleware မှာ ပြင်ရပါမယ်။
```js
//server.js

app.get("/available", (req, res) => {
  const choosenMonth = req.query.month;
  const availablityForChoosenDate = availableSlot.filter((slot) => slot.month === choosenMonth);

  res.send(availablityForChoosenDate? availablityForChoosenDate: []);
});
```
- react app start လိုက်ပြီး data ထဲမှာရှိတဲ့ ရက်တစ်ရက်ကို ရွေးကြည့်လိုက်ပါက server က response ပြန်လာတဲ့ data ကို log ထုတ်ထားတာမလို့ console မှာ ရွေးလိုက်တဲ့ ရက်နဲ့ သက်ဆိုင်တဲ့ **လ တစ်လ မှာ ရှိသမျှ ရက်တွေရဲ့ data** ကို ပြပေးနေတာတွေ့ရမှာပါ
```js
//output in console
 (2) [{…}, {…}]
 0: {date:  '11-03-2023',  month:  '2',  slot:  Array(5)}
 1: {date:  '12-03-2023',  month:  '2',  slot:  Array(5)}
  length: 2
 [[Prototype]]: Array(0)
```
---
### Disable Date(no available slots) in Date picker
- Mui Date picker တစ်ခုမှာ date တွေ disable လုပ်ချင်ရင် `shouldDisableDate` attribute ကို အသုံးပြူနိုင်ပါတယ်။
```js
// DatePicker.tsx

import * as React from "react";
import dayjs, { Dayjs } from "dayjs";
import Stack from "@mui/material/Stack";
import TextField from "@mui/material/TextField";
import { LocalizationProvider } from "@mui/x-date-pickers/LocalizationProvider";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { DesktopDatePicker } from "@mui/x-date-pickers/DesktopDatePicker";

interface Props {
  value: Dayjs | null;
  handleDateChange: (value: Dayjs | null) => void;
}

export default function DatePicker({ value, handleDateChange }: Props) {
 
  // date to disable function (return Boolean)
  const dateToDisable = () => {
    return true;
  };

  return (
    <div className="container">
      <h2>Choose available Date</h2>
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Choose Date"
            inputFormat="DD/MM/YYYY"
            value={value}
            shouldDisableDate={dateToDisable}//attribute for disable date
            onChange={(value) => handleDateChange(value)}
            renderInput={(params) => <TextField {...params} />}
          />
        </Stack>
      </LocalizationProvider>
    </div>
  );
}

```
-  `shouldDisableDate` attribute ကို အသုံးပြုပြီး dateToDisable function ကို ခေါ်ထားပါတယ်
-  dateToDisable function က return **true** ဖြစ်တဲ့ ရက်မှန်သမျှကို MUI Date picker က disable လုပ်ပေးမှာ ဖြစ်ပါတယ်.
- datepicker component ကို အပေါ်ကလို ပြင်ပေးပြီး react app မှာ သွားကြည့်ပါက datepicker မှာ date တွေအကုန်  disable ဖြစ်နေတာတွေ့ရမှာ ဖြစ်ပါတယ်။
- ---
-  slot တွေ ပြည့်နေတဲ့ ရက်ကို ပဲ disable လုပ်ချင်တာမလို့ server က data မှာ full slot ဖြစ်နေတဲ့ ရက်တစ်ရက် ထပ်ဖြည့်လိုက်ပါမယ်
```js
//push to data.js

{
    date: "13-03-2023",
    month: "2",
    slot: [
      { time: "09:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "10:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "13:00", total: 200, booked: 200, availableSlot: 0 },
    ],
  },
```
- App component မှာလဲ code တစ်ချို့ ပြင်ရေးပါမယ်
```js
//App.tsx
import React, { useEffect, useState } from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
// chang Slot ot Availability
import TimePicker, { Availability} from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";

function App() {
  const [value, setValue] = useState<Dayjs | null>(dayjs());
  
  // before --> const [slots, setSlots] = useState<Slot[]>();
  //after
  const [availability, setAvilability] = useState<availability[]>()

  useEffect(() => {
    fetchData(value);
  }, [value]);

  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");

    // change query param (Date to month)
    const url = `http://localhost:5000/available?month=${value?.month()}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    //before -- > setSlots(data);
    //after
    setAvilability(data)
  };

  return (
    <div className="App">
      <DatePicker value={value} handleDateChange={setValue} />
      
      {/* before --> <TimePicker slots={slots} /> */}
      {/* after */}
      <TimePicker availability={availability} />
    </div>
  );
}

export default App;

```
- slot  ဆိုတဲ့ ဟာတွေကို availability ဆိုပြီး ပြောင်းလိုက်တာဖြစ်ပါတယ်
- နာမည်ပြောင်းလိုက်တာမလို့ type တွေ ပြန်သတ်မှတ်ပေးရပါမယ်။
- availability ကို props အဖြစ် လက်ခံထားတဲ့ TimePicker component မှာ type လုပ်ပြီး export လုပ်လိုက်ပါမယ်။
```js
//TimePicker.tsx

import React from "react";
import "./Timepicker.css";
import {
  FormControl,
  FormLabel,
  RadioGroup,
  FormControlLabel,
  Radio,
} from "@mui/material";

export interface Availability {
  date: string;
  month: string;
  slot: Slot[];
}
export interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}
interface Props {
  availability?: Availability[];
}
export default function TimePicker({ availability }: Props) {
  return <h1>{availability?.length}</h1>;
  // if (!slots) {
  //   return null;
  // }
  // return (
  //   <div className="container">
  //     <FormControl>
  //       <FormLabel id="demo-radio-buttons-group-label">Choose Time</FormLabel>
  //       <RadioGroup
  //         aria-labelledby="demo-radio-buttons-group-label"
  //         name="radio-buttons-group"
  //       >
  //         {/* mapping slots array and show time */}
  //         {slots.map((slot) => {
  //           return (
  //             <FormControlLabel
  //               value={slot.time}
  //               control={<Radio />}
  //               label={slot.time}
  //             />
  //           );
  //         })}
  //       </RadioGroup>
  //     </FormControl>
  //   </div>
  // );
}

```
- Availability ဆိုတဲ့ interface တစ်ခု type လုပ်လိုက်ပြီး export လုပ်ထားပါတယ်။
- TimePicker function မှာ App component က လာမယ့် availability props ကို လက်ခံပြီး head tag နဲ့ return ပြန်လုပ်ထားပါတယ်။
- အရင် သင်ခန်းစာက code တွေကို  ခန ပိတ်ထားလိုက်ပါတယ်.
- file တွေအကုန် save ပြီး react app ကို start လုပ်ကြည့်ပါက အောက်ပါအတိုင်း ပြပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/1ep40-1.png)
##
### Send data to DatePicker Component
- App Component ကနေ server ဆီ  request လုပ်ပြီး ရလာတဲ့ data ကို DatePicker Component ဆီ ပို့ပါမယ်
```js
// App.tsx
import React, { useEffect, useState } from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";
import TimePicker, { Availability } from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";

function App() {
  const [value, setValue] = useState<Dayjs | null>(dayjs());

 
  const [availability, setAvilability] = useState<Availability[]>();

  useEffect(() => {
    fetchData(value);
  }, [value]);

  const fetchData = async (date: Dayjs | null) => {
    const choosenDate = date?.format("DD-MM-YYYY");

   
    const url = `http://localhost:5000/available?month=${value?.month()}`;
    const response = await fetch(url);
    const data = await response.json();

    //before -- > setSlots(data);
    //after
    setAvilability(data);
  };

  return (
    <div className="App">
      <DatePicker
        value={value}
        handleDateChange={setValue}
        availability={availability}
      />

      <TimePicker availability={availability} />
    </div>
  );
}

export default App;

```
-  DatePicker Component မှာလည်း  App Component ကနေ ၀င်လာမယ့် availability props ကို လက်ခံပြီး log ထုတ်ကြည့်ပါမယ်
```js
//DatePicker.tsx

import * as React from "react";
import dayjs, { Dayjs } from "dayjs";
import Stack from "@mui/material/Stack";
import TextField from "@mui/material/TextField";
import { LocalizationProvider } from "@mui/x-date-pickers/LocalizationProvider";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { DesktopDatePicker } from "@mui/x-date-pickers/DesktopDatePicker";
import { Availability } from "./TimePicker/TimePicker";

interface Props {
  value: Dayjs | null;
  handleDateChange: (value: Dayjs | null) => void;
  availability?: Availability[];
}

export default function DatePicker({
  value,
  handleDateChange,
  availability,
}: Props) {
  console.log(availability);
  const dateToDisable = () => {
    return true;
  };

  return (
    <div className="container">
      <h2>Choose available Date</h2>
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Choose Date"
            inputFormat="DD/MM/YYYY"
            value={value}
            shouldDisableDate={dateToDisable} //attribute for disable date
            onChange={(value) => handleDateChange(value)}
            renderInput={(params) => <TextField {...params} />}
          />
        </Stack>
      </LocalizationProvider>
    </div>
  );
}

```
- ခုဆိုရင် reacr app မှာ availability props ကို log ထုတ်ပေးနေတာ တွေ့ရမှာဖြစ်ပါတယ်
- ဆိုလိုတာက လအလိုက် စစ်ထုတ်ထားတဲ့ array ကို DatePicker Component မှာလည်း အသုံးပြုလို့ ရပြီး ဖြစ်ပါတယ်။
----
## Homework
- DatePicker Component မှာ props အနေနဲ့ ၀င်လာတဲ့ array ကို သုံးပြီး slot full ဖြစ်နေတဲ့( availableSlot = 0 ) ရက်တွေကို date picker မှာ ရွေးလို့မရအောင် လုပ်ကြည့်ကြပါ။

