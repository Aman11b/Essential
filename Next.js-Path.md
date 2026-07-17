# Next.js Project roadmap

- Creating a new project
```Terminal
npm install -g pnpm
```
> pnpm is faster then npm and yarn

- create a Next.js app
```Terminal
npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm
```
> --example -This tells create-next-app not to create a blank project, but instead to copy an existing

- Running the development server

> install the project's packages.
```
pnpm i
```
> is got any [ERR_PNPM_IGNORED_BUILDS] Ignored build scripts: bcrypt@5.1.1, sharp@0.34.5 error set this in pnpm-workspace.yaml
```yaml
allowBuilds:
  bcrypt: true
  sharp: true

```

> start development
```
pnpm dev
```
## CSS Styling

### Global styles
- You can import global.css in any component in your application, but it's usually good practice to add it to your top-level component. In Next.js, this is the root layout

### CSS Modules
> create a new file called home.module.css
```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```
> /app/page.tsx
```
import styles from '@/app/ui/home.module.css';
<div className={styles.shape} />
```
### Using the clsx library to toggle class names
> clsx is a library that lets you toggle class names easily.
```tsx
import clsx from 'clsx';
 
export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```
## Optimizing Fonts and Images

- using custom fonts in your project can affect performance if the font files need to be fetched and loaded.
- Cumulative Layout Shift is a metric used by Google to evaluate the performance and user experience of a website. With fonts, layout shift happens when the browser initially renders text in a fallback or system font and then swaps it out for a custom font once it has loaded. This swap can cause the text size, spacing, or layout to change, shifting elements around it.
- Next.js automatically optimizes fonts in the application when you use the next/font module. It downloads font files at build time and hosts them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

### Adding a primary font
- In your /app/ui folder, create a new file called fonts.ts. You'll use this file to keep the fonts that will be used throughout your application.
1. Import the Inter font from the next/font/google module
```ts
import { Inter } from 'next/font/google';
export const inter = Inter({ subsets: ['latin'] });
```
```ts
export const lusitana = Lusitana({
  weight: ['400', '700'],
  subsets: ['latin'],
});
```
> inter becomes something like (simplified):
```ts
{
  className: "__className_ab12cd",
  style: { fontFamily: "'Inter', sans-serif" }
}
```
> That is why we can write
```ts
<body className={inter.className}>
```
- A subset is simply a group of characters (letters, numbers, symbols).Imagine the complete Inter font contains every language.You're essentially saying "My website only needs Latin characters. Don't include the others."This makes the font file smaller, which helps the page load faster.
2. add the font to the <body>
```tsx
  import { inter } from '@/app/ui/fonts';
 <body className={`${inter.className} antialiased`}>{children}</body>
```
> adding the Tailwind antialiased class which smooths out the font

### Why optimize images?
- Next.js can serve static assets, like images, under the top-level /public folder. Files inside /public can be referenced in your application.
- With regular HTML
  - Ensure your image is responsive on different screen sizes.
  - Specify image sizes for different devices.
  - Prevent layout shift as the images load.
  - Lazy load images that are outside the user's viewport.
    
### The Image component

- The <Image> Component is an extension of the HTML <img> tag, and comes with automatic image optimization, such as:
  - Preventing layout shift automatically when images are loading.
  - Resizing images to avoid shipping large images to devices with a smaller viewport.
  - Lazy loading images by default (images load as they enter the viewport).
  - Serving images in modern formats, like WebP and AVIF, when the browser supports it.

### Adding the desktop hero image
- In your /app/page.tsx file, import the component from next/image
```tsx
import Image from 'next/image';
<Image
        src="/hero-desktop.png"
        width={1000}
        height={760}
        className="hidden md:block"
        alt="Screenshots of the dashboard project showing desktop version"
      />
```
> you're setting the width to 1000 and height to 760 pixels. It's good practice to set the width and height of your images to avoid layout shift, these should be an aspect ratio identical to the source image. These values are not the size the image is rendered, but instead the size of the actual image file used to understand the aspect ratio.

## Creating Layouts and Pages

