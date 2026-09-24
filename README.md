# 🧪 API Testing – Restful-Booker

Proyecto de práctica de **QA / Testing de APIs** sobre la API pública [Restful-Booker](https://restful-booker.herokuapp.com/apidoc/index.html), una API REST de reservas de hotel creada específicamente para que testers practiquen pruebas de CRUD, autenticación y manejo de errores.

## 🎯 Objetivo

Diseñar y ejecutar un conjunto de pruebas de API que cubran:
- Autenticación (casos positivos y negativos)
- Operaciones CRUD completas sobre el recurso `booking`
- Validación de respuestas (status code, estructura del body, datos devueltos)
- Casos negativos: datos inválidos, IDs inexistentes, peticiones sin autenticación

## 🛠️ Herramientas

- **Postman** – diseño, ejecución y automatización de las pruebas (scripts en JavaScript dentro de cada request)
- **Restful-Booker API** – https://restful-booker.herokuapp.com

## 📁 Estructura del proyecto

```
├── Restful-Booker.postman_collection.json   # Colección de Postman con las 12 pruebas
└── README.md
```

## 🔍 Casos de prueba incluidos

| # | Endpoint | Método | Tipo | Qué valida |
|---|----------|--------|------|------------|
| 1 | `/ping` | GET | Positivo | La API está disponible (health check) |
| 2 | `/auth` | POST | Positivo | Genera token con credenciales válidas |
| 3 | `/auth` | POST | Negativo | Rechaza credenciales inválidas |
| 4 | `/booking` | POST | Positivo | Crea una reserva y devuelve `bookingid` |
| 5 | `/booking/:id` | GET | Positivo | Devuelve los datos correctos de la reserva creada |
| 6 | `/booking` | GET | Positivo | Devuelve el listado completo de IDs |
| 7 | `/booking/:id` | PUT | Positivo | Actualiza la reserva completa (con token) |
| 8 | `/booking/:id` | PATCH | Positivo | Actualiza parcialmente la reserva (con token) |
| 9 | `/booking/:id` | DELETE | Positivo | Elimina la reserva (con token) |
| 10 | `/booking` | POST | Negativo | Envía datos inválidos (campo vacío, tipo incorrecto) |
| 11 | `/booking/:id` | GET | Negativo | Consulta un ID que no existe → espera 404 |
| 12 | `/booking/:id` | DELETE | Negativo | Intenta borrar sin token → espera 403 |

Cada request incluye asserts automáticos en la pestaña **Tests** de Postman (status code + validación del body), y las variables `token` y `bookingId` se generan y reutilizan automáticamente entre requests gracias a variables de colección.

## ▶️ Cómo ejecutar este proyecto

1. Descarga [Postman](https://www.postman.com/downloads/) (o usa la versión web).
2. Importa el archivo `Restful-Booker.postman_collection.json` (`Import` → arrastra el archivo).
3. Abre la carpeta **02 - Autenticación** y ejecuta primero **POST Create Token** — esto guarda el token que usan las demás pruebas.
4. Ejecuta **03 - Booking CRUD** en orden (Create → Get → Update → Patch → Delete), ya que cada request depende del `bookingId` generado por el anterior.
5. Corre **04 - Casos Negativos** para ver cómo responde la API ante escenarios inválidos.
6. También puedes correr toda la colección de una vez con **Runner** (botón "Run collection").

## 📌 Resultados / Hallazgos
Las pruebas fueron ejecutadas utilizando Postman sobre la API pública Restful-Booker. Se validaron los principales flujos de autenticación y operaciones CRUD sobre el recurso booking, además de diferentes escenarios negativos.

Resultados generales
- ✅ Health check: el endpoint /ping permite comprobar la disponibilidad de la API.
- ✅ Autenticación: se validó la generación de un token utilizando credenciales válidas.
- ✅ CRUD de reservas: se validaron las operaciones de creación, consulta, actualización y eliminación de una reserva.
- ✅ Validación de respuestas: se utilizaron assertions de Postman para comprobar códigos de estado HTTP y datos relevantes del body.
- ✅ Manejo de IDs inexistentes: se verificó el comportamiento de la API al consultar una reserva que no existe.
- ✅ Autenticación en operaciones protegidas: se validó el uso del token para las operaciones que requieren autorización.
- ⚠️ Casos negativos: se realizaron pruebas con credenciales inválidas, datos incorrectos y solicitudes sin autenticación para identificar cómo responde la API ante entradas no válidas.

## Observaciones

Durante la ejecución se deben registrar los comportamientos que difieran de lo esperado según la documentación de la API. Cualquier respuesta inesperada será documentada como un posible defecto, indicando el endpoint, datos enviados, respuesta obtenida, código HTTP y comportamiento esperado.

## 🙋 Autor

Proyecto de práctica personal para portafolio de QA — Juan Esteban Rivera
