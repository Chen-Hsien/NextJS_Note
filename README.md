# NextJS_Note
Build a Production React Product.  
## SEO
## file-based routing system
藉由檔案目錄來控制Routing   
![image](https://github.com/Chen-Hsien/NextJS_Note/assets/24216536/e706921e-03f3-4a46-978e-c94d43d3f90f).  
## fullstack dev -> API Routes
can create Serverless APIs in Nextjs, won't ne worry about scaling, manage another backend server.  
<img width="1093" alt="image" src="https://github.com/Chen-Hsien/NextJS_Note/assets/24216536/78c6bc2c-3633-4daf-9298-9889834f3fe7">
## Automatic code splitting
split pages into separate chunks!  Only loaded it when you need it.
-----
## Default is server side components
<img width="964" alt="image" src="https://github.com/Chen-Hsien/NextJS_Note/assets/24216536/d6c20412-e236-470b-bb31-c95ee549fe85">.  
Add ```use client``` to modify it as a client side components.  
## when to use Server / Client Components
![image](https://github.com/Chen-Hsien/NextJS_Note/assets/24216536/c4bfa5a8-0a19-4371-9c92-f6b2b7f8d41d)
## Data Fetching in 3 ways
1. Server side Rendering (SSR)
2. Static site Heneration (SSG)
3. Incremental Static Generation (ISR)
SSR 在每次請求時動態生成頁面，SSG 在構建時生成靜態 HTML 頁面，而 ISR 則結合了兩者的優點，提供了靜態網站的快速載入速度和一定程度的動態性。   
### SSR
Dynamic server rendering data, each request trigger a rendering
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
    { cache: 'no-store'}
);
}
```

### SSG
Default JS use Static side generation
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
);
}
```

### ISR
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
    { next:{ revalidate:10 } }
);
}
```
