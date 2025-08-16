# Wrangler with OpenNext/Cloudflare bug reproduce

## How to reproduce

1. Clone the repository
2. Install dependencies

```bash
npm install
```

3. Create Vectorize index

```
npx wrangler vectorize create bug --dimensions 1024 --metric cosine
```

4. Add Vectorize binding to wrangler.jsonc

```json
 {
  "vectorize": [
      {
        "binding": "VECTOR",
        "index_name": "bug"
      }
   ]
 }
```

5. Run the development server

```bash
npm run dev
```

```
Error: ENOENT: no such file or directory, open 'C:\Users\<user>\AppData\Roaming\xdg.config\.wrangler\registry\__WRANGLER_EXTERNAL_VECTORIZE_WORKER:<project_name>:VECTORIZE'
    at writeFileSync (node:fs:2425:20)
    at DevRegistry.register (C:\Users\<user>\path\to\project\node_modules\miniflare\dist\src\index.js:58663:41)
    at #registerWorkers (C:\Users\<user>\path\to\project\node_modules\miniflare\dist\src\index.js:60456:23)
    at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
    at async C:\Users\<user>\path\to\project\node_modules\miniflare\dist\src\index.js:60464:7
    at async _Miniflare._getProxyClient (C:\Users\<user>\path\to\project\node_modules\miniflare\dist\src\index.js:60595:5)
    at async _Miniflare.getBindings (C:\Users\<user>\path\to\project\node_modules\miniflare\dist\src\index.js:60614:25)
    at async getPlatformProxy (C:\Users\<user>\path\to\project\node_modules\wrangler\wrangler-dist\cli.js:184490:20)
    at async getCloudflareContextFromWrangler (file:///C:/Users/<user>/path/to/project/node_modules/@opennextjs/cloudflare/dist/api/cloudflare-context.js:144:30)      
    at async initOpenNextCloudflareForDev (file:///C:/Users/<user>/path/to/project/node_modules/@opennextjs/cloudflare/dist/api/cloudflare-context.js:84:21) {
  errno: -4058,
  code: 'ENOENT',
  syscall: 'open',
  path: 'C:\\Users\\<user>\\AppData\\Roaming\\xdg.config\\.wrangler\\registry\\__WRANGLER_EXTERNAL_VECTORIZE_WORKER:<project_name>:VECTORIZE'
}
```

## Cleanup

```bash
npx wrangler vectorize delete bug
```
