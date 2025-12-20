# React JS

- React is JavaScript front-end framework/library. Specially it used for single page applications which used for fast and interactive experiences.
- It is developed by Facebook software Engineer - Jordan Walke.
- It is a tool for building UI components.
- `Components` -

  - Components are the building blocks of a React app. Each component is a small piece of code that does one specific thing.
  - In simple words, Components are the reusable pieces of a website which helps us to manage how the site behaves based on user interactions.

- `Virtual DOM` -

  - DOM stands for Document Object Model.
  - Updates the part of a page where it is needed. No full page refresh.
  - Superfast and responsive, even with complex interactions.

---

## Basics about React

### Requirements

- Node.js
- npm (included in Node.js)
- npx (included in Node.js)

### Check the Installations

1. node --version
2. npm --version #npm stands for Node Package Manager
3. npx --version #npx stands for Node Package Executable

### Basic-App folder structure

```apache
|- node_modules/            # stores third-party modules
|- public/                   # Similar to assets but considered as constant
|- src/                     # Main folder which stores App.js, Index.js and test files
|- package.json            # App config file
```

- Inside `src` folder

  - `index.js` :- This is the Entrypoint file
  - `App.js` :- This is the main functioning file
  - `App.test.js` :- This is the Test file for debugging

### Organize `src` folder structure

```apache
|- components           # Reusable components used in pages/screens
|- pages/screens        # Contains multiple page
|- styles               # The Cascading Style Sheets are stored
|- Other necessary
```

### How to Setup React App

### 1. Creating React App

1. Using `npx` -

```shell
> npx create-react-app 'app_name'
> cd 'app_name'
> npm start
```

2. Using `vite` -

```shell
> npm create vite@latest
> cd 'app_name'
> npm install
> npm run dev
```

### 2. Installing React Routes

```shell
> npm i react-router-dom
```

---

## Setup the Tailwind with React+Vite

### Create Vite Project

- `npm create vite@latest [ project-name ]-- --template react`
- Move inside project folder `cd [ project-name ]`
- Install tailwind in React

  - `npm install tailwindcss @tailwindcss/vite`

- Configure the vite plugin

  - Add the `@tailwindcss/vite` plugin to vite configuration `(vite.config.js)`

    ```js
    import { defineConfig } from "vite";
    import tailwindcss from "@tailwindcss/vite";
    import react from "@vitejs/plugin-react";

    export default defineConfig({
      plugins: [react(), tailwindcss()],
    });
    ```

- Add `@import "tailwindcss";` into `index.css` file.

---

## Things in ReactJS

### 1. React Components

- We have to create a folder named components which contains different components in our project.

### 2. React Fragment

- This is also called as Parent.
- The elements inside this are called children.
- This is used because of react doesn't allow siblings.
- React Fragment are represented as follows.

  ```js
  function temp() {
    return <></>;
  }
  ```

### 3. JSX in React

- The `JSX` stands for `JavaScript XML`
- This helps react to add different HTML elements into the `index.js` file.
- The following is JSX

  ```js
  import './assets/style.css'
  const text = () => {
    return (
      <>
        <!-- In JSX/JavaScript class is a keyword, that why we use ClassName -->
        <h1 ClassName="h1">Hello World</h1>
      </>
    )
  }

  export default text
  ```

- The above JSX is actually as follows

  ```js
  import React from "react";

  const h1_element = React.createElement("h1", null, "Hello World");

  function text() {
    return <>{h1_element}</>;
  }

  export default text;
  ```

### 4. Props in React

- Props is used to pass data from parent components to child component.
- This is similar to self in python.
- Following is an example of props,

  - Suppose we have a child component as `message.jsx` defined as follows

    ```js
    import React from "react";

    const message = (props) => {
      return <h2>message = {props.msg}</h2>;
    };

    export default message;
    ```

  - Suppose we have another child component as `newmessage.jsx` defined as follows

    ```js
    import React as 'react'

    function newmessage({msg}){
      return (
        <h2>{msg}</h2>
      )
    }

    export default newmessage
    ```

  - Suppose we have a parent component as `App.jsx` defined as follows

    ```js
    import React from 'react'
    import Message from './components/message'
    import NewMessage from './components/newmessage'

    function App() {
      <Message msg="Hello"/>
      <NewMessage msg="World"/>
    }

    export default App
    ```

### 5. Events in React

- Events are the actions which happen onto user interface (UI).
- Eg. Click, Keyboard press, Form Submission, etc.
- Eg.

```js
const eventListener = () => {
  return (
    <>
      <button onClick={console.log("Button is Clicked")}>Click Me</button>
    </>
  );
};

export default eventListener;
```

