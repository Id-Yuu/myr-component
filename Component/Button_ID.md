## Create Component

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

## How to use

```
import { Button } from "./components/Button";

<Button
    type="button"
    onClick={() => console.log("test")}
    classStyle="btn-primary"
>
    Test
</Button>
```
