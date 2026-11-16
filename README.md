# GS

## Comparació entre JSON propi i convertidor online

Hem comparat el nostre fitxer [Lenguaje_Marca/Xslt/Catalogo_json.json](Lenguaje_Marca/Xslt/Catalogo_json.json) amb el fitxer generat per un convertidor online [Lenguaje_Marca/Xslt/cataleg_convertidor.json](Lenguaje_Marca/Xslt/cataleg_convertidor.json).

### 1. Números convertits en text

Aquest error no apareix al nostre JSON ni al convertidor online en aquest cas, perquè `precio`, `valoracion` i `stock` estan com a nombres reals.

Exemple del nostre JSON:
```json
"precio": 35.99,
"valoracion": 9.1,
"stock": 11
```

Exemple del convertidor online:
```json
"Precio": 35.99,
"Valoracion": 9.1,
"Stock": 11
```

Conclusió: aquí no es comet el problema, ja que els nombres es mantenen correctes.

### 2. Atributs marcats amb símbols

Aquest és un error típic dels convertidors automàtics.

Exemples del convertidor online:
```json
"@_id": "RET-001",
"@_comentario": "Obra maestra del metroidvania.",
"@_Moneda": "&eur;",
"@_Fecha_actualizacion": "2025-09-08",
"@_estilo": "retro"
```

Aquests atributs tenen prefixos com `@_`, `@`, `_`, `-`, que no són valids segons les regles de conversió que hem establert.

En canvi, al nostre JSON ho hem convertit com a camps normals:
```json
"id": "RET-001",
"moneda": "euro",
"fecha": "1995-03-11"
```

Joc on apareix: `RET-001` i `RET-002` mostren aquest problema al convertidor online, perquè tenen atributs com `@_id` i `@_comentario`.

### 3. Llistes d'un sol element que no són llista

Aquest és el segon error habitual en convertidors automàtics.

Exemple del convertidor online:
```json
"Plataforma": "SNES"
```

En lloc de:
```json
"plataformas": ["SNES"]
```

I també passa amb `Genero`:
```json
"Genero": "Plataformas"
```

En lloc de:
```json
"generos": ["Plataformas"]
```

Jocs on apareix: `RET-003`, `RET-004`, `RET-005`, `RET-006`, `RET-008` tenen aquest problema en el convertidor online, perquè els elements repetits es guarden com a cadena simple quan només n'hi ha un.

### Com ho tenim nosaltres

Al nostre JSON, aquesta regla està corregida:

```json
"generos": ["RPG", "Aventura"]
"plataformas": ["SNES"]
```

I quan no hi ha descripció, ho representem com a `null`:

```json
"descripcion": null
```

### Conclusió

El convertidor online falla en dos dels tres errors típics:
- atributs amb `@`, `_` o `-`
- llistes d'un sol element mal representades

El nostre JSON no comet cap d'aquests errors i manté els nombres com a nombres reals, que és la manera correcta segons les regles de conversió establertes.

### Resum final

- Convertidor online: comete errors en atributs i llistes d'un sol element.
- JSON propi: correcte en aquests punts i segueix la normativa acordada.