### 6. Lifting state up in React

- It is exactly opposite to props.
- Here we pass the data from child component to parent component.
- Eg.
- Suppose we have two components `App.jsx` is parent and `Child.jsx` is child

```js
// App.jsx

import Child from "./components/Child";

const data = (message) => {
  console.log(message);
};

function App() {
  return <Child funcvar={data} />;
}

export default App;
```

```js
//Child.jsx

function Child(props) {
  const showmessage = () => {
    props.funcvar("Hello World");
  };

  return <button onClick={showmessage}>click me</button>;
}

export default Child;
```

### 7. State in React

- State is a special object that holds data that can change over time.
- Unlike props, which are passed down from parent to child components, state is managed within the component itself.

### 8. Hooks in React

- Hooks are special functions in React that allows you to use state and other React features in functional components.
- Hooks make your code easier to understand and share logic between the components.
- Built-in Hooks in React

  - useState
  - useEffect
  - useContext
  - useReducer
  - useRef
  - useMemo
    -useCallback
  - Custom hooks

  #### 1. Use of `useState`

  - useState is returns two values (current_state_value, function_to_update_value).
  - Eg.

  ```js
  Example 1

  import {useState} from 'react'

  function useStateEg() {
    const [value, setValue] = useState(0)

    return (
      <>
        <h1>Value : {value}</h1>
        <button onClick={ ()=> {setValue(value + 1)} }>Update value</button>
      </>
    )
  }

  export default useStateEg
  ```

  ```js
  Example 2

  import React from 'react'

  const useStateEg = () => {
    const [stockPrice, newStockPrice] = React.useState({stock : "Google", price : "100$"})

    const updateStockPrice = () => {
      newStockPrice({...stockPrice, price : "200$"})
    }

    return (
      <>
        <h1>Stock : {stockPrice.stock} <br>Price : {stockPrice.price}</h1>
        <button onClick={updateStockPrice}>Get Current Stock Price</button>
      </>
    )

  }

  export default useStateEg
  ```

  #### 2. Use of `useEffect`

  - It is a hook that lets you perform side effects in your functional components.
  - Mainly this function is used while working with API.
  - `Side Effect` - Any action that affects somthing outsite the scope of your component can be considered a side effect.
  - It takes two input (function, dependacy_array)
  - When the components are get mounts on DOM or or when the dependency triggers the `useEffect` function get triggered.
  - `cleanup` function in `useEffect` it is a function which used at return statement of `useEffect`.
  - When the components are get unmounts from DOM or when the dependency state is changed the `cleanup` function is executed.
    - Eg.
    - Fetching data from an API.
    - Subscribing to a data stream
    - Manually change the DOM.
  - Eg.

  ```js
  Example 1

  import React from 'react'

  const EffectEg = () => {
    const [randNum, setRandNum] = React.useState(0);

    const genRandNum = () => {
      setRandNum(Math.floor(Math.random() * 100));
    }

    React.useEffect(() => {
      console.log("useEffect is Triggered);     // This triggers every randNum new value

      return (() => {
        console.log("Cleanup function is Triggered);  // This triggers every randNum old value get vanished
      })

    }, [randNum]);

    return (
      <>
        <h1>Random Number : {randNum}</h1>
        <button onClick = {genRandNum}>Gen new randNum</button>
      </>
    )
  }

  export default EffectEg
  ```

#### 3. use of `useMemo`

- useMemo is a hook that memorizes a value. It remembers the result of a function.
- Useful from avoid expensive calculations on every render.
- It takes two arguments (function, dependancy_array)
- Eg.

  ```js
  import { useMemo, useState } from "react";

  const useMemoEg = () => {
    const [count, setCount] = useState(1);
    const [num, setNum] = useState(1);

    const increaseCount = () => {
      setCount(count + 1);
      if (count % 5 == 0) {
        setNum(count);
      }
    };

    const sumOfNum = useMemo(() => {
      let sum = 0;
      for (let i = 1; i <= num; i++) {
        sum += i;
      }
      return sum;
    }, [num]);

    return (
      <>
        <h1>Count Value : {count}</h1>
        <button className="button" onClick={increaseCount}>
          Increase - Count
        </button>
        <h1>Sum Value : {sumOfNum}</h1>
        <i>The sum is evaluate every 5 count</i>
      </>
    );
  };

  export default useMemoEg;
  ```

#### 4. use of `prop drilling`

