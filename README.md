GUIA DE INSTALACION DE SVELTE PARA QUE FUNCIONE SVELTE-MATERIAL-UI
Bibliografia y enlaces de interes
Video paso a paso para realizar la instalacion descripta mas abajo
--> https://youtu.be/k9hyeORWSTA
Pagina oficial de svelte
--> https://svelte.dev/
Pagina del proyecto svelte-material-ui (github)
--> https://github.com/hperrin/svelte-material-ui
Pagina con los componentes y ayudas de codigo de svelte-material-ui
--> https://sveltematerialui.com/

Primero instalamos svelte con el comando
--> npx degit sveltejs/template svelte-smui

Luego instalamos la libreria de material-ui
--> npm i --save-dev svelte-material-ui

Luego instalamos path
--> npm i --save-dev path

Instalamos sass
--> npm i --save-dev node-sass

Instalamos rollup postcss
--> npm i --save-dev rollup-plugin-postcss

Realizamos una instalacion general
--> npm install

Agregamos en rollup.config.js la siguiente configuracion
Primero importamos path
--> import path from 'path';

    Luego importamos postcss
        --> import postcss from 'rollup-plugin-postcss';

    Luego de la linea "const production = !process.env.ROLLUP_WATCH;" agregamos el siguiente codigo

        const postcssOption = () => ({
            extensions:['.scss', '.sass'],
            extract: false,
            minimize:true,
            use: [
                ['sass', {
                    includePaths: [
                        './src/theme',
                        './node_modules',
                        // This is only needed because we're using a local mo...
                        // Normally, you would not need this line.
                        path.resolve(__dirname, '..', 'node_modules')
                    ]
                }]
            ]
        })

    En plugins luego de svelte agregamos el siguiente plugins
        --> postcss(postcssOption()),

En la carpeta src agregamos una carpeta para themes y dentro un archivo nuevo. Quedando de la siguiente manera
--> src
|--theme
|--\_smui-theme.scss

    Una vez creado el archiv scss solo se cierra. Notar que el nombre comienza con guion bajo "_"

Ejecutamos la aplicacion para verificar que no existen errores y que la misma es desplegada con el siguiente comando
--> npm run dev

Abrimos el componente App.svelte
--> realizamos el import de un componente de tipo Button de la siguiente manera en la seccion de <script>
--> import Button from '@smui/button';

    --> agregamos en el area del <main> un componente de tipo Button de la siguiente manera
        --> <Button on:click={() => alert('clicked!')}>Just a Button</Button>

INFORMACION PARTICULAR DEL PROYECTO DE INSTALACION DE SVELTE

_Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)_

---

# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

_Note that you will need to have [Node.js](https://nodejs.org) installed._

## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).

## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for _any_ path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