### Nested routing
- Next.js uses file-system routing where folders are used to create nested routes. Each folder represents a route segment that maps to a URL segment.
- page.tsx is a special Next.js file that exports a React component, and it's required for the route to be accessible
- By having a special name for page files, Next.js allows you to colocate UI components, test files, and other related code with your routes. Only the content inside the page file will be publicly accessible. For example, the /ui and /lib folders are colocated inside the /app folder along with your routes.

### Creating the dashboard layout
- Dashboards have some sort of navigation that is shared across multiple pages. In Next.js, you can use a special layout.tsx file to create UI that is shared between multiple pages.
```tsx
import SideNav from '@/app/ui/dashboard/sidenav';
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
      <div className="w-full flex-none md:w-64">
        <SideNav />
      </div>
      <div className="grow p-6 md:overflow-y-auto md:p-12">{children}</div>
    </div>
  );
}
```
- First, you're importing the <SideNav /> component into your layout. Any components you import into this file will be part of the layout.
- The Layout component receives a children prop. This child can either be a page or another layout
- One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering which preserves client-side React state in the layout when transitioning between pages.

### Root layout
```tsx
import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```
- This is called a root layout and is required in every Next.js application. Any UI you add to the root layout will be shared across all pages in your application. You can use the root layout to modify your <html> and <body> tags, and add metadata

## Navigating Between Pages

### Why optimize navigation?
- There's a full page refresh on each page navigation by using a
### The Link component
- Component to link between pages in your application. Link allows you to do client-side navigation with JavaScript.
```tsx
import Link from 'next/link';
  <Link
            key={link.name}
            href={link.href}
            className="flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3"
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
```
- You should now be able to navigate between the pages without seeing a full refresh.
-  Although parts of your application are rendered on the server, there's no full page refresh, making it feel like a native web app.
### Automatic code-splitting and prefetching
---
### Server Rendering
- In Next.js, Layouts and Pages are React Server Components by default
-  On initial and subsequent navigations, the Server Component Payload is generated on the server before being sent to the client.
- There are two types of server rendering, based on when it happens:
  - Prerendering happens at build time or during revalidation and the result is cached.
  - Dynamic Rendering happens at request time in response to a client request.
- The trade-off of server rendering is that the client must wait for the server to respond before the new route can be shown.
-  Next.js addresses this delay by prefetching routes the user is likely to visit and performing client-side transitions.
### Prefetching
- Prefetching is the process of loading a route in the background before the user navigates to it.
- This makes navigation between routes in your application feel instant, because by the time a user clicks on a link, the data to render the next route is already available client side.
- Next.js automatically prefetches routes linked with the Link component when they enter the user's viewport.
- How much of the route is prefetched depends on whether it's static or dynamic:
  - Static Route: the full route is prefetched.
  - Dynamic Route: prefetching is skipped, or the route is partially prefetched if loading.tsx is present.
- By skipping or partially prefetching dynamic routes, Next.js avoids unnecessary work on the server for routes the users may never visit.
-  However, waiting for a server response before navigation can give the users the impression that the app is not responding.
-  To improve the navigation experience to dynamic routes, you can use streaming.
### Streaming
- Streaming allows the server to send parts of a dynamic route to the client as soon as they're ready, rather than waiting for the entire route to be rendered.
- This means users see something sooner, even if parts of the page are still loading.
## Client-side transitions
- Traditionally, navigation to a server-rendered page triggers a full page load.
- This clears state, resets scroll position, and blocks interactivity.
- Next.js avoids this with client-side transitions using the Link component.
- Instead of reloading the page, it updates the content dynamically by:
    - Keeping any shared layouts and UI.
    - Replacing the current page with the prefetched loading state or a new page if available.
- Client-side transitions are what makes a server-rendered apps feel like client-rendered apps.
- And when paired with prefetching and streaming, it enables fast transitions, even for dynamic routes.
---
### Pattern: Showing active links
- A common UI pattern is to show an active link to indicate to the user what page they are currently on.
-  To do this, you need to get the user's current path from the URL.
-   Next.js provides a hook called usePathname() that you can use to check the path and implement this pattern.
- Since usePathname() is a React hook, you'll need to turn nav-links.tsx into a Client Component.
-  Add React's "use client" directive to the top of the file
```tsx
'use client';
import { usePathname } from 'next/navigation';
```
```tsx
export default function NavLinks() {
  const pathname = usePathname();
  // ...
}
```
```tsx
<Link
            key={link.name}
            href={link.href}
            className={clsx(
              'flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3',
              {
                'bg-sky-100 text-blue-600': pathname === link.href,
              },
            )}
          >
```
---
## Fetching Data