- It is similar as multilevel inheritance.
- In props we share the data from parent to child.
- But if we want to share the data from parent to child 3 by child 1, child 2 and child 3, then we use prop drilling.
- Eg.

  ```js
  // Child 3
  import React from 'react'

  const ChildC = ({message}) => {
    <>
      console.log({message});
      <h1>{message}</h1>
    </>

  }

  export default ChildC

  // Child 2
  import React from 'react'
  import ChildB from './/childC'

  const ChildB = (props) => {
    <ChildC message = { props.message }>
  }

  export default ChildB

  // Child 1
  import React from 'react'
  import ChildB from './/childB'

  const ChildA = (props) => {
    return(
      <ChildB message = { props.message }/>
    )
  }

  export default ChildA

  // Parent
  import React from 'react'
  import ChildA from './/components//childA'

  function Parent(){
    return (
      <>
        <ChildA message = "Hello Child C"/>
      </>
    )
  }

  export default Parent
  ```

#### 5. Context API

- This is used to remove complexity in props drilling as we have to pass the props data from parent to child through multiple childs.
- Context API contains `create`, `provider` and `consumer`.
- Context API's consumer contains a function with single argument.
- For multiple context API we have to create multiple providers and multiple consumers.
- Eg.

  ```js
  // ConsumerComponent  - ChildB

  import {egContext1, egContext2} from '../App'

  const ConsumerComponent = () => {
    return (
      <egContext1.Consumer>
        {
          (message1) => {
            return (
              <egContext2.Consumer>
                {
                  (message2) => {
                    <h1>Message 1 : {message1}</h1>
                    <h1>Message 2 : {message2}</h1>
                  }
                }
              <egContext2.Consumer>
            )
          }
        }
      </egContext1.Consumer>
    )
  }

  export default ConsumerComponent

  // ConsumerPage             - ChildA
  import ConsumerComponent from '../Components/consumerComponent'

  const ConsumerPage = () => {
    return (
      <>
        <ConsumerComponent />
      </>
    )
  }

  export default ConsumerPage

  // App                          - Parent
  import ConsumerPage from ./Pages/customerPage
  import { createContext } from 'react'

  const egContext1 = createContext()
  const egContext2 = createContext()

  function App () {
    let message1 = "Hello World"
    let message2 = "New Hello World"

    return (
      <>
        <egContext1.Provider value = {message1}>
          <egContext2.Provider value = {message2}>
            <ConsumerPage />
          </egContext2.Provider>
        </egContext1.Provider>
      </>
    )
  }

  export default App
  export { egContext1, egContext2 }
  ```

#### 6. use of `useContext`

- It is used to remove complexity in `props drilling` and `context api`.
- It just remove the extra code and complex code on consumer.
- Eg.

  ```js
  // ConsumerComponent  - ChildB

  import {useContext} from 'react'

  const ConsumerComponent = () => {
    const egContext1 = useContext(egContext1);
    const egContext2 = useContext(egContext2);

    return (
      <>
        <h1>Message 1 : {egContext1}</h1>
        <h1>Message 2 : {egContext2.msg}</h1>
      </>
    )
  }

  export default ConsumerComponent

  // ConsumerPage             - ChildA
  import ConsumerComponent from '../Components/consumerComponent'

  const ConsumerPage = () => {
    return (
      <>
        <ConsumerComponent />
      </>
    )
  }

  export default ConsumerPage

  // App                          - Parent
  import ConsumerPage from ./Pages/customerPage
  import { createContext } from 'react'

  const egContext1 = createContext()
  const egContext2 = createContext()

  function App () {
    let message1 = "Hello World"
    let message2 = {msg : "New Hello World"}

    return (
      <>
        <egContext1.Provider value = {message1}>
          <egContext2.Provider value = {message2}>
            <ConsumerPage />
          </egContext2.Provider>
        </egContext1.Provider>
      </>
    )
  }

  export default App
  export { egContext1, egContext2 }
  ```

#### 7. use of `useRef`

- Use to access and interact with DOM elements directly.
- Used to store mutable values that doesn't trigger a component re-render.
- `useRef` can hold the previous state value.
- Eg.

  ```js
  // Child
  import { useRef, useState } from "react";

  const useRefeg = () => {
    const { name, setName } = useState("");
    const refElement = useRef("");
    const previousData = useRef("");

    const clearData = () => {
      setName("");
      refElement.current.focus();
    };

    const updateData = (e) => {
      previousData.current = name;
      setName(e.target.value);
    };

    return (
      <>
        <label>Enter your name : </label>
        <input ref={refElement} value={name} onChange={updateData}></input>
        <button onClick={clearData}>- Clear -</button>
        <p>Your previous data : {previousData.current}</p>
      </>
    );
  };
  ```

