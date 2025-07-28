
# 🤓 Starting a Basic Express App with Mongoose & TypeScript

## ✅ 1. Initialize Project

Write these commands in your powershell.

```bash
mkdir my-app
cd my-app
npm init -y
```

## ✅ 2. Install Dependencies

### Runtime Dependencies

```bash
npm i express mongoose
npm install bcryptjs cookie-parser cors dotenv express express-session http-status-codes jsonwebtoken mongoose passport passport-google-oauth20 passport-local zod
```

### Development Dependencies (if you need others)

```bash
npm i -D typescript
npm i -D @types/express @types/cors @types/dotenv @types/jsonwebtoken
npm install --save-dev @eslint/js @types/bcryptjs @types/cookie-parser @types/cors @types/dotenv @types/express @types/express-session @types/jsonwebtoken @types/passport @types/passport-google-oauth20 @types/passport-local eslint ts-node-dev typescript typescript-eslint
```

## ✅ 3. Create `tsconfig.json`

Generate the config:

```bash
tsc --init
```

Edit `tsconfig.json`:

```json
{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}
```

## ✅ 4. Setup Project Structure

```md
my-app/
├── src/
│   ├── app.ts
│   ├── server.ts
│   └── app/        
├── package.json
├── tsconfig.json
└── .gitignore
```

## ✅ 5. Add Scripts to `package.json`

To automatically restart the server whenever you make changes, you can use either `ts-node-dev` or `tsx`. This improves your development experience by saving time and effort.

🔧 Option 1: Using `ts-node-dev`;
Install it as a dev dependency:

```shell
npm i -D ts-node-dev
```

Then, update your `package.json` scripts:

```json
"scripts": {
  "dev": "ts-node-dev --respawn --transpile-only src/server.ts",
  "lint": "npx eslint ./src",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

🔧 Option 2: Using `tsx`;
Install it (either globally or locally as a dev dependency):

> `tsx`- (<https://www.npmjs.com/package/tsx>)

```bash
npm install --save-dev tsx
```

Then, update your `package.json`:

```json
"scripts": {
  "dev": "tsx watch --clear-screen=false src/server.ts",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

---

## 📄 6: Create `eslint.config.mjs`

In your project root, create a file named `eslint.config.mjs`. Then add the following:

```js
// @ts-check

import eslint from "@eslint/js";
import tseslint from "typescript-eslint";

export default tseslint.config(
  eslint.configs.recommended,             // Base JavaScript rules
  tseslint.configs.strict,                // Strict TypeScript rules
  tseslint.configs.stylistic,             // Style-focused rules
  {
    rules: {
      "no-console": "warn",              // Warn on console.log (but allow for debugging)
      // Add more custom rules here if needed
    },
  }
);
```

## ✅ 7. Create `.gitignore`

```gitignore
node_modules/
dist/
```

## ✅ 8. Example Code

### `src/app.ts`

```ts
import express, { Application, Request, Response } from 'express';

const app: Application = express();
app.use(express.json())

app.get('/', (req: Request, res: Response) => {
  res.send('Welcome from Note App!');
});

export default app;
```

### `src/server.ts`

```ts
import mongoose from 'mongoose';
import { Server } from 'http';
import app from './app';

let server: Server;
const port = 5000;

async function main() {
  try {
    await mongoose.connect("mongodb+srv://<db_username>:<db_password>@cluster.mongodb.net/todoDB?retryWrites=true&w=majority&appName=Cluster0");
    console.log('✅ Connected to MongoDB using Mongoose');

    server = app.listen(port, () => {
      console.log(`🚀 Server is listening on port ${port}`);
    });
  } catch (error) {
    console.error('❌ Error connecting to MongoDB:', error);
  }
}

main();
```

## ✅ 9. Run in Development Mode

```bash
npm run dev
```

---
## 10. Lint

Now you can lint your code using:

```bash
npm run lint
```
