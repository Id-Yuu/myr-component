## Create hooks

create folder and put this code to useFetch.js

```
import { useState, useEffect } from 'react';

export const useFetch = () => {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(
          `https://api.github.com/users/USERNAME/repos?sort=updated`
        );
        const json = await response.json();
        setData(json);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    }
    fetchData();
  }, []);

  return { data, error, loading };
};
```

## How to use

better use mapping component, this component for show data name & description on repository

- [MappingComponent](https://github.com/Id-Yuu/myr-component/blob/main/Component/MappingComponent_ID.md)

last, use this code for output

```
import { Card } from './component/card';
import { useFetch } from "./hooks/useFetch";

export const HomePage = () => {
  const { data, error, loading } = useFetchs();
  return (
    <div>
      <h1>Show Data Repo Github</h1>
      {loading ? <div>Loading...</div> : <Card list={data} />}
      {error && <div>{error}</div>}
    </div>
  );
};
```
