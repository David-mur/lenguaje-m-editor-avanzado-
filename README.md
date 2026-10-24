# lenguaje-m-editor-avanzado-

## 1. ¿Qué hace exactamente el bloque let.... in en el lenguaje M?
   El bloque let desarrolla los pasos que van cambiando lo que está allí en el momento, y finalmente el in indica que aplique todos esos cambios y muestre cómo queda al final. Cada paso DEPENDE y USA lo que había en el anterior paso paea transformar desde ahí.

## 2. ¿Por qué el lenguaje M es Case Sensitive?
   Porque es un lenguaje donde se entiende estrictamente que los caracteres usados para una palabra reservado son los que requiere el lenguaje, por lo que se debe ceñir a usar mayusuculas donde éstas deban ir.
   Un ejemplo de las consecuencias de un mal uso es:
   * **Consecuencia en código:** Escribir `table.transformcolumns` en lugar de `Table.TransformColumns` genera un error inmediato de compilación porque el motor no reconoce el nombre de la función en minúsculas.


## 3. ¿Cuál es la diferencia entre usar `Text.Trim` y `Text.Clean` en M?
`Text.Trim` se especializa exclusivamente en remover los espacios en blanco sobrantes situados al inicio y al final de una cadena de texto (por ejemplo, transformar `" Laptop Pro 15 "` en `"Laptop Pro 15"`). Por el contrario, `Text.Clean` está diseñado para eliminar caracteres de control no imprimibles o invisibles que puedan encontrarse incrustados en medio o al final de los textos (como saltos de línea o tabulaciones).

## 4. ¿Por qué filtraste los registros "PRUEBA" después de estandarizar la categoría y no antes?
Porque los datos de origen contenían variaciones inconsistentes en las mayúsculas (como `"PRUEBA"`, `"prueba"` o `"Prueba"`). Si se hubiera intentado aplicar el filtro `[categoria] <> "Prueba"` antes de la estandarización, las variantes en minúsculas o mayúsculas completas no habrían coincidido con el texto exacto del filtro y habrían permanecido en el reporte final. Al estandarizar primero toda la columna a *Title Case* mediante `Text.Proper`, todos los registros de prueba se unifican de forma homogénea en `"Prueba"`, permitiendo su exclusión limpia y centralizada en un solo paso
   
