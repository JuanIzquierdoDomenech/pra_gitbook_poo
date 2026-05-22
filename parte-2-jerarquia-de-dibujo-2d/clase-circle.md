# Clase Circle

## Descripción de la clase

El tipo de datos Circle, que representa un círculo en un espacio bidimensional, estará definido por una clase concreta de igual nombre, derivada de la interfaz Shape.

### Atributos

<table><thead><tr><th width="129">Visibilidad</th><th width="190">Declaración</th><th>Descripción</th></tr></thead><tbody><tr><td>private</td><td><code>Point2D center</code></td><td>Centro del círculo</td></tr><tr><td>private</td><td><code>double radius</code></td><td>Radio del círculo</td></tr></tbody></table>

### Métodos

**Además de los métodos&#x20;**<mark style="color:red;">**abstractos**</mark>**&#x20;heredados de la interfaz** [**`Shape`**](clase-abstracta-shape.md), deberá implementar los siguientes métodos:

<table><thead><tr><th width="129">Visibilidad</th><th width="372">Perfil</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>Circle()</code></td><td>Método constructor por defecto. Crea un círculo del color que se haya establecido por defecto, centro (0,0) y radio 1.</td></tr><tr><td><code>public</code></td><td><code>Circle(std::string color, Point2D center, double radius)</code></td><td>Método constructor (con parámetros).</td></tr><tr><td><code>public</code></td><td><code>Point2D get_center() const</code></td><td>Método consultor del atributo <code>center</code>.</td></tr><tr><td><code>public</code></td><td><code>void set_center(Point2D p)</code></td><td>Método modificador del atributo <code>center</code>.</td></tr><tr><td><code>public</code></td><td><code>double get_radius() const</code></td><td>Método consultor del atributo <code>radius</code>.</td></tr><tr><td><code>public</code></td><td><code>void set_radius(double r)</code></td><td>Método modificador del atributo <code>radius</code>.</td></tr><tr><td><code>public</code></td><td><code>std::ostream&#x26; operator&#x3C;&#x3C;(std::ostream &#x26;out, const Circle &#x26;c)</code></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code>. <br><br>Recuerda incluir la cabecera <code>&#x3C;ostream></code> en el <code>.h</code>, así como declararlo <code>friend</code> en la clase.</td></tr></tbody></table>

{% hint style="success" %}
Intenta reaprovechar la implementación del método abstracto `print()` (interfaz de `Shape`)  en  `operator<<()` (o viceversa), para evitar duplicidad de código.
{% endhint %}

***

## Actividad 12a: Declaración de la clase Circle&#x20;

Desde nuestro directorio de trabajo, crea con vim el fichero de cabeceras `Circle.h`. Aquí tienes una plantilla:

```cpp
#include <iostream>
#include "Shape.h"

class Circle : public Shape {
    // ...
};
```

{% hint style="warning" %}
Recuerda que **debes declarar las funciones abstractas heredadas de `Shape`**, para poder implementarlas. Usa la directiva **`override`** para prevenir posibles errores de programación.
{% endhint %}

Comprueba que la sintaxis es correcta, y finalmente añade el fichero al repositorio git.

***

## Actividad 12b: Implementación de la clase Circle

Desde nuestro directorio de trabajo, crea con vim el fichero de código fuente `Circle.cpp`, de acuerdo con la especificación del fichero de cabeceras `Circle.h`.&#x20;

{% hint style="warning" icon="head-side-brain" %}
Recuerda implementar las funciones virtuales puras heredadas de `Shape` y declaradas en el `.h`!
{% endhint %}

{% hint style="info" icon="pi" %}
Usa la función  [`pow()`](https://es.cppreference.com/w/cpp/numeric/math/pow)de la librería [`<cmath>`](https://en.cppreference.com/w/cpp/header/cmath).&#x20;

Recuerda que $$\pi = 3.141592$$.
{% endhint %}

Añade al fichero `Makefile` la regla de compilación pertinente. Corrige los errores de compilación, en caso necesario, y añade los cambios de ambos ficheros al repositorio git.&#x20;

***

## Actividad 13: Depuración de la clase Circle

Desde nuestro directorio de trabajo, crea con vim el fichero de código fuente `testCircle.cpp`, con el siguiente contenido:

```cpp
#include <iostream>
#include "Circle.h"
#include "Point2D.h"

int main(){
    Circle c1;
    Circle c2("green", Point2D(1,1), 2);
    std::cout << "c1 = " << c1 << std::endl;
    std::cout << "c2 = " << c2 << std::endl; 
    std::cout << std::endl;

    c1.set_center(c2.get_center());
    c1.set_radius(c2.get_radius());
    c2.set_color("blue");

    std::cout << "c1 = " << c1 << std::endl;
    std::cout << "c2 = " << c2 << std::endl;
} 

```

A continuación, añade esta regla a tu `Makefile` para generar el binario ejecutable (se guardará en el directorio `bin`):

```makefile
bin/testCircle: testCircle.cpp Circle.o Shape.o Point2D.o
        g++ -c testCircle.cpp
        mkdir -p bin
        g++ -o bin/testCircle testCircle.o Circle.o Shape.o Point2D.o
```

{% hint style="info" %}
Notar como `testCircle` no solo depende de `Circle.o`, también de `Shape.o` y `Point2D.o`.
{% endhint %}

Finalmente, ejecuta el binario para comprobar que tu implementación es correcta:

```bash
./bin/testCircle
```

Debería generar una salida como esta:

```
c1 = [Circle: color = red; center = (0,0); radius = 1]
c2 = [Circle: color = green; center = (1,1); radius = 2]

c1 = [Circle: color = red; center = (1,1); radius = 2]
c2 = [Circle: color = blue; center = (1,1); radius = 2]
```

Si la semántica de tu salida es diferente, revisa tu código.&#x20;

Finalmente, añade `testCircle.cpp` y `Makefile` y haz un _commit_ con git.
