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

> Esta sección la completas tú después de correr la colección — es la parte que más valor le da al proyecto frente a un reclutador.

Ejemplo de cómo documentarlo:
- ✅ Los endpoints de autenticación y CRUD responden según lo documentado.
- ⚠️ El endpoint `/booking` con datos inválidos (`totalprice` como texto) devuelve `500 Internal Server Error` en lugar de un `400 Bad Request` — comportamiento a reportar como bug de la API.
- ✅ Las peticiones `PUT`/`PATCH`/`DELETE` sin token son correctamente rechazadas con `403`.

## 🙋 Autor

Proyecto de práctica personal para portafolio de QA — [tu nombre aquí]

