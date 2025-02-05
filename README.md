# Introducción al lenguaje Go
Go es un lenguaje de programación de código abierto desarrollado por Google. Es conocido por su simplicidad, eficiencia y soporte robusto para la concurrencia.


## Instalación y configuración
1. Descarga el instalador desde [golang.org](https://golang.org/dl/).
2. Sigue las instrucciones según tu sistema operativo.
3. Verifica la instalación ejecutando:


```
go version
```

## Sintaxis básica
Aquí tienes un ejemplo de un programa básico en Go:


```
go
package main

import "fmt"

func main() {
    fmt.Println("¡Hola, mundo!")
}
```

## Tipos de datos y estructuras
Go soporta los siguientes tipos de datos básicos:
- `int`, `float64`, `string`, `bool`.
- Arrays y slices.
- Mapas.
- Structs.

```go
type Persona struct {
    Nombre string
    Edad   int
}


```
type Persona struct {
    Nombre string
    Edad   int
}

func main() {
    p := Persona{Nombre: "Eduardo", Edad: 25}
    fmt.Println(p)
}
```

## Control de flujo
Go soporta estructuras como `if`, `switch`, y bucles `for`.

Ejemplo:
```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}


```
func main() {
    for i := 0; i < 5; i++ {
        fmt.Println(i)
    }
}
```

## Goroutines y concurrencia
Go es famoso por su modelo de concurrencia basado en Goroutines y canales.

Ejemplo:
```go
func imprimirMensaje(msg string) {
    fmt.Println(msg)
}

func main() {
    go imprimirMensaje("Hola desde Goroutine")
    imprimirMensaje("Hola desde la función principal")
}



```
func imprimirMensaje(msg string) {
    fmt.Println(msg)
}

func main() {
    go imprimirMensaje("Hola desde Goroutine")
    imprimirMensaje("Hola desde la función principal")
}
```

# Fundamentos del Lenguaje Go

### Declarar y usar una función:
```go
package main

import "fmt"

func sumar(a int, b int) int {
    return a + b
}

func main() {
    resultado := sumar(5, 7)
    fmt.Println("La suma es:", resultado)
}



### Crear y ejecutar una prueba unitaria
```go
// archivo: mathutils/sumar_test.go
package mathutils

import "testing"

func TestSumar(t *testing.T) {
    resultado := Sumar(2, 3)
    esperado := 5
    if resultado != esperado {
        t.Errorf("Resultado %d; se esperaba %d", resultado, esperado)
    }
}


```
go test ./...
```


---

# Manejo de Errores en Go

### Usar el tipo `error`:
```go
package main

import (
    "errors"
    "fmt"
)

func dividir(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("no se puede dividir por cero")
    }
    return a / b, nil
}

func main() {
    resultado, err := dividir(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Resultado:", resultado)
    }
}


# Crear un servidor HTTP básico

Go tiene un paquete estándar llamado `net/http` que permite crear servidores web fácilmente.

En este ejemplo, construiremos un servidor HTTP que escuche en el puerto `8080` y devuelva un mensaje de saludo en la ruta `/`.

### Código:
El siguiente código muestra cómo crear y ejecutar el servidor:

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "¡Bienvenido al servidor HTTP en Go!")
}

func main() {
    http.HandleFunc("/", handler) // Configura la ruta "/"
    fmt.Println("El servidor está corriendo en http://localhost:8080")
    http.ListenAndServe(":8080", nil)
}



```
go
package main

import (
    "fmt"
    "net/http"
)

// Manejador para la ruta "/"
func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "¡Bienvenido al servidor HTTP en Go!")
}

func main() {
    // Configurar la ruta "/"
    http.HandleFunc("/", handler)
    fmt.Println("El servidor está corriendo en http://localhost:8080")

    // Iniciar el servidor en el puerto 8080
    http.ListenAndServe(":8080", nil)
}

```

## Análisis del servidor HTTP

### Ventajas del paquete `net/http`:
- No necesitas instalar dependencias externas, ya que es parte de la biblioteca estándar de Go.
- Es fácil de usar para construir aplicaciones web simples.

### Posibilidades de expansión:
1. **Añadir más rutas:**
   Puedes agregar más rutas usando `http.HandleFunc` para diferentes funcionalidades. Ejemplo:
   ```go
   http.HandleFunc("/about", func(w http.ResponseWriter, r *http.Request) {
       fmt.Fprintln(w, "Acerca de nosotros")
   })



```
go
package main

import (
    "fmt"
    "net/http"
    "time"
)

func timeHandler(w http.ResponseWriter, r *http.Request) {
    currentTime := time.Now().Format("15:04:05")
    fmt.Fprintf(w, "La hora actual es: %s", currentTime)
}

func greetHandler(w http.ResponseWriter, r *http.Request) {
    name := r.URL.Query().Get("name")
    if name == "" {
        name = "visitante"
    }
    fmt.Fprintf(w, "¡Hola, %s! Bienvenido a nuestro servidor.", name)
}

func main() {
    http.HandleFunc("/time", timeHandler)
    http.HandleFunc("/greet", greetHandler)
    fmt.Println("El servidor está corriendo en http://localhost:8080")
    http.ListenAndServe(":8080", nil)
}
```

---

### **8. Buenas Prácticas**
#### Contenido sugerido:
- Sigue el formato de código con `gofmt`.
- Usa nombres significativos para variables y funciones.
- Documenta tu código con comentarios.
- Evita funciones largas y realiza separación lógica.

---

### **9. Recursos Adicionales**
#### Contenido sugerido:
- Documentación oficial de Go: [https://golang.org/doc/](https://golang.org/doc/).
- Libros recomendados como *"The Go Programming Language"*.
- Cursos y tutoriales en línea (Codecademy, Coursera, etc.).

---
