# KathWare JSONs

Datos públicos utilizados por las herramientas, catálogos y páginas de [KathWare](https://kathware.com.ar/).

**Este repositorio es un almacén de datos**, no un plugin de WordPress. Los lectores y componentes de presentación siguen siendo responsabilidad del sitio; subir un JSON no modifica automáticamente la página pública.

## Archivos actuales

| Archivo | Datos | Estructura |
| --- | --- | --- |
| [`frases.json`](./frases.json) | 114 frases de KathWare Dice | Arreglo de objetos `{ "texto", "autor" }` |
| [`apps.json`](./apps.json) | 69 aplicaciones en 11 categorías | `categorias`, `aplicaciones` |
| [`anuncios.json`](./anuncios.json) | 15 fichas de servicios, emprendimientos y recomendaciones | `categorias`, `anuncios` |
| [`colaboraciones.json`](./colaboraciones.json) | 6 formas de apoyar el sitio | `categorias`, `colaboraciones`, `contacto` |
| [`version.json`](./version.json) | Versiones independientes de los recursos | `recursos` |

Los datos de apps, anuncios y colaboraciones se transcribieron de los contenidos HTML utilizados en KathWare, conservando la identificación, el orden y las URLs de las fichas.

## Contrato de datos

- `id`: identificador estable de ficha; debe conservarse para no romper enlaces a fragmentos (por ejemplo `/apps/#softbraille`).
- `categoria`: identifica la sección a la que pertenece la ficha.
- `orden`: orden de publicación original, no aleatorio.
- `activa`: permite excluir una ficha de un catálogo o selección de promociones sin borrarla.
- `etiqueta` y `tipo`: identifican la clase de promoción y permiten generar sus rótulos accesibles.
- `contenido`: secuencia ordenada de bloques de tipo `parrafo` o `lista`; el campo `html` o cada elemento de lista puede contener HTML editorial básico (énfasis, enlaces, etc.). **El componente que los renderiza debe sanear el HTML y los atributos antes de mostrarlo.**
- `enlaces` (apps): conservan el texto descriptivo de cada enlace, su URL, apertura externa y relación `rel`.

Los datos bancarios de `colaboraciones.json` son públicos porque se publican para recibir aportes voluntarios. Revisarlos y mantenerlos actualizados antes de utilizarlos en una página.

## Versiones y caché

Consultar [`version.json`](./version.json). Cada recurso tiene su versión y fecha de última edición. **Al actualizar un JSON, cambiar también su versión en `version.json`.** Eso permite que los componentes web detecten una nueva publicación sin descargar repetidamente todos los catálogos.

Ejemplo de consulta (sin asumir que ya exista un lector de catálogos instalado en WordPress):

```js
const raiz = "https://raw.githubusercontent.com/dragonmoon1522/KathWare-Jsons/main/";
const manifiesto = await fetch(raiz + "version.json").then(r => {
  if (!r.ok) throw new Error("No se pudo cargar el manifiesto");
  return r.json();
});
const version = manifiesto.recursos.apps.version;
const catalogo = await fetch(raiz + "apps.json?v=" + encodeURIComponent(version))
  .then(r => {
    if (!r.ok) throw new Error("No se pudo cargar el catálogo");
    return r.json();
  });
```

Cuando el sistema de caché y los renderizadores estén listos, las páginas y los fragmentos de WPCode Lite podrán leer estos archivos sin modificar el tema Femina.

## Compatibilidad con KathWare Dice

`frases.json` conserva su esquema original: un arreglo de `{ "texto", "autor" }`. No se requiere modificar las frases para incorporar los nuevos catálogos.

## Antecedentes

Este repositorio nació como el proyecto de la antigua skill de Alexa «Pastillas Inspiradoras», que ya fue retirada. Se conservan algunos archivos de esa etapa por motivos históricos, **pero la skill no se mantiene ni forma parte de las funcionalidades actuales de KathWare**.

## Licencias

La reorganización del repositorio no cambia los derechos de autor ni las condiciones previas de los contenidos. Consultar [`LICENSE.md`](./LICENSE.md) y las atribuciones originales de cada recurso.