### Choosing how to fetch data
- API layer
- APIs are an intermediary layer between your application code and database. There are a few cases where you might use an API:
  - If you're using third-party services that provide an API.
  - If you're fetching data from the client, you want to have an API layer that runs on the server to avoid exposing your database secrets to the client.
- In Next.js, you can create API endpoints using Route Handlers.

### Database queries
- When you're creating a full-stack application, you'll also need to write logic to interact with your database. For relational databases like Postgres, you can do this with SQL or with an ORM.
- There are a few cases where you have to write database queries:
  - When creating your API endpoints, you need to write logic to interact with your database.
  - If you are using React Server Components (fetching data on the server), you can skip the API layer, and query your database directly without risking exposing your database secrets to the client.

### Using Server Components to fetch data
- By default, Next.js applications use React Server Components. Fetching data with Server Components is a relatively new approach and there are a few benefits of using them:
  -  Server Components support JavaScript Promises, providing a solution for asynchronous tasks like data fetching natively. You can use async/await syntax without needing useEffect, useState or other data fetching libraries.
  -  Server Components run on the server, so you can keep expensive data fetches and logic on the server, only sending the result to the client.
  -  Since Server Components run on the server, you can query the database directly without an additional API layer. This saves you from writing and maintaining additional code.
### Using SQL
- There are a few reasons why you should be using SQL
  - SQL is the industry standard for querying relational databases (e.g. ORMs generate SQL under the hood).
  - Having a basic understanding of SQL can help you understand the fundamentals of relational databases, allowing you to apply your knowledge to other tools.
  - SQL is versatile, allowing you to fetch and manipulate specific data.
  - The postgres.js library provides protection against SQL injections.

- The sql function allows you to query your database
```ts
import postgres from 'postgres';
const sql = postgres(process.env.POSTGRES_URL!, { ssl: 'require' });
```
- You can call sql anywhere on the server, like a Server Component.

### there are two things you need to be aware of

- The data requests are unintentionally blocking each other, creating a request waterfall.
---
### What are request waterfalls?
- A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests
- This pattern is not necessarily bad. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the next request.
- However, this behavior can also be unintentional and impact performance.

### Parallel data fetching
- A common way to avoid waterfalls is to initiate all data requests at the same time - in parallel.
- In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData()
  - Start executing all data fetches at the same time, which is faster than waiting for each request to complete in a waterfall.
  - Use a native JavaScript pattern that can be applied to any library or framework.
> However, there is one disadvantage of relying only on this JavaScript pattern: what happens if one data request is slower than all the others?
---
- By default, Next.js prerenders routes to improve performance, this is called Static Rendering. So if your data changes, it won't be reflected in your dashboard.
---
### What is Static Rendering?
- With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or when revalidating data.

> Fetching = Getting the data (from a database, API, CMS, etc.).

> Rendering = Turning React components into HTML and sending it to the browser.

- Whenever a user visits your application, the cached result is served. There are a couple of benefits of static rendering:
  - Faster Websites - Prerendered content can be cached and globally distributed when deployed to platforms like Vercel. This ensures that users around the world can access your website's content more quickly and reliably.
  - Reduced Server Load - Because the content is cached, your server does not have to dynamically generate content for each user request. This can reduce compute costs.
  - SEO - Prerendered content is easier for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.

- Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data which is regularly updated.

### What is Dynamic Rendering?
- With dynamic rendering, content is rendered on the server for each user at request time (when the user visits the page). There are a couple of benefits of dynamic rendering:
   - Real-Time Data - Dynamic rendering allows your application to display real-time or frequently updated data. This is ideal for applications where data changes often.
  - User-Specific Content - It's easier to serve personalized content, such as dashboards or user profiles, and update the data based on user interaction.
  - Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or the URL search parameters.
---
