# RA5 · Projecte Fase 3 · SpawnCamp

## 1. Part A — Conversió manual del JSON

**Convertidor utilitzat:** W3Schools XML to JSON: https://www.w3schools.com/tools/tool_xml_json.php

<img width="600" height="351" alt="Captura de la Part A" src="https://github.com/user-attachments/assets/2462105b-cdd1-430b-bb02-856ecb640cfa" />

## 2. Part B — Conversió automàtica

<img width="630" height="259" alt="Captura de la Part B" src="https://github.com/user-attachments/assets/9a77fce3-17cf-4c25-a3d4-7da1c685b280" />

## 3. Decisions de la Part B — casos del joc RET-002

- **Diferència 1 (números com a text):** en tots els jocs, per exemple `"Precio": "35.99"` i `"Stock": "11"`; el convertidor els va passar com a string i en el meu són nombres enters (`35.99`, `11`).

- **Diferència 2 (atributs amb símbol):** el convertidor va posar tots els IDs dels jocs així: `"@id"`.

- **Diferència 3 (llista d'un sol element):** RET-001 té `"Plataforma": "SNES"` sense llista.

- **Número o text:** `id` i `fecha` els he utilitzat com a string perquè són textos; i per a `precio`, `valoracion` i `stock` he utilitzat numbers perquè són valors numèrics i es fan càlculs amb ells.

- **Retorn XML:** `id` i `comentario` passen d'atributs a elements; no hi ha arrel nova, queda `<tienda>` i vuit `<juegos>` sols; les llistes es repeteixen sense contenidor i es perden DOCTYPE, comentaris, CDATA i els zeros finals (`41.90` passa a `41.9`).

- **Valida amb el DTD? No:** el DTD defineix `id` com a atribut obligatori de `Juego` (`ATTLIST Juego id ID #REQUIRED`) i aquí és un element fill de `<juegos>`; a més faltan `Catalogo` i l'arrel `Tienda`.

- **Errors de sintaxi (Part D):** 6 errors de 4 tipus: 1 de cometes simples (`'codi'`), 1 clau sense cometes (`plataformes`), 1 comentari (`// preu sense IVA`) i 3 comes (1 que faltava després de `estoc` i 2 sobrants).

- **Error que el validador no detecta:** `"preu": "24.99"` era text i havia de ser número.

## 4. Part E — Mostrar JSON en HTML

- La funció que pinta cada targeta està a `Js/cataleg_json.js` i es diu `crearTarjeta(juego)`. Genera un `article` amb el títol, la imatge, els gèneres, les plataformes, el preu, la valoració i l'stock.
- Si es carrega `cataleg_convertidor.json`, `JSON.parse` funciona, però l'estructura no coincideix amb la que espera la pàgina; llavors `validarDatos()` falla i la web mostra un missatge de “estructura no compatible” en lloc de dibuixar targetes.
