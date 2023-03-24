## MSquare Programing Fullstack Course
### Episode-*43* 
### Summary For `Room(1)` intermediate Class
##
## Online Booking App (part6)
### ဒီနေ့ သင်ခန်းစာမှာတော့ Slot အလွတ်တွေရှိနေတဲ့ အချိန်တွကို ပြနိုင်အောင် လုပ်ကြပါမယ်
##
- အရင်ဆုံး App.tsx မှာ ရွေးလိုက်တဲ့ date ရဲ့ slot array ကို ထုတ်ယူပါမယ်
```js
 //Get slot from seleted Date
  const getSelectedDateSlots = (): Slot[] | undefined => {
    const selectedDateAvailability = availability?.find(
      (item) => item.date === value?.format("DD-MM-YYYY")
    )?.slot;
    return selectedDateAvailability;
  };
```
- ပြီးရင် Time picker component ဆီ availability တစ်ခုလုံးမပို့တော့ပဲ getSelectedDateSlots function ရဲ့ return တန်ဖိုးကို slots props အနေနဲ့ ပို့ပေးလိုက်ပါမယ်
```js
// in return at App.tsx

<TimePicker slots={getSelectedDateSlots()} />
```
- TimePicker.tsx မှာလည်း အရင်က လက်ခံထားတဲ့ availability နေရာမှာ slots ကို လက်ခံပြီး
ရလာတဲ့ SLOTS array ထဲက time တွေကို ပြပေးအောင် လုပ်ပါမယ်.။
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

export interface Availability {
  date: string;
  month: number;
  slot: Slot[];
}
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
- အခုဆိုရင် ရက်တစ်ရက် ရွေးလိုက်တာနဲ့ အဲ့ဒီရက်ထဲမှာ ရှိတဲ့ time တွေကို ပြပေးမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-23%20100215.png)

- ဒါပေမယ့် slot ပြည့်နေတဲ့ အချိန်ကို ပြပေးနေတာကို မြင်ရမှာပါ
- available slot ( 0 ) ဖြစ်နေတဲ့ အချိန်ကို မပြပေးပဲ ဖျောက်ထားဖို့ လုပ်ပါမယ်။
```js
// Timepicker.tsx > in return section

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
          {/* check availableSlot */}
            if (slot.availableSlot === 0) {
              return;
            }
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
```
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-23%20111256.png)
- available Slot  0 ဖြစ်နေတဲ့ 11:00 ကို ဖျောက်ပေးထားတာကို မြင်ရမှာ ဖြစ်ပါတယ်။
- ဒါပေမယ့် date picker မှာ april လကို ရွေးကြည့်လိုက်ရင် server data မှာ available Slotရှိတဲ့ ရက်တွေ ရှိနေပေမယ့် date picker မှာ disable ဖြစ်နေတာကို မြင်ရမှာပါ။
- အဲ့ဒီerror ကို ဖြေရှင်းကြည့်ရအောင်။
```js
// App.tsx

import React, { useEffect, useState } from "react";
import "./App.css";
import DatePicker from "./components/DatePicker";

import TimePicker, {
  Availability,
  Slot,
} from "./components/TimePicker/TimePicker";
import dayjs, { Dayjs } from "dayjs";


function App() {
  //defind 2 new useState hooks
  const [date, setDate] = useState<Dayjs | null>(null);
  const [month, setMonth] = useState<number>();

  const [availability, setAvilability] = useState<Availability[]>();
  

  useEffect(() => {
    fetchData();
  }, [month]);// change depanancy value to month

  const fetchData = async () => {
    // get selscted month
    const selectedMonth = month ? month : dayjs().month();
    const url = `http://localhost:5000/available?month=${selectedMonth}`;
    const response = await fetch(url);
    const data = await response.json();

    setAvilability(data);
  };

  //Get slot from seleted Date(New write ) 
  const getSelectedDateSlots = (): Availability | undefined => {
    const selectedDateAvailability = availability?.filter(
      (item) => item.date === date?.format("DD-MM-YYYY")
    )[0];
    console.log(selectedDateAvailability);
    return selectedDateAvailability;
  };

  //set step state
  const [step, setStep] = useState(1);

  return (
    <div className="App">
      <DatePicker
        value={date}
        handleDateChange={setDate}
        availability={availability}
        month={month}
        handleMonthChange={setMonth}
      />

      <TimePicker availability={getSelectedDateSlots()} />
      {/* <Main /> */}
    </div>
  );
}

export default App;

```
 ```
 const [date, setDate] = useState<Dayjs | null>(null);
  const [month, setMonth] = useState<number>();
  ```
  - useState hook နှစ်ခု သတ်မှတ်လိုက်ပါတယ်
  ```
 useEffect(() => {
    fetchData();
  }, [month]);
