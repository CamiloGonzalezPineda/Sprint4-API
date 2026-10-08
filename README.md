# API Testing — Urban Grocers

Proyecto de pruebas de API REST desarrollado durante el Sprint 4 de mi formación como QA Engineer en TripleTen.

Durante este sprint trabajé en un proyecto de **pruebas de API REST** sobre **Urban Grocers**, utilizando principalmente **Postman** y **Swagger** para diseñar, ejecutar y analizar solicitudes HTTP y sus respuestas.

---

## Descripción del proyecto

El objetivo del proyecto fue diseñar y ejecutar casos de prueba para validar el comportamiento de diferentes endpoints de la API de Urban Grocers.

Se trabajó con escenarios positivos y negativos, aplicando diferentes técnicas de diseño de pruebas y validando tanto las solicitudes como las respuestas obtenidas.

Durante el proyecto se realizaron pruebas sobre:

- Parámetros de las solicitudes.
- Tipos de datos.
- Estructuras de los cuerpos JSON.
- Códigos de estado HTTP.
- Mensajes de error.
- Valores límite.
- Autenticación y autorización.
- Comparación entre resultados esperados y resultados actuales.
- Identificación y documentación de defectos.
- Análisis de posibles causas raíz.

---
---

## 📊 Evidencia de casos de prueba

Los casos de prueba, resultados de ejecución y documentación correspondiente al proyecto se encuentran en el siguiente archivo:

