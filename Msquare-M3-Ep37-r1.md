## MSquare Programing Fullstack Course
### Episode-*37* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part2)
- ပြီးခဲ့တဲ့သင်ခန်းစာမှာ date picker တစ်ခု ထည့်ခဲ့ပါတယ်
- အဲ့ဒီ date picker ကို လက်ရှိနေ့ရက် အမှန်ရအောင် ပြင်ရေးပါမယ်
```js
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
// code changed here
  const [value, setValue] = React.useState<Dayjs | null>(dayjs());

  const handleChange = (newValue: Dayjs | null) => {
    setValue(newValue);
   
  };
// code change End

  return (
    <div className="container">
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Date desktop"
            inputFormat="DD/MM/YYYY"
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
-အခု react app ကို run လိုက်တာနဲ့ လက်ရှိအချိန်ကို ပြပေးနေမှာဖြစ်ပါတယ်။ 
##
## Send  get method request with choosen date( query params)
### Query Params ( ? )

![enter image description here](https://nullbeans.com/wp-content/uploads/2020/05/urldescription-1.png)

 - termianl နောက်တစ်ခုမှာ backend folder ထဲက expressကို ဖွင့်ထားပေးပါ။
 - react မှာ query ပါတဲ့ url တစ်ခုနဲ့ serverဆီ  request လုပ်ပါမယ်။ query မှာ date picker က ရွေးလိုက်တဲ့ date ကို ထည့်ပေးလိုက်ပါမယ်။
 - request လုပ်မယ့် function ကို handleChange function မှာ  ခေါ်ထားပါမယ်။
 ```jsx
const fetchData = async (date: Dayjs | null) => {
  const choosenDate = date?.format("DD-MM-YYYY");
  const url = `http://localhost:5000/available?date=${choosenDate}`;
  const response = await fetch(url);
  const data = await response.json();
  console.log(data);
};

export default function DatePicker() {
  const [value, setValue] = React.useState<Dayjs | null>(dayjs());
  

  const handleChange = (newValue: Dayjs | null) => {
    setValue(newValue);
    fetchData(newValue);
  };

  return (
    <div className="container">
      <LocalizationProvider dateAdapter={AdapterDayjs}>
        <Stack spacing={3}>
          <DesktopDatePicker
            label="Choose Date"
            inputFormat="DD/MM/YYYY"
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
- fetchData function မှာ server  ဆီကို query params နဲ့ request လုပ်ထားပြီး response ပြန်လာတဲ့ data ကို log ထုတ်ထားပါတယ်
- handleChange function ထဲမှာ တော့ fetchData ကို ပြန်ခေါ်ထားပြီး date တစ်ခု ရွေးလိုက်တိုင်း  server ဆီ request တစ်ခါလုပ်နိုင်အောင် ပြုလုပ်ထားပါတယ်။
- server request လုပ်ရန် ပြင်ဆင်ထားပါပြီး
##
### client က ၀င်လာတဲ့ request ကို server မှာ လက်ခံဖို့ ပြင်ဆင်ပါမယ်
- အရင်ဆုံး server project ထဲမှ နမူနာ data file တစ်ခု လုပ်ပါမယ်
```js
// backend/data.js

onst availableSlot = [
  {
    date: "05-03-2023",
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "06-03-2023",
    slot: [
      { time: "09:00", total: 100, booked: 70, availableSlot: 30 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "07-03-2023",
    slot: [
      { time: "09:00", total: 100, booked: 80, availableSlot: 20 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
];

module.exports = availableSlot;
```
- data.jsဆိုပြီး  Date သုံးခုစာအတွက် Dummy data တွေ ပြုလုပ်ထားပါပြီး export လုပ်ထားပါတယ်။
```js
// backend/server.js

onst express = require("express");
const cors = require("cors");
const availableSlot = require("./data");

const app = express();
const port = 5000;
app.use(cors());

app.get("/available", (req, res) => {
  const choosenDate = req.query.date;
  const choosenSlot = availableSlot.find((slot) => slot.date === choosenDate);

  res.send(choosenSlot ? choosenSlot.slot : []);
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}!`);
});
```
- express server တစ်ခု လုပ်ထားပြီး data.js ထဲက data တွေကို require လုပ်ထားပါတယ်။
- `/available` မှာ ၀င်လာတဲ့ request ကို  လက်ခံထားပြီး request နဲ့အတူပါလာတဲ့ date ကို req.quare နဲ့ ဖမ်းယူလိုက်ပါတယ်။
- find method ကို သုံးပြီး ရလာတဲ့ slot ကို response လုပ်ထားပါတယ်။
- express ဆာဗာ နဲ့ react app ကို  start လုပ်ထားပြီး data.js ထဲမှာ ပါတဲ့ date တစ်ခုကို pick ကြည့်ပါက consloe မှာ server က ပြန်လာတဲ့ slot array ကို မြင်ရမှာဖြစ်ပါတယ်။
```js
// browser console
(5) [{…}, {…}, {…}, {…}, {…}]0: 
{time: '09:00', total: 100, booked: 70, availableSlot: 30}
{time: '10:00', total: 100, booked: 20, availableSlot: 80} 
{time: '11:00', total: 100, booked: 100, availableSlot: 0}
{time: '12:00', total: 100, booked: 50, availableSlot: 50}
{time: '13:00', total: 200, booked: 170, availableSlot: 30}
```
