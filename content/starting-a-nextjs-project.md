---
title: Starting A NextJS Project
date: 2024-10-26
tags:
  - snippets
---
```
npx create-next-app@latest
```

Set up `shadcn/ui`

```bash
cd my-app
npx shadcn@latest init
```

```bash
npx shadcn@latest add button
```

```js
import { Button } from "@/components/ui/button"

export default function Home() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  )
}
```



