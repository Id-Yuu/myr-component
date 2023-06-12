## Create hooks

```
import { useState, useEffect } from 'react';

export const useFetch = () => {
  const [data, setData] = useState(null);
  const [isPending, setIsPending] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setTimeout(() => {
      fetch('https://api.github.com/users/USERNAME/repos?sort=updated')
      .then(res => {
        if (!res.ok) {
          throw Error('could not fetch the data');
        }
        return res.json();
      })
      .then(data => {
        setIsPending(false);
        setData(data);
        setError(null);
      })
      .catch(err => {
        setIsPending(false);
        setError(err.message);
      })
    }, 1000);
  }, [])

  return { data, isPending, error };
}
```

## How to use

better use mapping component, this component for show data name & description on repository

- [MappingComponent](https://github.com/Id-Yuu/myr-component/blob/main/Component/MappingComponent_ID.md)

last, use this code for output

```
import { Card } from "./components/card";
import { useFetch } from "./hooks/useFetch";

export const HomePage = () => {
  const { data, isPending, error } = useFetch();
  return (
    <MainPage>
      <h1>gi Home</h1>
      {isPending ? <div>Loading...</div> : <Card list={data} />}
      {error && <div>{error}</div>}
    </MainPage>
  );
};
```