```
-  useEffect hook ကို သုံးတဲ့အခါ dependency array နေရာမှာ  value အစား month ကို ပြောင်းသုံးလိုက်ပါတယ်။
- fetchData function  မှာလည်း code  တစ်ချို့ ပြောင်းထားပါတယ်။
```
  const getSelectedDateSlots = (): Availability | undefined => {
    const selectedDateAvailability = availability?.filter(
      (item) => item.date === date?.format("DD-MM-YYYY")
    )[0];
    console.log(selectedDateAvailability);
    return selectedDateAvailability;
  };
```
 - getSelectedDateSlots function မှာလည်း find method ကနေ filter method ပြောင်းသုံးထားပါတယ်။
 - DatePicker and TimePicker component မှာလည်း အောက်ပါ props တွေ ထည့်းပေးထားပါတယ်
 ```
 <DatePicker
        value={date}
        handleDateChange={setDate}
        availability={availability}
        month={month}
        handleMonthChange={setMonth}
      />

      <TimePicker availability={getSelectedDateSlots()} />
```

- DatePicker and TimePicker component တွေမှာ ရလာတဲ့ props တွေကို သုံးပြီး ပြင်ရေးပါမယ်
```js
// DatePicker.tsx

interface Props {
  value: Dayjs | null;
  handleDateChange: (value: Dayjs | null) => void;
  availability?: Availability[];
  month?: number;
  handleMonthChange: (month?: number) => void;
}

export default function DatePicker({
  value,
  handleDateChange,
  availability,
  handleMonthChange,
  month,
}: Props) {
  const selectedMonth = month ? month : dayjs().month();
 
  const currentMonthAvailability = availability?.filter(
    (item) => item.month === selectedMonth
  );
  console.log("day", availability);

  const dateToDisable = (date: Dayjs | null) => {
    const currentDate = currentMonthAvailability?.find(
      (item) => item.date === date?.format("DD-MM-YYYY")
    );

    const isAvailable = currentDate?.slot.some(
      (item) => item.availableSlot !== 0
    );
    return isAvailable ? false : true;
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
            onMonthChange={(value) => handleMonthChange(value?.month())}
            disableHighlightToday
            renderInput={(params) => <TextField {...params} />}
          />
        </Stack>
      </LocalizationProvider>
    </div>
  );
}

```

```
interface Props {
  value: Dayjs | null;
  handleDateChange: (value: Dayjs | null) => void;
  availability?: Availability[];
  month?: number;
  handleMonthChange: (month?: number) => void;
}

export default function DatePicker({
  value,
  handleDateChange,
  availability,
  handleMonthChange,
  month,
}: Props) 
```
- props အနေနဲ့ လက်ခံထားတွေကို type လုပ်ပေးထားတာဖြစ်ပါတယ်။
```
  onMonthChange={(value) => handleMonthChange(value?.month())}
