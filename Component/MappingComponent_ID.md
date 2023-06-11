## Create Component
create sample data
```
const ListData = [
  {
    id: 1,
    name: "Naruto",
    description: "Naruto is the best",
  },
  {
    id: 2,
    name: "Naruto shippuden",
    description: "Naruto shippuden is the best",
  },
  {
    id: 3,
    name: "Boruto",
    description: "Boruto is the bad",
  },
  {
    id: 4,
    name: "Non non biyori",
    description: "Non non biyori best is the best",
  },
  {
    id: 5,
    name: "Sword Art online",
    description: "Sword Art online best",
  },
];
```

create component with mapping  
```
export const Card = (props) => {
  const { list } = props;
  return (
    <>
      {list.map((item) => {
        return (
          <div className="card" key={item.id}>
            <h1>{item.name}</h1>
            <p>{item.description}</p>
          </div>
        );
      })}
    </>
  );
};
```

## How to use
call this function to use
```
import { Card } from './component/card';

export const CardList = () => {
  return (
    <>
      <!--   List All Data   -->
      <Card list={ListData} />
      
      <!--    Search Filter By name    -->
      <Card list={ListData.filter((item) => item.name === "Non non biyori")} />
    </>
  );
};
```
