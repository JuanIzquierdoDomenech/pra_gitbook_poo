# Clase Node\<T>

### Descripción de la clase <a href="#descripcion-de-la-clase" id="descripcion-de-la-clase"></a>

En esta práctica consideraremos una implementación **alternativa** de la interfaz `List<T>`, basada en representación de secuencias en memoria dispersa, mediante **nodos enlazados**. Para ello, necesitaremos generar una implementación genérica de nodo, que llamaremos `Node<T>`, para almacenar elementos de un tipo de datos genérico `T`.

#### Atributos <a href="#atributos" id="atributos"></a>

| Visibilidad | Declaración     | Descripción                                                                                   |
| ----------- | --------------- | --------------------------------------------------------------------------------------------- |
| public      | `T data`        | El elemento almacenado, de tipo genérico `T`.                                                 |
| public      | `Node<T>* next` | Puntero al siguiente nodo de la secuencia (o `nullptr` si es el último nodo de la secuencia). |

<figure><img src="../.gitbook/assets/https___content.gitbook.com_content_XJ8cratcuUw79RTeMnO7_blobs_VOWV7Lc30SCPWpcBoIjJ_Captura%20de%20pantalla%20de%202023-09-19%2000-41-30.avif" alt=""><figcaption><p>Representación gráfica de objetos de la clase <code>Node&#x3C;T></code></p></figcaption></figure>

#### Métodos <a href="#metodos" id="metodos"></a>

La clase ofrecerá un método constructor:

| Visibilidad | Método                                                                    | Descripción                                                                                                                                                                                |
| ----------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `public`    | `Node(T data, Node<T>* next=nullptr)`                                     | Método constructor. `next` será `nullptr` en caso de que no se proporcione.                                                                                                                |
| `public`    | `friend std::ostream& operator<<(std::ostream &out, const Node<T> &node)` | Sobrecarga global del operador `<<` para imprimir una instancia de `Node<T>` por pantalla. Se limitará a imprimir su atributo `data`. Recuerda incluir la cabecera `<ostream>` en el `.h`. |

***

## Actividad 5: Declaración e implementación de la clase Node\<T>

{% hint style="danger" %}
**La definición e implementación de clases genéricas/templatizadas se debe realizar en un único fichero de cabeceras (.h)**, para que el compilador pueda generar código específico derivado de los templates (más info [aquí](https://isocpp.org/wiki/faq/templates#templates-defn-vs-decl) y [aquí](https://isocpp.org/wiki/faq/templates#templates-defn-vs-decl)).
{% endhint %}

Desde nuestro directorio de trabajo (raíz del repositorio git), abre Vim para crear el fichero `Node.h` que contendrá tanto la definición como la implementación de la clase `Node<T>`.

```bash
vim Node.h
```

Escribe en él la declaración de la clase genérica `Node<T>`, de acuerdo con la especificación del apartado anterior. A continuación tienes una "inicialización" o plantilla de dicho fichero, por si te sirve de ayuda para empezar:

<details>

<summary>Plantilla del fichero Node.h</summary>

```cpp
#include <ostream>

template <typename T> 
class Node {
    public:
        // miembros públicos
    
};
```

</details>

Guarda el fichero y, sin salir de vim, ejecuta el compilador g++ para depurar tu implementación:

```bash
:!g++ -c Node.h  # Recuerda ejecutarlo desde el modo comando de vim!
```

Comprueba la salida del compilador, y depura tu implementación en caso necesario.  A continuación, añade el fichero al área de preparación de git:

```bash
git add Node.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadida implementación de la clase Node"
```

***

## Actividad 6: Depuración de la clase Node\<T>

Guarda en nuestro directorio de trabajo, en el fichero `testNode.cpp`, el siguiente código fuente:

<details>

<summary>Código de test (testNode.cpp)</summary>

```cpp
#include <iostream>
#include "Node.h"

int main(){
    Node<char>* first = new Node<char>('A');
    first = new Node<char>('R', first);
    first = new Node<char>('P', first);

    std::cout << "Secuencia: ";
    Node<char>* aux = first;
    while (aux != nullptr){
        std::cout << aux->data << " ";
        aux = aux->next;
    }
    std::cout << std::endl;
}
```

</details>

Examina su contenido. Verás que crea una secuencia de nodos enlazados para el tipo de datos `char`, y finalmente, la recorre para imprimir sus contenidos.&#x20;

A continuación, abre vim para modificar el fichero `Makefile`:

```bash
vim Makefile
```

y añade la regla `bin/testNode`:

<pre class="language-makefile"><code class="lang-makefile"><strong>bin/testNode: testNode.cpp Node.h
</strong>        mkdir -p bin
        g++ -o bin/testNode testNode.cpp Node.h
</code></pre>

{% hint style="warning" %}
Recuerda: **debes usar tabulador** (tecla `TAB`) para indentar los comandos de la regla.
{% endhint %}

A continuación, ejecuta la regla `bin/testNode`:

```bash
make bin/testNode
```

Ahora, ejecuta el programa de test, para comprobar que tu implementación es correcta. Estando en el directorio raíz del proyecto:

```bash
./bin/testNode
```

Esto debería generar una salida parecida a esta:

<details>

<summary>Salida esperada del progama de test "testNode"</summary>

```
Secuencia: P R A 
```

</details>

Si la semántica de tu salida es diferente, revisa tu código. &#x20;

Añade `testNode.cpp` y `Makefile` a git (y `Node.h` también, si has hecho cambios):

```bash
git add testNode.cpp Makefile Node.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadido código de test de la clase Node; Makefile actualizado"
```

Finalmente, sincroniza tu repositorio local con tu repositorio remoto de GitHub, para enviarle todos los cambios (_commits_) realizados localmente:

```bash
git push
```