```
- DesktopDatePicker ထဲမှာ onMonthChange attribute တစ်ခု ထပ်ထည့်ပြီး props အနေနဲ့ ရလာတဲ့ handleMonthChange ကို ခေါ်လိုက်တာဖြစ်ပါတယ်။
- ဆက်ပြီးတော့ Timepicker.tsx မှာလည်း code တစ်ချို့ပြင်ရေးပေးပါမယ်
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

export interface Availability {
  date: string;
  month: number;
  slot: Slot[];
}
export interface Slot {
  time: string;
  total: number;
  booked: number;
  availableSlot: number;
}
interface Props {
  availability?: Availability;
}
export default function TimePicker({ availability }: Props) {
  if (!availability) {
    return null;
  }

  const slots = availability.slot;
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
            if (slot.availableSlot === 0) {
              return;
            }
            return (
              <FormControlLabel
                value={slot.time}
                control={<Radio />}
                label={slot.time}
                key={slot.time}
              />
            );
          })}
        </RadioGroup>
      </FormControl>
    </div>
  );
}

```
- ဒါဆိုရင်တော့  ကျနော်တို့ရဲ့ date picker နဲ့ time picker မှာ လိုချင်တဲ့ ပုံစံရပြီးဖြစ်ပါတယ်
##
### ADD MUI stepper
- Component folder အောက်မှာ Bookingsteps ဆိုတဲ့ folder တစ်ခု လုပ်ပြီး Bookingsteps.tsx ဖိုင်တစ်ခုလုပ်ပါ
- https://mui.com/material-ui/react-stepper/  က ကုဒ်တွေ ကူးယူပြီး Bookingsteps.tsx မှာ ထည့်ပေးလိုက်ပါ။
```
//  Bookingsteps.tsx
import * as React from "react";
import Box from "@mui/material/Box";
import Stepper from "@mui/material/Stepper";
import Step from "@mui/material/Step";
import StepLabel from "@mui/material/StepLabel";
import Button from "@mui/material/Button";
import Typography from "@mui/material/Typography";
import { useState } from "react";

const steps = [
  "Select Date and Time",
  "Personal Information",
  "Review and comfirm",
];

export default function Bookingsteps() {
  const [activeStep, setActiveStep] = useState(0);

  const handleNext = () => {
    setActiveStep((prevActiveStep) => prevActiveStep + 1);
  };

  const handleBack = () => {
    setActiveStep((prevActiveStep) => prevActiveStep - 1);
  };

  return (
    <Box sx={{ width: "80%", mx: "auto", my: "10px" }}>
      <Stepper activeStep={activeStep}>
        {steps.map((label, index) => {
          const stepProps: { completed?: boolean } = {};
          const labelProps: {
            optional?: React.ReactNode;
          } = {};

          return (
            <Step key={label} {...stepProps}>
              <StepLabel {...labelProps}>{label}</StepLabel>
            </Step>
          );
        })}
      </Stepper>
      {activeStep === steps.length ? (
        <React.Fragment>
          <Typography sx={{ mt: 2, mb: 1 }}>
            All steps completed - you&apos;re finished
          </Typography>
          <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
            <Box sx={{ flex: "1 1 auto" }} />
          </Box>
        </React.Fragment>
      ) : (
        <React.Fragment>
          <Typography sx={{ mt: 2, mb: 1 }}>Step {activeStep + 1}</Typography>
          <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
            <Button
              color="inherit"
              disabled={activeStep === 0}
              onClick={handleBack}
              sx={{ mr: 1 }}
            >
              Back
            </Button>
            <Box sx={{ flex: "1 1 auto" }} />

            <Button onClick={handleNext}>
              {activeStep === steps.length - 1 ? "Finish" : "Next"}
            </Button>
          </Box>
        </React.Fragment>
      )}
    </Box>
  );
}


```
- ပြီးရင် App.tsx ထဲက return လုပ်တဲ့နေရာမှာ ကျန်တာအကုန် ခနပိတ်ပြီး Bookingsteps component ကိုပဲ import လုပ်ပြီး return လုပ်လိုက်ပါမယ်
```js
// App.tsx --> return section

return (
    <div className="App">
      <Bookingsteps />
      {/* <DatePicker
        date={date}
        handleDateChange={setDate}
        availability={availability}
        month={month}
        handleMonthChange={setMonth}
        fetchData={fetchData}
      />

      <TimePicker availability={getSelectedDateSlots()} /> */}
      {/* <Main /> */}
    </div>
  );
```
- အခု react app မှာ အောက်ကပုံလိုပြပေးနေမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-24%20095831.png)
##
### Updating Steps Display
- step တွေမှာ လိုချင်တဲ့ COMPONENT  တွေပြနိုင်ဖို့ ဆက်လုပ်ပါမယ်။
- App.tsx က code တွေ အကုန်cut လုပ်ပြီး Bookingstpes.tsx ဆီ ပြောင်းထည့်ပေးပါမယ်
- App.tsx မှာ Bookingsteps component ကို return လုပ်တဲ့ code ပဲ ချန်ခဲ့ပါမယ်
```js
// App.tsx

import "./App.css";

import Bookingsteps from "./components/Bookingsteps/Bookingsteps";

function App() {
  //

  return (
    <div className="App">
      <Bookingsteps />
      {/* <DatePicker
        date={date}
        handleDateChange={setDate}
        availability={availability}
        month={month}
        handleMonthChange={setMonth}
        fetchData={fetchData}
      />

      <TimePicker availability={getSelectedDateSlots()} /> */}
      {/* <Main /> */}
    </div>
  );
}

export default App;


```

```js
// Bookingsteps.tsx

export default function Bookingsteps() {

  // code from App.tsx
  const [date, setDate] = useState<Dayjs | null>(null);
  const [availability, setAvilability] = useState<Availability[]>();
  const [month, setMonth] = useState<number>();

  useEffect(() => {
    fetchData();
  }, [month]);

  const fetchData = async () => {
    const selectedMonth = month ? month : dayjs().month();
    const url = `http://localhost:5000/available?month=${selectedMonth}`;
    const response = await fetch(url);
    const data = await response.json();

    setAvilability(data);
  };

  //Get slot from seleted Date
  const getSelectedDateSlots = (): Availability | undefined => {
    const selectedDateAvailability = availability?.filter(
      (item) => item.date === date?.format("DD-MM-YYYY")
    )[0];
    console.log(selectedDateAvailability);
    return selectedDateAvailability;
  };

 // end of code from App.tsx

  const [activeStep, setActiveStep] = useState(0);
