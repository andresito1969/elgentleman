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

### De back a front

#### Bundler v2
Obviamente un bundler hace más cosas que las mencionadas antes, también 
  - transpila código: Hace que el browser entienda nuestro código
  - Bundling: Crea bundles
  - LazyLoading: Carga solo lo necesario


#### Backend:
  - Archivos pueden ser largos y no pasa nada porque se compila y ya está


#### Front:
  - El tamaño y la cantidad de archivos importa para tener un bundle más o menos optimizado
  - Los archivos deben tener solo lo que necesitan
  - Cada componente debe encargarse de una única lógica
  - 400/200 líneas por archivo es ideal
  - Patrón container: Como se muestran las cosas en pantalla
  - Patrón presentacional: Lógica asociada a una única funcionalidad


# REACT
Tenemos 2 triggers:
  - Inicial: monta la app
  - Re-render: Algo ya montado que hace renderizar de nuevo (se triggerea por eventos, llamadas a api etc)

#### Renderizados del DOM y DOM virtual
React tiene un DOM y un DOM virtual, los compara y ve si hay cambios, de haber cambios ejecuta el render solo de lo que ha cambiado.
  - Trigger => Acción que empieza el flujo para que el DOM virtual pueda o no detectar cambios
  - Render => Function que ejecuta la función (para montar un componente o actualizarlo por ejemplo)
  - Commit => Aplicar el cambio detectado en el DOM virtual al DOM real
