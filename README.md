# elgentleman
cosillas aprendidas en el strimin joya

### bundler consta de : (El bundler básicamente transpila nuestra app y realiza estas 3 cosas, a modo de seguridad y velocidad) con npm run build por ejemplo ejecutamos un bundle para producción!
  - uglify
  - minify
  - tree shaking (si algo que creamos no es usado, desaparece del bundle)

### strict mode react (entrevista):
  - renderiza 2 veces todos nuestros componentes de app, normalmente usado mucho en dev y no en producción lógicamente para que el propio react compruebe si el primer renderizado es igual al segundo, de no ser así nos devuelve errors
  - Puede llegar a hacer 2 peticiones en network

### shadcn
  - Nos permite usar componentes reutilizables, lo bueno de esto es que solo importamos el componente a usar y lo mismo al instalarlo, no necesitamos instalar/importar la librería/framework entera
  - Por ejemplo con: npx shadcn@latest add menubar, importaríamos el componente menubar!

### tsconfig.json (configurar)
  - tsconfig.json son opciones a nivel de instalaciones que realizamos en nuestro proyecto: (compilerOptions es interesante)
    ```
{
  "files": [],
  "references": [
    { "path": "./tsconfig.app.json" },
    { "path": "./tsconfig.node.json" }
  ],
  "compilerOptions": {
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
  }, 
}

    ```
  - tsconfig.app.json son opciones a nivel de proyecto, como por ejemplo que al importar usemos @ en vez del path entero:
  ```
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
},
  "include": ["src"]
}

  ```
