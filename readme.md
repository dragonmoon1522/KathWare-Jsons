# KathWare JSONs

Repositorio público de datos JSON utilizados por las herramientas de [KathWare](https://kathware.com.ar/).

Este repositorio comenzó como **Pastillas Inspiradoras**, el proyecto de frases para Alexa. La skill de Alexa ya no está en uso; los archivos de esa implementación se conservan como antecedentes históricos y no son necesarios para el funcionamiento de **KathWare Dice** en el sitio.

## Datos disponibles

| Archivo | Contenido |
| --- | --- |
| [`frases.json`](./frases.json) | Frases de KathWare Dice. Actualmente es un arreglo de objetos con los campos `texto` y `autor`. |
| [`version.json`](./version.json) | Manifiesto de versiones de los conjuntos de datos publicados. |
| [`version.md`](./version.md) | Historial histórico del proyecto original. |

Más adelante podrán incorporarse `apps.json` y `anuncios.json`, con su propia estructura y control de versiones.

## Formato de las frases

```json
[
  {
    "texto": "Ejemplo de una frase.",
    "autor": "Autor de la frase"
  }
]
```

El sitio selecciona una frase aleatoria del archivo y la presenta como texto, sin interpretar HTML. Los nombres de las propiedades `texto` y `autor` deben mantenerse para conservar la compatibilidad.

## Control de versiones de datos

`version.json` registra la versión de cada recurso. Por ejemplo:

```json
{
  "esquema": 1,
  "recursos": {
    "frases": {
      "archivo": "frases.json",
      "version": "1.3.3",
      "actualizado": "2026-03-19"
    }
  }
}
```

**Cuando se modifique `frases.json`, se debe actualizar también `recursos.frases.version` y la fecha**. El lector web puede comparar este número con la versión almacenada en el navegador y descargar las frases solo cuando cambien. Cada conjunto futuro podrá tener su propia versión independiente.

## Uso en KathWare

Los JSON son públicos y están destinados a ser consumidos por las páginas y componentes del sitio. Conviene usar las URL de la rama principal del repositorio para las cargas remotas y disponer de un comportamiento alternativo cuando falle la red.

La información se publica de forma independiente del código PHP, JavaScript o HTML que la presenta. Los componentes del sitio se mantienen en WPCode Lite y pueden consumir estos archivos sin necesidad de modificar el tema de WordPress.

## Licencias e historia

Consultar [`LICENSE.md`](./LICENSE.md) para el código y los documentos originales del repositorio. El contenido literario de las frases debe conservar sus créditos y condiciones de uso originales. Esta reorganización no modifica automáticamente sus licencias.

El código original de Alexa permanece en el historial y los archivos del repositorio solamente como referencia; **no forma parte de los componentes activos de KathWare**.
