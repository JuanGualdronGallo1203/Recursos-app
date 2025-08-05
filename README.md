# 📚 Proyecto MongoDB: Base de Datos Estática de Recursos Multimedia

Este proyecto implementa una **base de datos estática en MongoDB**, cuyo objetivo es representar y estructurar información multimedia (libros, películas, series, usuarios y géneros) usando archivos `.json`. Está pensada para fines educativos, demostrativos o como base para futuros desarrollos, **sin conexión a una aplicación funcional**.

---

## 🧩 Tecnologías Utilizadas

- **MongoDB** – Base de datos NoSQL orientada a documentos.
- **JSON** – Formato ligero de intercambio de datos.
- **MongoDB Compass** *(opcional)* – Herramienta gráfica para explorar la base de datos.

---

## 📂 Estructura de Archivos

📦 recursos-multimedia
├── generos.json
├── libros.json
├── peliculas.json
├── series.json
├── recursos.json
├── usuario.json
└── README.md

yaml
Copiar
Editar

Cada archivo `.json` contiene documentos independientes o relacionados entre sí a través de claves foráneas simuladas, como `genero_id`.

---

## 🧾 Descripción de Colecciones

### 📁 `generos.json`

Define los géneros disponibles (Ej: Acción, Romance, Fantasía).

| Campo           | Tipo     | Descripción                                  |
|------------------|----------|----------------------------------------------|
| id_genero        | String   | ID único del género                         |
| nombre_genero    | String   | Nombre del género                           |
| descripcion      | String   | Descripción del género                      |
| popularidad      | String   | Nivel de popularidad (Alta, Media, Baja)    |
| target           | String   | Público objetivo                            |

---

### 📚 `libros.json`

Representa los libros registrados en el sistema.

| Campo             | Tipo     | Descripción                                  |
|-------------------|----------|----------------------------------------------|
| id_libro          | String   | ID único del libro                           |
| titulo            | String   | Título del libro                             |
| autor             | String   | Autor del libro                              |
| anio_publicacion  | Number   | Año de publicación                           |
| genero_id         | String   | Relación con `generos.id_genero`             |
| disponible        | Boolean  | Indica si el libro está disponible           |
| formato           | String   | Físico o Digital                             |
| editorial         | String   | Nombre de la editorial                       |

---

### 🎬 `peliculas.json`

Películas disponibles con sus respectivos datos.

| Campo         | Tipo     | Descripción                                  |
|---------------|----------|----------------------------------------------|
| id_pelicula   | String   | ID único de la película                      |
| titulo        | String   | Nombre de la película                        |
| director      | String   | Director de la película                      |
| anio_estreno  | Number   | Año de estreno                               |
| genero_id     | String   | Relación con `generos.id_genero`             |
| plataforma    | String   | Plataforma (Netflix, HBO, etc.)              |
| estado        | String   | Estado de visualización (Vista, Pendiente)   |

---

### 📺 `series.json`

Series disponibles por género, plataforma y estado.

| Campo        | Tipo     | Descripción                                   |
|--------------|----------|-----------------------------------------------|
| id_serie     | String   | ID único de la serie                          |
| titulo       | String   | Título de la serie                            |
| temporadas   | Number   | Número de temporadas                          |
| capitulos    | Number   | Número total de capítulos                     |
| genero_id    | String   | Relación con `generos.id_genero`              |
| plataforma   | String   | Plataforma donde se transmite                 |
| estado       | String   | En progreso, Terminada, Pendiente, etc.       |

---

### 🗃️ `recursos.json`

Agrupación general de recursos para categorización unificada.

| Campo         | Tipo     | Descripción                                  |
|---------------|----------|----------------------------------------------|
| id_recurso    | String   | ID único del recurso                         |
| nombre        | String   | Nombre del recurso                           |
| tipo          | String   | Tipo: Libro, Serie, Película                 |
| formato       | String   | Físico, Digital, Streaming                   |
| estado        | String   | Terminado, En Progreso, Pendiente            |
| plataforma    | String   | Plataforma (si aplica)                       |
| genero_id     | String   | Relación con `generos.id_genero`             |

---

### 👤 `usuario.json`

Usuarios que han interactuado con los recursos.

| Campo           | Tipo     | Descripción                                  |
|------------------|----------|----------------------------------------------|
| id_usuario       | String   | ID único del usuario                         |
| nombre           | String   | Nombre completo del usuario                  |
| correo           | String   | Correo electrónico del usuario               |
| recursos_vistos  | Array    | Lista de `id_recurso` vistos por el usuario |
| pendientes       | Array    | Lista de recursos que el usuario desea ver  |

---

## ⚙️ Uso con MongoDB

### 1. Crear base de datos y colecciones (desde terminal)

```bash
mongo
use recursos_multimedia
2. Importar archivos .json (estáticos)
bash
Copiar
Editar
mongoimport --db recursos_multimedia --collection generos --file generos.json --jsonArray
mongoimport --db recursos_multimedia --collection libros --file libros.json --jsonArray
mongoimport --db recursos_multimedia --collection peliculas --file peliculas.json --jsonArray
mongoimport --db recursos_multimedia --collection series --file series.json --jsonArray
mongoimport --db recursos_multimedia --collection recursos --file recursos.json --jsonArray
mongoimport --db recursos_multimedia --collection usuario --file usuario.json --jsonArray
🔎 Consultas de Ejemplo
Estas consultas pueden ejecutarse en MongoDB Compass o en Mongo Shell.

Libros disponibles:
js
Copiar
Editar
db.libros.find({ disponible: true })
Series en Netflix que están en progreso:
js
Copiar
Editar
db.series.find({ estado: "En Progreso", plataforma: "Netflix" })
Unir recursos con su género:
js
Copiar
Editar
db.recursos.aggregate([
  {
    $lookup: {
      from: "generos",
      localField: "genero_id",
      foreignField: "id_genero",
      as: "genero_detalle"
    }
  }
])
✅ Notas Importantes
Este proyecto no realiza validaciones automáticas, ya que no está conectado a una aplicación funcional.

Su propósito es simular la estructura de una base de datos multimedia con relaciones implícitas por claves.

Útil para pruebas, educación o punto de partida para futuros sistemas con backend.

📝 Licencia
Este proyecto está disponible bajo la licencia MIT.

✉️ Contacto
Desarrollado por Cristian Pérez y Juan Sebastian Gualdron

