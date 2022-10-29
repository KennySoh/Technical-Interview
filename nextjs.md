# Install NVM & Use Node lts
```
nvm install --lts
nvm use --lts
node --version ##Check node lts
```
# Start  nextjs & typescript project
https://nextjs.org/docs/getting-started
```
npx create-next-app@latest --typescript
```

# Add tailwind css
https://tailwindcss.com/docs/guides/nextjs


# Example Folder structure
<img width="250" alt="Screenshot 2022-10-29 at 1 59 46 PM" src="https://user-images.githubusercontent.com/32699647/198816430-32c62f19-fa90-4208-bb47-5520dd7accba.png">





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
## Page pre-rendering & Data fetching
```

```
