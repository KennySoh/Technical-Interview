# Nextsj notes
https://nlbsg.udemy.com/course/nextjs-react-the-complete-guide/learn/lecture/25145296#overview

```
1. Pages & File-based Routing 
2. 
```

## Pages & File-based Routing
```
> pages
>> index.tsx
>> about.tsx - static routes
>> blog 
>>>>[blogId].tsx - dynamic routes
>> [id].tsx
>>>> [projectId].tsx  - nested dynamic routes
```

```
import {useRouter} from "next/router"

function PortfolioPage () {
  const router = useRouter();
  console.log(router.pathname);   #/portfolio/something 
  console.log(router.query);             # {projectId: "something"}, in nested routes there will be more key,values pairs
}
```
