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
