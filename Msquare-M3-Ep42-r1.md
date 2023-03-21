## MSquare Programing Fullstack Course
### Episode-*42* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part6)
### ဒီနေ့ သင်ခန်းစာမှာတော့ available slot ( 0 ) ဖြစ်နေတဲ့ ရက်တွေနဲ့ server မှာ မရှိတဲ့ ရက်တွေကို date picker  မှာ disable လုပ်တာကို လေ့လာသွားပါမယ်။
- အရင်ဆုံး backend က  data.js မှာ data နဲနဲ ပြင်ပါမယ်
```js
// backend/src/data.js

const availableSlot = [
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
    date: "18-03-2023",
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

module.exports = availableSlot;
```
- ရက်တစ်ချို့ ထပ်ထည့်လိုက်ပြီး month ကို number အဖြစ် ပြောင်းလိုက်တာဖြစ်ပါတယ်။
- backend က index.js မှာလဲ query params ကနေယူတဲ့အခါ number ပြန်ပြောင်းပေးရပါမယ်။
```js
// backend/src/index.js
app.get("/available", (req, res) => {
  const choosenMonth = parseInt(req.query.month, 10);
  const availablityForChoosenDate = availableSlot.filter(
    (slot) => slot.month === choosenMonth
  );

  res.send(availablityForChoosenDate ? availablityForChoosenDate : []);
});
```
- Timepicker ထဲရှိ Availability interface ထဲမှာလဲ type ကို ချိန်းပေးရပါမယ်
```js
export  interface  Availability {

date: string;

month: number; // string to number

slot: Slot[];

}
```
##
- ဆက်ပြီးတော့ slot ပြည့်နေတဲ့ date တွေနဲ့ server data ထဲ မရှိတဲ့ ရက်တွေကို disable လုပ်ပါမယ်။
```js
// DatePicker.tsx (add new code  )
......
const currentMonthAvailability = availability?.filter(
    (item) => item.month === value?.month()
  );
  console.log(currentMonthAvailability);

  const dateToDisable = (date: Dayjs | null) => {
   // filter current date in data
    const currentDate = currentMonthAvailability?.find(
      (item) => item.date === date?.format("DD-MM-YYYY")
    );
   
   // check current date is not full slot
    const isAvailable = currentDate?.slot.some(
      (item) => item.availableSlot !== 0
    );
    return isAvailable ? false : true;
  };
  ......
```
- အရင်ဆုံး availability ကို filter လုပ်ပြီး လက်ရှိ လရဲ့ server  အထဲမှာရှိတဲ့ date တွေကို ရယူလိုက်ပါတယ်
-  dateToDisable function ထဲမှာ filter လုပ်ထားတဲ့ currentMonthAvailability array ကို သုံးပြီး current date ကို သတ်မှတ်လိုက်ပါတယ်
-  current date ထဲမှာ SLOT 0 မဖြစ်နေတဲ့ ရက်တွေကို ရှာလိုက်ပြီး Date picker မှာ disable လုပ်မယ့်ရက်ကို return ပြန်လိုက်ဖြစ်ပါတယ်
- ခုဆိုရင် date picker ကို ဖွင့်လိုက်တာနဲ့ available slot ရှိနေတဲ့ ရက်တွေပဲ ပြပေးမှာဖြစ်ပြီး ကျန် ရက်တွေအကုန်  disable ဖြစ်နေတာကို မြင်ရမှာပါ။


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-21%20121716.png)

## try this
- Date picker မှာ လက်ရှိရက်ကို auto select လုပ်ပြီး အပြာရောင်နဲ့ ပြနေတာကို ဖျောက်ကြည့်ပါ။
