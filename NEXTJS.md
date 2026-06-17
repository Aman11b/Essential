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
