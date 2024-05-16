# Guide to setting up TypeScript with Express

## Initialize NPM

```bash
npm init -y
```

## Update main field

Update the `main` field in `package.json` from `index.js` to `dist/index.js`

## Create a Express server

```bash
npm i express dotenv
```

The `DotEnv` package is utilized to read environment variables from the `.env` file.

## Install TypeScript with Express and Node types as dev dependency

```bash
npm i -D typescript @types/express @types/node
```

## Create index.ts

Create `src` folder in the root directory and create `index.ts` file there. Populate it with the following code:

```ts
import dotenv from 'dotenv';
import express, { Express, Request, Response } from 'express';

dotenv.config();

const app: Express = express();
const port = process.env.PORT || 3000;

app.get('/', (req: Request, res: Response) => {
    res.send('Express + TypeScript Server');
});

app.listen(port, () => {
    console.log(`[server]: Server is running at http://localhost:${port}`);
});
```

## Initialize tsconfig.json

```bash
tsc --init
```

In `tsconfig.json`, set the `outDir` field to `./dist` and `rootDir` field to `./src`.

## Install `ts-node` and `nodemon` as dev dependency

```bash
npm i -D nodemon ts-node
```

## Create `nodemon.json` file in root directory

Add the following json in `nodemon.json`:

```json
{
    "watch": ["src"],
    "ext": ".ts,.js",
    "ignore": [],
    "exec": "npx ts-node ./src/index.ts"
}
```

## Add scripts in `package.json`

Add the following scripts in `scripts` field of `package.json`:

```json
"build": "npx tsc",
"start": "npm run build && node dist/index.js",
"dev": "npx nodemon"
```
