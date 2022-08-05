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
>> [projectId].tsx  - dynamic routes
>> blog 
>>>>[blogId].tsx
```

```
import {useRouter} from "next/router"

function PortfolioPage () {
  const router = useRouter();
  console.log(router.pathname);   #/portfolio/something 
  console.log(router.             # {projectId: "something"}
}
```
