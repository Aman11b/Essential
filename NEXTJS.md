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
# Next js

- Each page is a react component whihc we export from page.js file
- whatever is rendered is returned by RootLaoyout
- layouts are server components

## What is React Server Components?

- why react server components?
- in react UI=f(state) 100% client side

  > but it requires lots of js,client server waterfall(multiple compoent needs to fetch data one after another)

- in PHP alternative is 100% server-side
- UI=f(data)

  > easy and fast to fetch data,close to data source,0kb of js needed to sent

- we want UI=f(data,state)
  - we want best of both that is REACT SERVER COMPONENT

## What is RSC(name of whole paradigm)?

- a new full satck architecture forr eact apps
- we are eriting frontend and backend code side by side
- RSC is NOT active by default in new React apps(vite apps) it needs to be plemented by framwork like next.js(app router)(coz there is no server)
- intrduced the server as an integral part of react component tree: server component ,it does it by Server component
- server component(name of component type)
  - which only rendered on server never on client
  - they basically do UI=f(data)
  - we can build back end by react
  - dont nmake into bundle
  - default in apps that use the RSC architecture
- client Component (UI=f(state))
  - regular component

### server client boundry

- split point between server and client code
- useclient is used to create this boundry
  - created client subtree which executed in browser

## SERVER COMPONENT VS CLIENT COMPONENT

### server componet

- default
- no state/hooks
- lifting state up -> NA
- Props -> Yes (must be serializable when passed ot client component.No function or classes)
- data fetching : preferred.used asynch,await in component
- can import -> Client amd server components
  > import another module using import syntax
- can render -> Client and server component
  > means on calls another one
- when re-render? ->one state changes

### client component

- use client
- have state/hooks
- lifting state up possible
- Props
- data fetching with 3rd party lib like RQ
- can import -> other client components(cant go back in the client server boundry)
- can render -> can render if client and server component passed as props
- when re-render? -> on URL chnages(navigation)

> render to readable stream is used to strem loading compoent

## How RSC Works behind the scene

{react server}

- compoent tree
  - all server component render on server which create react element which have output of server component,how the dom for each compoent will look like, no longer has code to render each component hence the SC has disappered this is why we cant use state as they will disappear, this is so cox they need ot be sent to client and hence need to be serilizable whihc function are not
- this component thee has hole where the client component will be rendered
  - serialized props passed from SC CC
  - URL to script with component code(powered by framework bundler) this is why it is difficult to implement RSC without Framework

> Virtual DOM of SC + tree of CC (RSC PAYLOAD)

{react client}

- RSC playload is sent to client
- CC are rendered here
- complete "Virtual DOM"

### why RSC playload? why not render SCs as HTML

