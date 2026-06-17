# NEXT.js

> old ways - Server side rendering

> mordern way - client side rendering

> now again server side rendering is getting famous by Next.js remix(full stack framework- has both aspect of server side and client side rendering)

## Client side rendering
- HTML is rendered on the client(the user's computer) using javascript
- leads to slow initila page load
-> bigger javascript bundle needs to be dowlloded before app start running
-> data is fetching after component mount
- highly interavtive : all the code and content has already been loaded(except data)
- SEO can be problematic
- perfect for building heighly interactive SPAs web apps
- Apps taht dont need SEO
-> App that are used "internally" as tools inside companies
-> apps that are completely hidden behind login
## server side rendering
- HTML is rendered on the server(the developer's computer)
- faster initial page load
-> less JS needs to be downloded
-> data fetched before HTML is rendered
- less interactive:pages might be downloded on demand and require full page reload
- SEO -friendly content is easier for search engines to index
- Content driven websites or app where SEO is essential: Ecommerce blogs news marketing etc
### two types of SSR
1. Staic: HTML generated at build time(often called Static Site Generation, or SSG)
2. Dynamic: HTML generated each time server receives a new request(some call only this ssr)

### Typical timeline for CSR

{server} empty page(html css js)->

{client}->(download JS bundle)-> render spinner(first paint meteric)->

{server} fetchin data->

{client}-> render app with data

> initial page load aka Largest conteful paint or Content paint

### Typical timeline for SSR
{server}-> fetching data-> render app with data -> 

{client} -> (sends data to client) (First pain FCP content paint LCP) downlode js bundle -> hydrate(static html becomes interactive by add js)

### Manual ssr
```node
const { createServer, Server } = require("http");

const server = createServer((req, res) => {
  res.end("hellow world");
});

server.listen(8000, () => console.log("listening for request on port 8000"));
```
```bash
node server.js
```
```bash
node --watch server.js
```
> to run react code
```bash
npm i -D @babel/core @babel/preset-env @babel/preset-react @babel/register
npm i react react-dom
```
```js
const { readFile, readFileSync } = require("fs");
const { createServer, Server } = require("http");
const { parse } = require("url");
const { renderToString } = require("react-dom/server");
const React = require("react");
const htmlTemplate = readFileSync(`${__dirname}/index.html`, "utf-8");

const server = createServer((req, res) => {
  const pathName = parse(req.url, true).pathname;
  if (pathName === "/") {
    const renderedReact = renderToString(<Home />);
    const html = htmlTemplate.replace("%%%content%%%", renderedReact);
    res.writeHead(200, { "content-type": "text/html" });
    res.end(html);
  } else if (pathName === "/test") {
    res.end("hellow world testing");
  } else {
    res.end("URL cannot be found");
  }
});

server.listen(8000, () => console.log("listening for request on port 8000"));

const pizzas = [
  {
    name: "Focaccia",
    price: 6,
  },
  {
    name: "Pizza Margherita",
    price: 10,
  },
  {
    name: "Pizza Spinaci",
    price: 12,
  },
  {
    name: "Pizza Funghi",
    price: 12,
  },
  {
    name: "Pizza Prosciutto",
    price: 15,
  },
];

function Home() {
  return (
    <div>
      <h1>🍕 Fast React Pizza Co.</h1>
      <p>This page has been rendered with React on the server 🤯</p>

      <h2>Menu</h2>
      <ul>
        {pizzas.map((pizza) => (
          <MenuItem pizza={pizza} key={pizza.name} />
        ))}
      </ul>
    </div>
  );
}

function Counter() {
  const [count, setCount] = React.useState(0);
  return (
    <div>
      <button onClick={() => setCount((c) => c + 1)}>+1</button>
      <span>{count}</span>
    </div>
  );
}

function MenuItem({ pizza }) {
  return (
    <li>
      <h4>
        {pizza.name} (${pizza.price})
      </h4>
      <Counter />
    </li>
  );
}

```
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">%%%content%%%</div>
  </body>
</html>
```
```js
require("@babel/register").default({ extensions: [".js", ".jsx"] });

require("./server.js");

```
- this runs the HTML and react but ther eis no interactivity
## The Missing Piece -> Hydration(concept)

{server} - React compoent tree -> SSRd HTML, 

- RCT sends react bundle as well which will hydarate with rendered webpage DOM
  
{client} - (content paint LCP ) rendered webpage DOM 

React App on client side (page interactive)

- Hydaration adds back interactivity and event handlers that were lost when HTML was server side randered
- React builds the component tree on the client and compares it with the actual SSRd DOM: Thye must be same so react can adopt it
- if both mismathc we get hydration error,common hydartion error cause,incorrect HTML elemetn ensting,different data used for rendering using browser-only API side effects

## What is Next.js
- react framework for web
- meta framwork build on top of react: we still use component props react hooks etc
- opinionated way of building react app: set of conventions and best practicies regading routing data fetching etc
- allows us to build complex full stack web apps and sites
- allows us to use cutting edge react features that need to be integrated into framework: suspense server components server action steaming etc

## the next.js key ingredients
- server isde rendering(dynamic and static can be selected for each rout)
- file based routing conventions (folder as route,special files for pages layout loader,etc
- data fetching and mutaion on server(fetching data directly in server compoennt,mutation in server action)
- optimization (image,fonts SEO preloading)

## App Router(mordern)
- since 2023
- implements react full stack architucture
- easy fetching with fetch(),create layout loader and advence routing
## page router(legacy)
- since 2016
- simple things like layout are confusing to implement
- data fetching using next.js specific API such as getStatticProps and getServerSideProps
















