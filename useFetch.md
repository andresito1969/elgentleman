# This is useFetch custom hook sample

```
  import { useEffect, useState } from "react";

  // Vemos que tenemos el T generic, esto significa que si usamos el tipo Data, por ejemplo
  // const userData: Data<User> = fetch(userUrl) el Data va a resolver como el tipo o interficie User
  // Lo mismo para params

  type Data<T> = T | null;
  type ErrorType = Error | null;

  interface Params<T> {
    data: Data<T>;
    loading: boolean;
    error: ErrorType;
  }

  // Esto puede llegar a ser raro de entender, pero nosotros tenemos una key (referencia) *useFetch*, que tiene un espacio de memoria el cual tiene una función
  // Entonces la función de la referencia useFetch primero tiene el generic <T> que nosotros podemos pasarle (en const App se puede ver)
  // Luego tenemos su parámetro url y finalmente tenemos que devuelve una interficie con otro genérico, en este caso lo que hemos pasado en App component
  export const useFetch = <T>(url: string): Params<T> {
    const [data, setData] = useState<Data<T>>(null)
    const [loading, setLoading] = useState(true)
    const [error, setError] = useState<ErrorType>(null)

    useEffect(() => 
      const controller = new AbortController()
      const fetchData = async () => {
        try {
          const response = await fetch(url, controller);

          if (!response.ok) throw new Error("error en la petición")

          const jsonData: T = await response.json()
          setData(jsonData)
        } catch(err) {
          setError(err as Error)
        } finally {
          setLoading(false)
        }

        return () => {
          controller.abort()
        }
      }

      fetchData()
    }, [url])

    return { data, loading, error }
  }

```


## Lo usamos en un componente....

import {useFetch} from 'customhooks'

const url = "...."

interface Data {
  name: string;
  lastName: string;
  age: number;
}

const App = () => {
  const {data, error, loading} = useFetch<Data>(url)

  // Ahora el data tiene type Data gracias al generic

  ....
}