📄 **[Casos de prueba — Urban Grocers (Excel)](https://docs.google.com/spreadsheets/d/1W8Kjz6eQOWPSmVZ2HZkRyXPO1lS8Zpy4/edit?usp=sharing&ouid=106691349693826056792&rtpof=true&sd=true)**

El archivo contiene los casos diseñados para los módulos:

- UG-1 — Grocery Bundles
- UG-2 — Delivery Services
- UG-3 — Shopping Cart

Incluye información sobre:

- ID del caso de prueba.
- Precondiciones.
- Datos de prueba.
- Pasos de ejecución.
- Resultado esperado.
- Resultado actual.
- Estado de la prueba.
- Bugs asociados.

---

## Herramientas utilizadas

- **Postman** — Diseño y ejecución de solicitudes API.
- **Swagger** — Consulta y análisis de la documentación de la API.
- **REST API** — Servicios web utilizados durante las pruebas.
- **HTTP** — Métodos y códigos de respuesta.
- **JSON** — Estructuración de requests y responses.
- **Git & GitHub** — Control de versiones y documentación del proyecto.

---

## Módulos probados

### UG-1 — Grocery Bundles

Se realizaron pruebas sobre la funcionalidad relacionada con la incorporación de productos a un grocery bundle.

**Endpoint principal:**

```text
POST /api/v1/grocery-bundles/{groceryBundleId}/products
```

Se validaron diferentes escenarios, entre ellos:

- Agregar un producto existente a un grocery bundle.
- Agregar 29 productos con IDs únicos.
- Agregar 30 productos con IDs únicos.
- Intentar agregar 31 productos con IDs únicos.
- Utilizar un `productId` inexistente.
- Utilizar un `groceryBundleId` inexistente.
- Enviar una estructura incorrecta en `productsList`.
- Enviar `quantity = 0`.
- Omitir un parámetro obligatorio.

### Boundary Value Analysis

Se aplicó **Boundary Value Analysis (BVA)** para validar el límite máximo de productos permitido:

```text
29 → válido
30 → válido
31 → inválido
```

Este conjunto permite comprobar el valor inmediatamente inferior al límite, el límite exacto y el valor inmediatamente superior al límite.

Durante la ejecución también se identificaron y documentaron diferentes comportamientos incorrectos de la API.

---

### UG-2 — Delivery Services

Se realizaron pruebas sobre el cálculo del costo y tiempo de entrega.

**Endpoint principal:**

```text
POST /speedy/v1/calculate
```

Se validaron escenarios como:

- Solicitud válida.
- Límite inferior del horario de servicio.
- Valor por debajo del límite inferior.
- Límite superior del horario de servicio.
- Valor por encima del límite superior.
- Cantidad extrema de productos.
- Campo obligatorio ausente.
- Tipo de dato incorrecto.
- Estructura incorrecta del body.

### Boundary Value Analysis

Se aplicó **Boundary Value Analysis (BVA)** sobre el parámetro `deliveryTime`:

```text
6  → fuera del horario de servicio
7  → límite inferior
21 → límite superior
22 → fuera del horario de servicio
```

También se realizó un análisis de los resultados obtenidos para determinar cuándo diferentes escenarios podían estar relacionados con una misma causa raíz.

---

### UG-3 — Shopping Cart

Módulo opcional enfocado en las operaciones relacionadas con el carrito de compras.

Se realizaron pruebas sobre diferentes operaciones de la API, incluyendo:

- Creación de carritos.
- Consulta de carritos.
- Actualización de carritos.
- Eliminación de carritos.
- Validación de parámetros.
- Autenticación y autorización.

También se verificó el comportamiento de las solicitudes cuando no se proporcionaban las credenciales requeridas.

---

## Técnicas de diseño de pruebas

### Equivalence Partitioning

Se utilizaron clases de equivalencia para dividir los posibles valores de entrada en grupos representativos y seleccionar casos de prueba que permitieran obtener una cobertura adecuada.

### Boundary Value Analysis

Se utilizaron valores ubicados en los límites y alrededor de ellos para verificar el comportamiento de la API.

**Ejemplo — Grocery Bundles:**

```text
29 → válido
30 → válido
31 → inválido
```

**Ejemplo — Delivery Services:**

```text
6  → inválido
7  → válido
21 → válido
22 → inválido
```

---

## Ejemplo de solicitud API

Ejemplo de solicitud utilizada para probar el servicio de entrega:

```json
{
  "products": [
    {
      "productId": 3,
      "quantity": 1
    }
  ],
  "deliveryTime": 9
}
```

La solicitud fue ejecutada mediante Postman y posteriormente se analizaron los datos de la respuesta obtenida.

---

##  Validaciones realizadas

Durante la ejecución de las pruebas se compararon los resultados esperados con los resultados actuales de la API.

Se validaron aspectos como:

- Código de estado HTTP.
- Estructura de la respuesta.
- Valores de los campos.
- Mensajes de error.
- Parámetros obligatorios.
- Tipos de datos.
- Estructuras de los objetos JSON.
- Valores límite.
- Comportamiento ante datos inválidos.
- Autenticación.
- Autorización.

---

## Reporte de defectos

Los comportamientos que no coincidían con los resultados esperados fueron documentados como defectos.

Los reportes incluyeron:

- ID del bug.
- Título.
- Precondiciones.
- Pasos para reproducir.
- Resultado esperado.
- Resultado actual.
- Severidad.
- Evidencia.

Uno de los aprendizajes importantes del proyecto fue comprender que diferentes escenarios que presentan comportamientos incorrectos pueden estar relacionados con una **misma causa raíz**.

Por esta razón, además de identificar los defectos, se realizó un análisis de los resultados para determinar cuándo diferentes fallos podían corresponder al mismo problema.

---

## Análisis de causa raíz

Durante el proyecto se identificaron diferentes escenarios que presentaban comportamientos incorrectos en el servicio de cálculo de entrega.

El análisis permitió determinar que varios de estos escenarios podían estar relacionados con una misma causa raíz.

Esto permitió consolidar los defectos relacionados y documentarlos de una manera más estructurada, evitando tratar cada comportamiento como un problema completamente independiente.

Este aprendizaje reforzó la importancia de analizar no solamente **qué está fallando**, sino también **por qué podría estar fallando**.

---

## Flujo de trabajo

El proceso seguido durante el proyecto fue:

1. Revisar los requisitos.
2. Analizar la documentación de Swagger.
3. Identificar los endpoints y parámetros.
4. Diseñar los casos de prueba.
5. Aplicar técnicas de diseño como Equivalence Partitioning y Boundary Value Analysis.
6. Configurar las solicitudes en Postman.
7. Ejecutar las pruebas.
8. Analizar las respuestas.
9. Comparar el resultado esperado con el resultado actual.
10. Identificar comportamientos incorrectos.
11. Documentar los bugs.
12. Analizar posibles causas raíz.

---

## Flujo de validación

```text
Requisitos
    ↓
Swagger
    ↓
Diseño de casos de prueba
    ↓
Configuración en Postman
    ↓
Ejecución
    ↓
Análisis de Response
    ↓
Expected vs Actual
    ↓
¿Comportamiento incorrecto?
    ↓
Documentación del bug
    ↓
Análisis de causa raíz
```

---

## Competencias desarrolladas

Durante este proyecto fortalecí mis conocimientos en:

- API Testing
- REST APIs
- Postman
- Swagger
- HTTP Methods
- HTTP Status Codes
- JSON
- Test Case Design
- Equivalence Partitioning
- Boundary Value Analysis
- Positive Testing
- Negative Testing
- Bug Reporting
- Root Cause Analysis
- Authentication
- Authorization
- Análisis de resultados
- Documentación de pruebas

---

## Principales aprendizajes

Este proyecto me permitió comprender que el trabajo de QA no consiste únicamente en ejecutar solicitudes y verificar si una respuesta es correcta.

También es necesario:

- Comprender los requisitos.
- Diseñar escenarios de prueba adecuados.
- Identificar valores límite.
- Validar diferentes tipos de entradas.
- Analizar las respuestas de la API.
- Diferenciar Expected Result y Actual Result.
- Documentar defectos de manera clara y reproducible.
- Analizar patrones entre diferentes fallos.
- Buscar posibles causas raíz.

El proyecto permitió fortalecer una metodología de trabajo más estructurada y analítica para la ejecución de pruebas de API.

---

## Contenido del repositorio

Este repositorio contiene los materiales utilizados durante el proyecto:

- Colección de Postman.
- Casos de prueba.
- Reportes de bugs.
- Evidencias de ejecución.
- Documentación del proyecto.

---

## Autor

**Camilo González**

QA Engineer — En formación

### Áreas de interés

- Manual Testing
- API Testing
- QA Automation
- Cypress
- Postman
- Software Testing

---

## Formación

**TripleTen — QA Engineering**

**Sprint 4 — API Testing**