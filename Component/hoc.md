# Higher-Order Components

create functional `withCounter.jsx`
```
import React, { useState } from "react";

function withCounter(OrinalComponent) {
  return (props) => {
    const { counter } = props;
    const [count, setCount] = useState(0);

    const handleClick = () => {
      setCount(count + counter);
    };

    return (
      <OrinalComponent count={count} handleClick={handleClick} {...props} />
    );
  };
}
export default withCounter;
```

create component `Button.jsx` and import `withCounter.jsx`
```
import React from "react";
import withCounter from "./withCounter";

function Button(props) {
  const { counter, count, handleClick } = props;

  return (
    <div>
      <p>Count : {counter}</p>
      <button onClick={handleClick} type="button">
        +
      </button>
      <p>Output : {count}</p>
    </div>
  );
}
export default withCounter(Button);
```

use component 
```
import Buttons from "./components/Button";

function App() {
  return (
    <>
      <Buttons counter={1} />
      <Buttons counter={2} />
    </>
  );
}

export default App;
```

Reference :

- [Higher-order components](https://legacy.reactjs.org/docs/higher-order-components.html)