#### 8. creating custom hooks

- Unlike pre-defined hooks we can create our custom hooks.
- It is mandatory to start custom hook name with use keyword, eg-`use'HookName'`
- Eg.

  ```js
  // Hook
  import { useState } from 'react'

  const useCounter = (initialValue = 0) => {
      const [num, setNum] = useState(initialValue)
      const increment = ()=> {setNum(num + 1)}
      const decrement = ()=> {setNum(num - 1)}
      const reset = ()=> {setNum(initialValue)}

      return { num, increment, decrement, reset }
  }

  export default useCounter

  // Component
  import useCounter from "../hooks/useCounter";

  const customhookeg = () => {
    const { num, increment, decrement, reset } = useCounter()
      return (
      <>
          <div className="container">
              <h1>Counter App New</h1>
              <p>Count : { num }</p>
          </div>
          <div className="button-container">
              <button onClick={increment}>Increment</button>
              <button onClick={decrement}>Decrement</button>
              <button onClick={reset}>Reset</button>
          </div>
      </>
    )
  }
  export default customhookeg
  ```

### 9. Conditional Rendering in React

- It is similar to if else statements in other languages.
- This will be achieved by using ternary operator.
- Eg.

```js
import React from "react";

const conditionalRenderingeg = () => {
  const [isLoggedIn, newLogIn] = React.useState(false);
  const [status, newStatus] = React.useState(true);

  return (
    <>
      <div className="container">
        {isLoggedIn ? (
          <h2>Log In successfully</h2>
        ) : (
          <h2>Please Log in First</h2>
        )}
      </div>
      <div className="container">{status && <h2>Status is ok</h2>}</div>
    </>
  );
};

export default conditionalRenderingeg;
```

### 10. Map function in React

- Map function is a powerful higher order function thats operates on a list.
- This mainly used while iterating onto the list of given data.
- Eg.

```js
import React from "react";

const mapeg = () => {
  const clients = ["Ajay", "Aditya", "Omkar", "Raj", "Rahul", "Sharad"];

  return (
    <>
      <h1>Names of our clients : </h1>
      <div className="container">
        <ul>
          {clients.map((name, i) => (
            <li key={i}>{name}</li>
          ))}
        </ul>
      </div>
    </>
  );
};

export default mapeg;
```

### 11. Inline CSS in React JS

- In this we have to pass style as objects.
- Eg.

```js
import React from "react";

const applyingcsseg = () => {
  const style = {
    container: {
      backgroundColor: "gray",
      color: "white",
      borderRadius: "20px",
    },
  };

  return (
    <>
      <h1>CSS Examples</h1>
      <h1>inline CSS Examples</h1>
      <div className="container">
        <div style={style.container}>
          <h1 style={{ fontSize: "20px", padding: "5px" }}>
            This is 1st Example of inline CSS
          </h1>
        </div>
        <h1
          style={{
            fontSize: "20px",
            color: "gray",
            backgroundColor: "white",
            borderRadius: "20px",
            padding: "5px",
          }}
        >
          This is 2nd Example of inline CSS
        </h1>
      </div>
      <br />
    </>
  );
};

export default applyingcsseg;
```

### 12. Internal CSS in React JS

- Eg.

```js
import React from "react";

const applyingcsseg = () => {
  return (
    <>
      <style>
        {`
                .container{
                  justify-items: center;
                }

                .new-container{
                    background-color: white;
                    color: black;
                    justify-items: center;
                    border-radius: 30px;
                    width: fit-content;
                }

                .new-container h1{
                    padding: 5px;
                    text-align: center;
                }
            `}
      </style>

      <h1>CSS Examples</h1>

      <h1>Internal CSS Examples</h1>
      <div className="container">
        <div className="new-container">
          <h1>This is Internal CSS Example</h1>
        </div>
      </div>
    </>
  );
};

export default applyingcsseg;
```

### 13. External CSS in React JS

- Eg.

```js
import React from "react";
import "../assets/style.css";

const applyingcsseg = () => {
  return (
    <>
      <h1>CSS Examples</h1>

      <h1>External CSS Examples</h1>
      <div className="container">
        <h1>This is External CSS Example</h1>
      </div>
    </>
  );
};

export default applyingcsseg;
```

### 14. Loading Images in React JS

- Eg.

```js
import Image1 from "../assets/images/430915.jpg";

const loadImageeg = () => {
  return (
    <>
      <h1>Loading Image</h1>
      <img src={Image1} alt="image1" width={500}></img>
    </>
  );
};

export default loadImageeg;
```

### 15. Forms in React JS

