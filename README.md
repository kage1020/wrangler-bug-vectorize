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

## Cleanup

```bash
npx wrangler vectorize delete bug
```
