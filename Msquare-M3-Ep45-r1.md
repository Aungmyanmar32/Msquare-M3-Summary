## MSquare Programing Fullstack Course
### Episode-*45* 
### Summary For `Room(1)` intermediate Class
##
### Render in react
- react မှာ 
1. Props ချိန်းတဲ့အခါ
2. State ချိန်းတဲ့အခါ
3. Parent component က render လုပ်တဲ့အခါ
- component တွေကို re-render လုပ်ပေးလေ့ရှိပါတယ်
- Parent component က re-render လုပ်တဲ့အခါ child component တွေကို re-render မဖြစ်စေချင်ရင် memo( ) ထဲမှာ ထည့်ပေးရပါမယ်။
##
- ပြီးခဲ့တဲ့ သင်ခန်းစာကို ဆက်လုပ်သွားပါမယ်
- အရင် passport booking app ထဲက Bookingsteps , DatePicker , TimePicker component တွေကို ခု project ထဲ ပြန်ကူးထည့်ပါမယ်
- အရင် passport booking app ထဲက components folder တစ်ခုလုံးကို src အောက်ကို ကူးထည့်လိုက်ပါမယ်
- မကူးထည့်ခင် dayjs နဲ့ @mui/x-date-pickers modules တွေကို ခု project ထဲ ထည့်ပါမယ်
```console
npm i dayjs @mui/x-date-pickers@5.0.20
```
- အရင် passport booking app ထဲက Bookingsteps , DatePicker , TimePicker component တွေကို ခု project ထဲ ပြန်ကူးထည့်ပါမယ်
- ပြီးရင် CreateBooikng.tsx မှာ Bookingsteps component ကို ထည့်ပေးပါမယ်
```js

//CreateBooikng.tsx

import React from "react";
import Bookingsteps from "../components/Bookingsteps/Bookingsteps";

const CreateBooking = () => {
  return (
    <div>
      <h1>CreateBooking Page</h1>
      <Bookingsteps />
    </div>
  );
};

export default CreateBooking;
```
- အခုဆိုရင် create booking button ကို နှိပ်လိုက်တာနဲ့ Date ရွေးတဲ့ နေရာကို ပြပေးနေတာကို မြင်ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-25%20134856.png)
- backend folder ထဲမှာလည်း အရင် project က server.js နဲ့ data.js ကို ပြန်ကူးထည့်ပြီး ts ပြောင်းလိုက်ပါမယ်
```js
// data.ts
export interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}

export interface Availability {
  date: string;
  month: number;
  slot: Slot[];
}
export const availableSlot = [
  {
    date: "22-03-2023",
    month: 2,
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "23-03-2023",
    month: 2,
    slot: [
      { time: "09:00", total: 100, booked: 70, availableSlot: 30 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "24-03-2023",
    month: 2,
    slot: [
      { time: "09:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "10:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "13:00", total: 200, booked: 200, availableSlot: 0 },
    ],
  },
  {
    date: "11-04-2023",
    month: 3,
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
    month: 3,
    slot: [
      { time: "09:00", total: 100, booked: 40, availableSlot: 60 },
      { time: "10:00", total: 100, booked: 20, availableSlot: 80 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 50, availableSlot: 50 },
      { time: "13:00", total: 200, booked: 170, availableSlot: 30 },
    ],
  },
  {
    date: "18-04-2023",
    month: 3,
    slot: [
      { time: "09:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "10:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "11:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "12:00", total: 100, booked: 100, availableSlot: 0 },
      { time: "13:00", total: 200, booked: 200, availableSlot: 0 },
    ],
  },
];


```

```js
//index.js

import express from "express";
import cors from "cors";
import { availableSlot, Availability, Slot } from "./data";

const app = express();
const port = 5000;
app.use(cors());
app.use(express.json());

app.get("/available", (req, res) => {
  const month = req.query.month as string;
  const choosenMonth = parseInt(month, 10);
  console.log(availableSlot);
  const availablityForChoosenDate = availableSlot.filter(
    (slot: Availability) => slot.month === choosenMonth
  );
  console.log(availablityForChoosenDate);

  res.send(availablityForChoosenDate ? availablityForChoosenDate : []);
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}!`);
});

```
- backend server ကို run ထားပြီး react app ကို စမ်းသပ်ကြည့်ပါက အရင် project ကအတိုင်း အလုပ်လုပ်နေတာ တွေ့ရမှာပါ
