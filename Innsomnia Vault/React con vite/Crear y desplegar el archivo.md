Crearemos un proyecto de laravel sin kit
```cmd
laravel new diremp
```
Y luego lo instalamos
```cmd
PS C:\xampp\htdocs\CursoReactLaravel\diremp> npm create vite
Need to install the following packages:
create-vite@6.3.1
Ok to proceed? (y) y


> npx
> create-vite

│
◇  Project name:
│  react
│
◇  Select a framework:
│  React
│
◇  Select a variant:
│  JavaScript
│
◇  Scaffolding project in C:\xampp\htdocs\CursoReactLaravel\diremp\react...
│
└  Done. Now run:

  cd react
  npm install
  npm run dev

npm notice
npm notice New major version of npm available! 10.9.2 -> 11.2.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.2.0
npm notice To update run: npm install -g npm@11.2.0
npm notice
PS C:\xampp\htdocs\CursoReactLaravel\diremp> cd react
PS C:\xampp\htdocs\CursoReactLaravel\diremp\react> npm install

added 149 packages, and audited 150 packages in 12s

30 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
PS C:\xampp\htdocs\CursoReactLaravel\diremp\react> npm run dev                                 

> react@0.0.0 dev
> vite


  VITE v6.2.2  ready in 404 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```
Al principio da un puerto rarete, vamos a cambiarlo: 
En la ruta react/package.json:
Dentro del scripts{dev{}} ponemos asi
```json
"scripts": {
    "dev": "vite --port=3000",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  }
```
Por cierto, para parar un servidor es con q+ENTER.
y voila, puerto cambiado a 3000.
