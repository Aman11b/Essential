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
