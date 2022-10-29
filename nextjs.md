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
```
/public
    favicon.ico
/src
    /common
        /components
            /elements
                /[Name]
                    [Name].tsx
                    [Name].test.ts
        /hooks
        /types
        /utils
    /modules
        /auth
            /api
                AuthAPI.js
                AuthAPI.test.js
            /components
                AuthForm.tsx
                AuthForm.test.ts
            auth.js
    /pages
        /api
          /authAPI
              authAPI.js
          /[Name]API
              [Name]API.js
        _app.tsx
        _document.tsx
        index.tsx
```




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