- Eg.

```js
import { useState } from "react";

const formsEg = () => {
  // for method 1
  const [firstName, setFirstName] = useState();
  const [lastName, setLastName] = useState();

  // for method 2
  const [formData, setData] = useState({
    firstName: "",
    lastName: "",
  });

  const updateData = (e) => {
    setData({ ...formData, [e.target.name]: e.target.value });
  };

  return (
    <>
      <h1>Method 1</h1>
      <form
        action=""
        onSubmit={(e) => {
          e.preventDefault();
          console.log("Form Data : ", firstName, lastName);
        }}
      >
        <label>First Name</label>
        <input
          type="text"
          onChange={(e) => setFirstName(e.target.value)}
          value={firstName}
        ></input>
        <br />
        <label>Last Name</label>
        <input
          type="text"
          onChange={(e) => setLastName(e.target.value)}
          value={lastName}
        ></input>
        <br />
        <button type="submit">Submit</button>
      </form>

      <h1>Method 2</h1>
      <form
        action=""
        onSubmit={(e) => {
          e.preventDefault();
          console.log("Form Data : ", formData);
        }}
      >
        <label>First Name</label>
        <input
          type="text"
          name="firstName"
          onChange={updateData}
          value={formData.firstName}
        ></input>
        <br />
        <label>Last Name</label>
        <input
          type="text"
          name="lastName"
          onChange={updateData}
          value={formData.lastName}
        ></input>
        <br />
        <button type="submit">Submit</button>
      </form>
    </>
  );
};

export default formsEg;
```

### 16. Multiple Pages in React

- We have to install React Router `router-dom` in react as it is not inbuilt with react.
- To install this we have to run following cmd,

```shell
npm i react-router-dom
```

- Setup router at `Page.jsx` or `App.jsx`
- HashRouter is for creating routing environments.
- Routes is a components where we specify all the potential router.
- Route is a component we use for individual page.
- To link the pages we need to use Link from `react-router-dom`.
- Eg.

```apache
// Following pages url as
localhost:5173/*
localhost:5173/*/page1
localhost:5173/*/page2
localhost:5173/*/page3
```

```js
// Layout.jsx

import { Navbar } from './navbar'
import { Outlet } from 'react-router-dom'

export function Layout() {
  return(
    <>
      <Navbar />
      <main>
        <Outlet />
      <main/>
    </>
  )
}

```

```js
// Navbar.jsx

import { Link } from "react-router-dom";

export function Home() {
  return (
    <>
      <Link to="/">Home</Link>
      <Link to="/Page1">Page1</Link>
      <Link to="/Page2">Page2</Link>
      <Link to="/Page3">Page3</Link>
    </>
  );
}
```

```js
// App.jsx

import { HashRouter as Router, Routes, Route } from "react-router-dom";
import { Home } from "home";
import { Page1 } from "./pages/page1";
import { Page2 } from "./pages/page2";
import { Page3 } from "./pages/page3";
import { Layout } from "./layout";

function App() {
  return (
    <Router>
      <Routes>
        <Route element={<Layout />}>
          <Route path="/" element={<Home />} />
          <Route path="/page1" element={<Page1 />} />
          <Route path="/page2" element={<Page2 />} />
          <Route path="/page3" element={<Page3 />} />
        </Route>
      </Routes>
    </Router>
  );
}

export default App;
```

---

### 12. More Hooks

#### 1. `useCallback`

- `useCallback` returns a memoized version of the callback function that only changes if one of the dependencies has changed.
- Useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders.

```js
import { useCallback, useState } from "react";

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []); // Dependency array

  return <Child onClick={handleClick} />;
}
```

#### 2. `useReducer`

- An alternative to `useState` for managing complex state logic.

```js
import { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}
```

---

### 13. Advanced Routing

- **`useNavigate` Hook**
  - Used to programmatically navigate to different routes.

```js
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // ... login logic
    navigate("/dashboard");
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

---

### 14. API Integration

- **Using Fetch**

```js
import { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/data")
      .then((response) => response.json())
      .then((json) => setData(json))
      .catch((error) => console.error(error));
  }, []);

  if (!data) return <div>Loading...</div>;
  return <div>{JSON.stringify(data)}</div>;
}
```

- **Using Axios**
  - First install: `npm install axios`

```js
import axios from "axios";
import { useState, useEffect } from "react";

function AxiosFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://api.example.com/data")
      .then((response) => setData(response.data))
      .catch((error) => console.error(error));
  }, []);

  if (!data) return <div>Loading...</div>;
  return <div>{JSON.stringify(data)}</div>;
}
```

---
