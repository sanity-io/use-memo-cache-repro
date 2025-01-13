## How to reproduce

```bash
pnpm install
pnpm build
```

And you should see this error:

```bash
Error occurred prerendering page "/". Read more: https://nextjs.org/docs/messages/prerender-error
TypeError: w.H.useMemoCache is not a function
    at c (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:68:4306)
    at /Users/cody/Developer/use-memo-cache-repro/.next/server/app/page.js:1:25800
    at eC (/Users/cody/Developer/use-memo-cache-repro/.next/server/app/page.js:1:27452)
    at nO (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:45681)
    at nj (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:47456)
    at nN (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:65255)
    at nI (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:62886)
    at nA (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:46033)
    at nj (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:47502)
    at nj (/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:20:62237)
```

Running `pnpm dev` yields a similar error on the server console:

```bash
 TypeError: resolveDispatcher(...).useMemoCache is not a function
    at App (app/page.tsx:9:32)
   7 |
   8 | export default function App() {
>  9 |   const seconds = useObservable(observable, 0)
     |                                ^
  10 |   return <>Seconds: {seconds}</>
  11 | }
  12 | {
  digest: '41685224'
}
 GET / 500 in 124ms
```

Downgrading to `next@15.1.4` resolves the issue and both `pnpm build` and `pnpm dev` are error-free.
