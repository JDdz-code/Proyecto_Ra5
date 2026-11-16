# RA5 · Projecte Fase 3 · SpawnCamp 
- **Número o texto:** `id` ("RET-001") es texto porque es un identificador y no se calcula con él; `fecha` es texto porque JSON no tiene tipo fecha; `precio`, `valoracion` y `stock` son números porque se operan con ellos (IVA con dos decimales, comprobar si el stock es menor que 5).
- **Decisiones de la Parte A:** los saltos de línea del CDATA de `descripcion_tienda` quitados.`fecha_actualizacion` va dentro de `tienda` porque se elimina el nivel `Catalogo`; RET-003 y RET-006 no tienen clave `descripcion` porque en el XML ese elemento opcional (`Descripcion?` en el DTD) no existe, no está vacío.

- **Convertidor:** W3Schools XML to JSON, https://www.w3schools.com/tools/tool_xml_json.php
- **Diferencia 1 (números como texto):** en todos los juegos, p. ej. RET-001 `"Precio": "35.99"` y `"Stock": "11"`; en el mío son números (`35.99`, `11`).
- **Diferencia 2 (atributos con símbolo):** `"@id"` en todos los juegos y `"@comentario"` en RET-002; en el mío son `"id"` y `"comentario"`.
- **Diferencia 3 (lista de un elemento):** RET-001 tiene `"Plataforma": "SNES"` sin lista (también RET-003 con `"Genero"`); en el mío siempre `["SNES"]`.

- **Vuelta a XML:** `id` y `comentario` pasan de atributos a elementos, no hay raíz nueva (queda `<tienda>` y ocho `<juegos>` sueltos), las listas se repiten sin contenedor y se pierden DOCTYPE, comentarios, CDATA y los ceros finales (`41.90` pasa a `41.9`).
- **¿Valida con el DTD? No:** el DTD define `id` como atributo obligatorio de `Juego` (`ATTLIST Juego id ID #REQUIRED`) y aquí es un elemento hijo de `<juegos>`; además faltan `Catalogo` y la raíz `Tienda`.

- **Errores de sintaxis (Parte D):** 6 errores de 4 tipos: 1 de comillas simples (`'codi'`), 1 clave sin comillas (`plataformes`), 1 comentario (`// preu sense IVA`) y 3 de comas (1 que faltaba tras `estoc` y 2 sobrantes).
- **Error que el validador no detecta:** `"preu": "24.99"` era texto y debe ser número.