- describe UI as date,not finished HTML
- when s SC is re-rendered: react is able to merge("reconcile) the current tree on the client with a new tree comming form the server
- as a result UI state can be preserved when a SCs re-renders insted on completely re-generating the page as HTML

## Truth is UI=f(1.-> data)(2.-> state)

## THE RELATIONSHIP BETWEEN RSC SSR

> not the same seperate technologies

- RSC does not replace SSR
- they usually work together
- both client and server compoent is insitailly rendered on the ser when SSR is used
- react server anf react client are two different environment,two part of RSC protocol
- in the RSC model "server" just means " the developers computer"
- RSC does not require a running web server compoent could run only once at built time(static site generation)
- SSR happens only on initial render on re-render client components only render on the actual client

> both client and server components are executed on the server,on the initial server-side render.But from there on, as the app is interactive in the browser,server components only run on the actual web server and client components only run on the actual client,so the actual web browser.

## Image

- First of all,it will automatically serve correctly sized images in modern formats.For example, WebP.And it will also only do this on demand,so only when it's actually necessary.
- Second, the Image component prevents layout shifts because it forces us to specify the exact height and width.
- finally, it also automatically lazy loads images onlywhen they actually enter the viewport,

## what is suspense?

- Built in react component that we can use to catch/isolate compoent(or entire subtree) that are not ready to be rendered("suspencing)
- what cases a compoent to be suspending
  - Fetching data(with support lib)
  - loading code (with react lazy loading)
- native wat to support asynchronous operations in a declarative way(no more isLoading states and render login)
- while rendering suspending component is found -> go to closest suspence parent ("boundry) af discard alredy rendered children
- display fallback compoent /JSX(spinner)
- after async work is done-> render subtree under suspense boundry

## A look behind the scenes of suspence

- in fiber tree dusinr suspence the another build in component gets add in called activity and spinner is also add as fallback as children with hidden as suspence comment the children will be hidden and spinner gets activated and when its done it toggles back
- state is preserved in subsquenet suspending
- fallback will not be shpwn again if ther suspence trigger is wrapped in a transition,in next.js thats the case with page navigation we can reset the suspense boundry with unique key prop
- how does suspense acutally knows that a component is suspending?-> trigger suspense by throwing promise

## error.js

- error.js dont catch error if that happenins in root layout,also only in rendering errors

## Static and dynamic rendering

### Server side rendering

- Nextjs is a react framwork so rendering is done by react follwoing the rules we learned earlier
- both server and client compoent are rnedered on the server on the initial render
- next js server-side rendering work is spilt by routes
- each routes can be either static (also called pre-rendered) or dynamic
- there is also a partial pre-rendering (PRR) whihc mixes dynamic and staic rendering in the same route

### Static rendering

- HTML is generated at built time or periodically in the backgroud by re-fetching data(IRS) Incremental staic regenration
- useful when data doent change often and is not personlized to user
- default rendering statergy in nextjs(even when a page or compoent fetched data)
- when deployed to vercel each static route is automatically hosted on CDN content delivery network
- if all routes of an app are staic the entire app can be exported as a static site SSG static site generation

## Dynamic rendering

- HTML is generated at request time(for each new request reaches the server)
- this makes sense if:
  - tehd ata chnages frequenty and is personiized to the user
  - rendering a route requires infomration that depends on request
- a route automaically switched to dynamic rendering in certain conditions
- whe deployed to versel each dynamic route becomes a serveless function

## when next switched between both

- the route has dynamic segments (page uses params)
- searchParams are used in the page component
- header() or cookies ( are used in any of the routers server compoent)
- an uncahcehd data request is made in any route server compoent

## some terminology

- CONTENT DELIVERY NETWORK(CDN) a network of server located aroud the globe that cache and deliver a website static content(HTML CSS JS IMAGE) from as close as possible to each user
- Serverless computing: with the serverless computing mode we can run aplication code ussually back-end code without managing the server ourselves we can just run single function on a cloud provider: SERVERLESS FUNCTION.The server is initilize and active only for the duration the serverless function is running unlike a traditional node.js app where the server is constantly running

### each dynamic route becomes serverless function

- the "Edge": as close as possible to the user.A CDN is a part of an edge network but there is alos serverless edge computing this is serverless coputing that doest not happebnds on a certral server but on a network that is distributed around the globe as close as possible to the user

> we can selecte certain routes to run on the edge when deploying on vercel

- incremental static regeneration (ISR) a next js feature that allow developer toupdate the content of a static page in the backgroud even after the website has a;ready been built and deployed,This happens by refetching the data of a conmponent or entire route after a certain interval

## Partial pre rendering(PPR)

- Idea/Problem : Most pages dont need to be 100% static aor 100% dyanamic
- Soultion : PPR
  > New rendering statergy that combines static and dynamic rendering in the same routes

1. A static (pre -rendered) shell is served imediete;y from CDN leaving holes for dynamic content (Static shell)
2. the slower dynamic content is streamed in as itsrenderred on the server

## caching in NEXTjs

- CASHING : storing fetched or computed data in a temporary location for furture access insted of having to re-redneer or re-computed the data every time its is needed
- Next.js caches very aggressively eberything that is possible will be chached
- Next.jjs provided APIS for cache revalidation: removing and updating with fresh data
- caching is always on by default

## caching mechanism

### server

## request memoization

- data fetched with similart GET request (same url and options in fetch function)
- one page request(one render, one user)
- no need to fetch at the top of tree: the same fetch in multiple componentns onlt makes on request(on;y in component not route handler or server actions)
- how to revalidate? NA
- how to opt out? AbortController

## data cache

- data fetched in a route or a single fetch request
- indefinitely even across de-deployes (can revalidate or opt out)
- data for static Pages + when revalidationISR
- how to revalidate?
  - Time based automatic for all data on page
    export const revalidate=(time);
  - fetch ("...),{next:{revalidate: time}}
  - on demaind(manual)
    revalidatePath or reavalidateTag

- how to opt out?
  - entire page revaidating=0
  - dynamic ="forced-dynamic"
  - individual request {cache:"no-store}
  - noStore()

## full route cache

- entire static pages(HTML and RSC payload)
- untill the "data" cache is invalidated(or app is re-deployed)
- enables static pages
- how to revalidate?
  - Time based automatic for all data on page
    export const revalidate=(time);
  - fetch ("...),{next:{revalidate: time}}
  - on demaind(manual)
    revalidatePath or reavalidateTag
- how to opt out?
  - entire page revaidating=0
  - dynamic ="forced-dynamic"
  - individual request {cache:"no-store}
  - noStore()

### client

## router cache

- pre-fetch and visisted pages static and dynamic
- 30 sec dynamic/5 min static throught out one session
- SPA like naviagtion
- how to revalidate? NA
- how to opt out? AbortController

### this is the behavious in production mode.cachiing doenst work in development

### Middleware in NXEXTJS

- Request-> Middle ware -> App route ->response
  > Middle ware needs to produce a response either by redirecting or rewriting t a route or sending response directly
- by default middle runs before every route in a project but we an speciy which path using a match
- read set cookines and headers
- authorisation adn authetication
- server side analytics

## server action

- enables interactivity in fulll statck apps
- async function that runs exclusively on the server
- created by " user server" directive only for server action not for server compoent it is default
- server conpoennt dont bridge anything as they are on server anyway
- next.js created API endpoint for each server action. whenever a server action is called POST req is made to URL
- require running web server unline server components

### server action can be defined at tht top of

1. an asunc function in a server component.can be used in component or passed to a client composene
2. standalone file(recommended)

- server <---("use server")----- client (API endpoint)
- server ---("use client")-----> client

### server can be called form

- action atribute in a form on SC and CC
- event handlers,useEffect only in CC

### in server action we can

- data mutation
- update ui with new data- revalidate cache
- work with cookies
  > code is runnign in backend so assuame input is unsafe







