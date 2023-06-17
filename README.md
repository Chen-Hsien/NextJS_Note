# NextJS_Note
Build a Production React Product.  
## SEO
1. Crawling - Find what pages exists
2. Indexing - Find what on the pages
3. Ranking - Rank based on users location, language and device
--
* Semantics - using correct html props
* Meta tags - title and description for meta tags
* Image alt tag - alt tag in image

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
Dynamic server rendering data, each request trigger a rendering, Ex. Dynamic News feed, Netflix
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
    { cache: 'no-store'}
);
}
```

### SSG
Default JS use Static side generation, EX. Products list, BLog posts...
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
);
}
```

### ISR
Both SSR + SSG, 
```JS
async finction Page({ params }) {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`,
    { next:{ revalidate:10 } }
);
}
```

### getServerSideProps & getStaticProps
* getServerSideProps
used for server-side rendering and it runs on every request   
當已知此畫面會頻繁的需要載入新資訊，會在每次rendering return props, redirect or notFound   
並且Props object is a key-value pair. 且可以轉為JSON.stringfy。 
* getStaticProps   
used for pre-rendering and it runs at build time   
當已知此畫面較少會出現更動，可以在build time就將畫面資料生成   
並且Props object is a key-value pair. 且可以轉為JSON.stringfy
### Data fetch in expressjs
<img width="626" alt="image" src="https://github.com/Chen-Hsien/NextJS_Note/assets/24216536/54a46199-bbac-47e9-9eae-02afc7b35b46">

### next/head
內建的component, 處理HTML中Head標籤下的內容, 並且可以添加key來避免重複rendering

### next/router
分為三種類型
1. index route -> 預設的root page route
2. nested route -> nested files e.g./coffee-store , 若為page/coffee-store/index.js, 則需要在資料夾下新增index.js做為預設page
3. dynamic routes -> define brackets e.g./coffee-store/[id]
以及兩種規
1. Page必須為React component
2. Component必須設定為 export by default

dynamic routes設定方式, /coffee-store/[id].js   
```JS
import { useRouter } from "next/router";

const CoffeeStore = () => {
  const router = useRouter();
  console.log(router);

  return (
    <div>
      <h1>Coffee Store {router.query.id}</h1>
    </div>
  );
};
```

### next/link
用於處理傳統Anchor element (<a>).  
分為兩種類別.  
1. Non-dynamic/known pages ```<Link to=<route-name> /> ```
2. Dynamic pages ```<Link to=<route-name/[value] />```
常用Props ->   
1. scroll 控制跳轉後要到哪邊
2. prefetch

### next/image
幫忙搞定Image Optimization, 可以隨著使用者的動作仔入需要的圖片


## 小專案
### 各種import
* import Link from 'next/link'
處理頁面之間的跳轉
* import Image from 'next/image'
* import { signIn, signOut, useSession } from 'next-auth/client'
* import GoogleProvider from 'next-auth/providers/google';
console.cloud.google.com


## WAGMI React Hooks for Ethers.js
* useAccount - Returns the connected address. Can also give updates on the type of connection type used. (Won't dig to deep, in short it can be used to display the connected address in other parts of your site or used as an argument for a function).
* useConnect - Can give status if a wallet is connected to the dapp (can have conditional displays). This can also return info on the connector type and the provider being used.
* useContract - An ethers based way of both writing and reading from the contract
* useContractRead - Used to read a function of the connected contract and return it to a variable such as totalSupply or totalMinted.
* useContractWrite - This is how you send calls to the contract, returns many statuses that we will dig into.
* useNetwork - Returns the value of which chain id you are currently on. Also allows you to easily switch network.
* useWaitForTransaction - This will watch your specified function and keep track of the transaction. Will give a loading, success, failure notice.
