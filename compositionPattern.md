### Diferencia entre jsx.Element i reactNode

Un jsx.Element es un elemento de jsx es decir cualquier cosa que consideremos DOM

ReactNode es cualaquier cosa que react pueda renderizar como componentes.

ReactNode es más recomendable que jsx.Element

### Cuándo usar composition pattern?
Generalmente cuando querrámos compartir estados entre componentes de una misma página, es decir al contrario que redux, esto va a venir a nivel de página no a nivel global de toda la app.

### Cómo usar el composition pattern

Tan fácil i elegante como usar la propiedad children en un hijo, el cual su padre la ha pasado dentro de la llamada del componente:

Como podemos ver la página al llamar a los componentes les pone un children junto a la función global que tienen que ejecutar.

Luego los componentes también podrán o no ejecutar un children, pero al menos lo tendrán en caso de que quisieramos continuar con la composition.

Pseudocode:
```
  <Form><Input><Button>Botón del formulario, podría por ejemplo borrar filas</Button></Input></Form>
  <Input/>
  <Button>Botón ajeno al formulario, podría enviar toda la request de la página</Button>
```

#### Archivo de la página
  ```
  interface FormProps {
    children: ReactNode
  }

  const Form = ({children} : FormProps) => {
    return (<form> {children} </form>  
  }

  const ParentComponent = () => {
    const submit = () => {
      console.log("submitted")
    }

    const handleClick = () => {
      console.log("Uy me clickeo todo")
    }

    const dimeHola = () => {
      alert("Hola!")
    }

    return (
      <>
        <!-- Como vemos llamamos al componente colorRed que a su vez llama al componente Button
        <ColorRed>
          <Button parentMethod={dimeHola}>Mi botón rojo</Button>
        </ColorRed>

        <Button parentMethod={handleClick}> Mi botón normal</Button>

        <Form>
          <!-- Desde el ParentComponent como vemos podemos ejecutar lógica global de la pantalla -->
          <!-- Y desde el Form podemos tener lógica que pertenezca al form *_* -->
          <button type="submit" onClick={submit}></button>
        </Form>
      </>
    )
  }
  ```
#### Archivos de componente botones (any porque me da palo xd)
  ```
    <!-- .color-red { color:red; }
    const ColorRed = ({children} : any) => {
      <div className="color-red">{children}</div>
    }

    <!-- .custom-button{ color: inherit} -->
    const Button = ({children, parentMethod} : any) => {
      return (
        <button className="custom-button" onClick={parentMethod}>
          {children}
        </button>
      )
    }
  ```
