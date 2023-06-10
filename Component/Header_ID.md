## Create Component

```
import React from "react";
import { Link } from "react-router-dom";

const Header = (props) => {
  const { redirectTo, children } = props;
  return (
    <header>
      <Link to={redirectTo}>{children}</Link>
    </header>
  );
};

const HeaderTitle = (props) => {
  const { children } = props;
  return <h1>{children}</h1>;
};

const HeaderDescription = (props) => {
  const { children } = props;
  return <p>{children}</p>;
};


Header.title = HeaderTitle;
Header.description = HeaderDescription;

export default Header;

```

## How to Use

```
import Header from "./components/Header";

<Header redirectTo="/">
  <Header.title>Home</Header.title>
  <Header.description>Description</Header.description>
</Header>
```
