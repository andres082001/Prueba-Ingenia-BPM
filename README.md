# Prueba-Ingenia-BPM

Solución al estudio de caso técnico de INGENIA BPM: Directorio de Estudiantes EDUCIT.

## Descripción

Este proyecto consiste en un directorio de estudiantes que consume la API pública de
JSONPlaceholder para listar usuarios. Se entregó con 3 bugs y una funcionalidad
incompleta, los cuales fueron corregidos según se detalla a continuación.

## Errores encontrados y solución

- **Bug 1 (CSS):** El botón usaba la clase `btn-primary` en el HTML, pero en el CSS
  estaba declarada como `.btn-primery` por un error de tipeo. Como los nombres no
  coincidían, el navegador nunca aplicaba el estilo. Corregí el selector en el CSS
  para que coincida exactamente con la clase del botón.

- **Bug 2 (mapeo de datos del JSON):** El código intentaba leer las propiedades
  `user.full_name` y `user.email_address`, pero la API de JSONPlaceholder en realidad
  devuelve esos datos como `user.name` y `user.email`. Por eso no se mostraba ninguna
  información (las propiedades eran `undefined`). Corregí las referencias para usar
  los nombres reales de las propiedades del objeto.

- **Bug 3 (Lógica SQL):** La consulta original tenía dos problemas: de sintaxis,
  declaraba dos columnas (`nombre, correo`) pero solo pasaba un valor (`userName`); y
  de seguridad, al concatenar variables directamente en el SQL se exponía la
  aplicación a inyección SQL. Corregí la consulta usando parámetros preparados:

```sql
  INSERT INTO estudiantes (nombre, correo) VALUES (?, ?);
```

  Los valores (`userName`, `userEmail`) se pasan por separado en lugar de
  incrustarlos directamente en el string del query, lo cual evita que un usuario
  malicioso pueda inyectar código SQL a través del nombre o el correo.

## Funcionalidad agregada

- **Buscador en tiempo real:** Agregué un input de texto que filtra la lista de
  estudiantes por nombre mientras se escribe, sin recargar la página. Los usuarios
  se guardan en memoria (`allUsers`) cuando se cargan por primera vez, de modo que el
  filtro se aplica directamente sobre esa lista local en cada tecla, sin necesidad
  de volver a llamar a la API.

## Tecnologías utilizadas

- HTML5
- CSS3
- JavaScript (Vanilla)
- API pública: [JSONPlaceholder](https://jsonplaceholder.typicode.com/)

