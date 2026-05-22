# Clase Point2D

### Descripción de la clase <a href="#descripcion-de-la-clase" id="descripcion-de-la-clase"></a>

El tipo de datos `Point2D`, que representa un punto bidimensional en el espacio cartesiano, estará definido por una clase concreta de igual nombre.

#### Atributos <a href="#atributos" id="atributos"></a>

| `public` | `double x` | Coordenada x |
| -------- | ---------- | ------------ |
| `public` | `double y` | Coordenada y |

#### Métodos <a href="#metodos" id="metodos"></a>

| `public` | `Point2D(double x=0, double y=0)`                               | Método constructor. Por defecto, los ejes tomarán el valor 0.                             |
| -------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `public` | `static double distance(const Point2D &a, const Point2D &b)`    | Calcula la distancia euclidiana entre dos puntos `a` y `b`.                               |
| `public` | `bool operator==(const Point2D &a, const Point2D &b)`           | Sobrecarga global del operador `==`. Comprueba si dos puntos son iguales.                 |
| `public` | `bool operator!=(const Point2D &a, const Point2D &b)`           | Sobrecarga global del operador `!=`. Comprueba si dos puntos son diferentes.              |
| `public` | `std::ostream& operator<<(std::ostream &out, const Point2D &p)` | Sobrecarga global del operador `<<`. Recuerda incluir la cabecera `<ostream>` en el `.h`. |

| fff | ww  | ccc |
| --- | --- | --- |
| asd | asd | asd |
|     | asd | asd |
|     |     |     |
