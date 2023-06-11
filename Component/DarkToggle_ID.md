## Create Component
create button component
```
import React from "react";

export const Button = (props) => {
  const { type, children, onClick, classStyle } = props;
  return (
    <>
      <button className={`btn ${classStyle}`} type={type} onClick={onClick}>
        {children}
      </button>
    </>
  );
};

```

## Create Context
put on folder context
```
import React, { createContext, useState } from "react";

export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("dark");
  const toggleTheme = () => {
    setTheme((prev) => (prev === "dark" ? "light" : "dark"));
  };
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={`theme-${theme}`}>{children}</div>
    </ThemeContext.Provider>
  );
};

```

## How to use
Put the Themeprovider between App, edit like this on main.js
```
import { ThemeProvider } from "./Context/Theme.jsx"; // call from directory folder 'Context'

ReactDOM.createRoot(document.getElementById("root")).render(
    <ThemeProvider> 
      <App />
    </ThemeProvider>
);

```

final use, Used anywhere
```
import React, { useContext } from "react";
import { Button } from "../components/Button"; // call from directory folder 'component'
import { ThemeContext } from "./Context/Theme"; // call from directory folder 'Context'

<!-- Create useContext -->
const { toggleTheme, theme } = useContext(ThemeContext);

<!-- Return -->
<Button
  onClick={toggleTheme}
  type="button"
  classStyle={`btn-${theme === "dark" ? "dark" : "light"}`}
>
  {theme === "dark" ? "🌙" : "☀️"}
</Button>
```

