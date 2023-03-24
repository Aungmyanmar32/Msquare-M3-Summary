## MSquare Programing Fullstack Course
### Episode-*34* 
### Summary For `Room(1)` intermediate Class
##
### React Router Dom
- passport-booking-fullstack ဆိုတဲ့ project folder တစ်ခုလုပ်ပါ
- -project folder အထဲမှာ...
- - react app အသစ်တစ်ခုလုပ်ပါ။
- - backend folderတစ်ခု လုပ်ပါ။
```console
// terminal 

mkdir passport-booking-fullstack && cd passport-booking-fullstack

npx create-react-app frontend --template typescript

mkdir backend

```
- backend folder ထဲမှာ express server တစ်ခုလုပ်ထားပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-24%20145850.png)

- frontend folder( react app ) ထဲမှာ mui ကို install လုပ်ပြီး button နှစ်ခု create လုပ်ပေးပါ။
```
npm install @mui/material @emotion/react @emotion/styled @mui/icons-material


```
```js
// App.tsx

import React from "react";
import logo from "./logo.svg";
import "./App.css";
import { Button } from "@mui/material";

function App() {
  return (
    <div className="container">
      <div className="app">
        <Button variant="contained" sx={{ mb: 2 }}>
          Create Booking
        </Button>
        <Button variant="contained" sx={{ mb: 2 }}>
          Check Booking
        </Button>
      </div>
    </div>
  );
}

export default App;
```

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-24%20151918.png)
##
### Src folder အောက်မှာ Routes ဆိုတဲ့ folder တစ်ခုလုပ်ပြီး 
- CheckBooking.tsx
- CreateBooking.tsx
ဖိုင်နှစ်ခု လုပ်ပေးပါ။

```console
//terminal

aungm@MSquare MINGW64 ~/Documents/passport-booking-fullstack/frontend (master)
$ cd src/

aungm@MSquare MINGW64 ~/Documents/passport-booking-fullstack/frontend/src (master)
$ mkdir Routes && cd Routes

aungm@MSquare MINGW64 ~/Documents/passport-booking-fullstack/frontend/src/Routes (master)
$ touch CheckBooking.tsx CreateBooking.tsx

```

- ပြီးရင် အသစ်လုပ်ထားတဲ့ ဖိုင်နှစ်ခုမှာ အောက်က code  တွေ ရေးပေးလိုက်ပါမယ်

```JS
// CheckBooking.tsx
import React from "react";

const CheckBooking = () => {
  return (
    <div>
      <h1>CheckBooking Page</h1>
    </div>
  );
};

export default CheckBooking;
```
```JS
// CreateBooking.tsx
import React from "react";

const CreateBooking = () => {
  return (
    <div>
      <h1>CreateBooking Page</h1>
    </div>
  );
};

export default CreateBooking;
```
##
### reatc router dom ကို install လုပ်ပေးပါ။
```
npm i react-router-dom
```
- index.tsx မှာ route တွေ သတ်မှတ်ပါမယ်။
```js
//index.tsx

import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import CreateBooking from "./Routes/CreateBooking";
import CheckBooking from "./Routes/CheckBooking";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "/create-booking",
    element: <CreateBooking />,
  },
  {
    path: "/check-booking",
    element: <CheckBooking />,
  },
]);

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);
root.render(<RouterProvider router={router} />);

```
- အခု သတ်မှတ်ထားတဲ့ route နဲ့ ၀င်ကြည့်ရင် သက်ဆိုင်ရာ component ကိုပြပေးတာ မြင်ရမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/Msquare-M3-Summary/main/Screenshot%202023-03-24%20160429.png)

- ဆက်ပြီးတော့ ခလုတ်တွေနှိပ်လိုက်ရင် သက်ဆိုင်ရာ route တွေကို သွားနိုင်အောင် ဆက်လုပ်ပါမယ်။
```js
// App.tsx

import React from "react";
import logo from "./logo.svg";
import "./App.css";
import { Button } from "@mui/material";

function App() {
  return (
    <div className="container">
      <div className="app">
        <Button variant="contained" sx={{ mb: 2 }}>
          <a
            href={`/create-booking`}
            style={{ textDecoration: "none", color: "white" }}
          >
            Create Booking
          </a>
        </Button>
        <Button variant="contained" sx={{ mb: 2 }}>
          <a
            href={`/check-booking`}
            style={{ textDecoration: "none", color: "white" }}
          >
            Check Booking
          </a>
        </Button>
      </div>
    </div>
  );
}

export default App;

```

- အခုဆိုရင် button တစ်ခုခု နှိပ်လိုက်တာနဲ့ သက်ဆိုင်တဲ့ page ကို ပြပေးတာ မြင်ရမှာဖြစ်ပါတယ်။