```
- ပြီးရင် Bookingsteps.tsx မှာ renderStep ဆိုတဲ့ function တစ်ခုလုပ်ပြီး  Datepicker & TimePicker component တွေကို render လုပ်ပါမယ်။
```js
 // end of code from App.tsx

  const [activeStep, setActiveStep] = useState(0);

  const handleNext = () => {
    setActiveStep((prevActiveStep) => prevActiveStep + 1);
  };

  const handleBack = () => {
    setActiveStep((prevActiveStep) => prevActiveStep - 1);
  };

  // Render step
  const renderStep = ()=>{
    if (activeStep === 0) {
      return (
        <>
       <DatePicker
        date={date}
        handleDateChange={setDate}
        availability={availability}
        month={month}
        handleMonthChange={setMonth}
        fetchData={fetchData}
      />

      <TimePicker availability={getSelectedDateSlots()} />
        </>
      )
    }
  }
  // end of Render step
  return (
    <Box sx={{ width: "80%", mx: "auto", my: "10px" }}>

```
- ပြီးရင် အခုလုပ်ထားတဲ့ renderStep function ကို return လုပ်တဲ့ အထဲမှာ ခေါ်သုံးပါမယ်
```js
// Bookingsteps.tsx --> return section

return (
    <Box sx={{ width: "80%", mx: "auto", my: "10px" }}>
      <Stepper activeStep={activeStep}>
        {steps.map((label, index) => {
          const stepProps: { completed?: boolean } = {};
          const labelProps: {
            optional?: React.ReactNode;
          } = {};

          return (
            <Step key={label} {...stepProps}>
              <StepLabel {...labelProps}>{label}</StepLabel>
            </Step>
          );
        })}
      </Stepper>
      {activeStep === steps.length ? (
        <>
          <Typography sx={{ mt: 2, mb: 1 }}>
            All steps completed - you&apos;re finished
          </Typography>
          <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
            <Box sx={{ flex: "1 1 auto" }} />
          </Box>
        </>
      ) : (
        <>
          {/* change render display */}
          {renderStep()}
          <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
            <Button
              color="inherit"
              disabled={activeStep === 0}
              onClick={handleBack}
              sx={{ mr: 1 }}
            >
              Back
            </Button>
            <Box sx={{ flex: "1 1 auto" }} />

            <Button onClick={handleNext}>
              {activeStep === steps.length - 1 ? "Finish" : "Next"}
            </Button>
          </Box>
        </>
      )}
    </Box>
  );
```
- အခု ဆိုရင် react app မှာ step 1 အနေနဲ့ DatePicker နဲ့ Timepicker component ကို render လုပ်ပေးနေတာ မြင်ရမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-24%20104018.png)
##
### Add personal information step( step 2 )
- renderStep function မှာ step 2 အတွက် ပြင်ဆင်ပါမယ်။
- Bookingsteps.tsx မှာ ရှိတဲ့ renderStep function မှာ codition ထပ် စစ်ပြီး mui input form  တစ်ခု ထည့်လိုက်ပါမယ်။
```js
// Bookingsteps.tsx --> renderStep function

else if (activeStep === 1) {
      return (
        <Box sx={{ "& > :not(style)": { m: 1 } }}>
          <FormControl variant="standard" sx={{ width: "50%", m: "5px" }}>
            <InputLabel htmlFor="name">Name:</InputLabel>
            <Input
              id="name"
              startAdornment={
                <InputAdornment position="start">
                  <AccountCircle />
                </InputAdornment>
              }
            />
          </FormControl>
          <FormControl variant="standard" sx={{ width: "50%", m: "5px" }}>
            <InputLabel htmlFor="name">Email:</InputLabel>
            <Input
              id="email"
              startAdornment={
                <InputAdornment position="start">
                  <AccountCircle />
                </InputAdornment>
              }
            />
          </FormControl>
          <FormControl variant="standard" sx={{ width: "50%", m: "5px" }}>
            <InputLabel htmlFor="nrc">NRC Number:</InputLabel>
            <Input
              id="nrc"
              startAdornment={
                <InputAdornment position="start">
                  <AccountCircle />
                </InputAdornment>
              }
            />
          </FormControl>
          <FormControl variant="standard" sx={{ width: "50%", m: "5px" }}>
            <InputLabel htmlFor="dob">Date of birth:</InputLabel>
            <Input
              id="dob"
              startAdornment={
                <InputAdornment position="start">
                  <AccountCircle />
                </InputAdornment>
              }
            />
          </FormControl>
        </Box>
      );
    }
```
- အခုဆိုရင် step 2 မှာလည်း form တစ်ခု ပြနေမှာ ဖြစ်ပါတယ်
##
### Try this ...
- ရွေးထားတဲ့ ရက် , အချိန် နဲ့ personal information တွေကို step 3 မှာ ပြနိုင်အောင် လုပ်ကြည့်ပါ

Source Code for this summary
https://github.com/Aungtat/mmpass-react
