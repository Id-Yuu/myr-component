## Create component

```
import React from "react";
import { NavLink } from "react-router-dom";

const NavBar = (props) => {
  const { children } = props;
  return <nav>{children}</nav>;
};

const NavbarLink = (props) => {
  const { href, text } = props;
  return <NavLink to={href}>{text}</NavLink>;
};

NavBar.link = NavbarLink;

export default NavBar;
```

## How to use

```
import NavBar from "./components/Navbar";

<NavBar>
    <NavBar.link href="gi" text="Genshin Impact" />
    <NavBar.link href="hsr" text="Honkai Star Rail" />
</NavBar>
```
