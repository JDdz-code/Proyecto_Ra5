# RA5 · Projecte Fase 3 · SpawnCamp 
- **Convertidor:** W3Schools XML to JSON, https://www.w3schools.com/tools/tool_xml_json.php

- **Decisiones de la Parte B: Todos los casos en el juego RET-002**

    - **Diferencia 1 (números como texto):** en todos los juegos, p. ej. RET-001 `"Precio": "35.99"` y `"Stock": "11"`; el convertidor los pasó como string y en el mío son números enteros (`35.99`, `11`).

    - **Diferencia 2 (atributos con símbolo):** el convertidor puso todos los IDs de los juegos así: `"@id"`.

    - **Diferencia 3 (lista de un elemento):** RET-001 tiene `"Plataforma": "SNES"` sin lista.

    - **Número o texto:** `id` y `fecha` los he utilizado como string porque son textos, y para `precio`, `valoracion` y `stock` utilicé integers porque son números y se hacen cálculos con ellos.

- **Retorno XML:** `id` y `comentario` pasan de atributos a elementos; no hay raíz nueva, queda `<tienda>` y ocho `<juegos>` sueltos; las listas se repiten sin contenedor y se pierden DOCTYPE, comentarios, CDATA y los ceros finales (`41.90` pasa a `41.9`).

- **¿Valida con el DTD? No:** el DTD define `id` como atributo obligatorio de `Juego` (`ATTLIST Juego id ID #REQUIRED`) y aquí es un elemento hijo de `<juegos>`; además faltan `Catalogo` y la raíz `Tienda`.

- **Errores de sintaxis (Parte D):** 6 errores de 4 tipos: 1 de comillas simples (`'codi'`), 1 clave sin comillas (`plataformes`), 1 comentario (`// preu sense IVA`) y 3 de comas (1 que faltaba tras `estoc` y 2 sobrantes).

- **Error que el validador no detecta:** `"preu": "24.99"` era texto y debe ser número.

## Parte E — Mostrar JSON en HTML

- La función que pinta cada tarjeta está en `Js/cataleg_json.js` y se llama `crearTarjeta(juego)`. Genera un `article` con el título, imagen, géneros, plataformas, precio, valoración y stock.
- Si se carga `cataleg_convertidor.json`, `JSON.parse` sí funciona, pero la estructura no coincide con la esperada por la página; entonces `validarDatos()` falla y la web muestra un mensaje de “estructura no compatible” en lugar de dibujar tarjetas.

