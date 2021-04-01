## wry deno bindings

Attention this is only a proof of concept. API will changes in a close futures.
You can use it for fun tho!

```bash
deno run --unstable -A https://raw.githubusercontent.com/lemarier/wry-deno/main/examples/helloworld.js
```

## Example

```typescript
import { Wry } from "https://raw.githubusercontent.com/lemarier/wry_deno/main/mod.ts";
import { listenAndServe } from "https://deno.land/std/http/server.ts";

const wryApplication = new Wry("http://localhost:8000");

listenAndServe({ port: 8000 }, (req) => {
   req.respond({ body: `Hello from Deno ${Deno.version.deno}` });
});

wryApplication.run(({event}) => {
  switch (event) {
    case 'close':
      Deno.exit()
      break;
    case 'windowCreated':
      console.log("It works! Window created , if webview didn't show, try to resize window");
      break;
    case 'domContentLoaded':
      console.log("It works! domContentLoaded")
      break;
    }
});
```

### Known issue:
- [ ] Window need to be resized to load the webview on macos.
- [x] Linux build do not works as it didnt use winit.