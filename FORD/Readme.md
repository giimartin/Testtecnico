## Descripción general

Este documento detalla el proceso de transformación y limpieza aplicado al archivo Proveedor FORD, con el objetivo de obtener un dataset estructurado, limpio y estandarizado para análisis o uso posterior.

## Proceso de preparación y carga

- Se creó una copia del archivo original en Google Drive para trabajar sobre ella sin modificar el archivo fuente.  
- El archivo fue abierto en Google Sheets para facilitar la manipulación y limpieza.

## Procesamiento y limpieza de datos

1. **Verificación de filas vacías:**  
   Se revisó que no existieran filas vacías para mantener una estructura tabular continua y evitar inconsistencias.

2. **Eliminacion de espacios en columna codigos:**  
    `=REGEXREPLACE(A2, "\s+", "")`

3. **Eliminación de fórmulas:**  
   Para garantizar que el archivo contenga solo valores estáticos y evitar dependencias, se copiaron todas las celdas con fórmulas (Ctrl + C) y se pegaron solo los valores utilizando pegado especial (Ctrl + Mayús + V).

4. **Configuración regional:**  
   Se ajustó la configuración regional en Google Sheets a “Argentina” para asegurar el correcto manejo de formatos numéricos y monetarios.  
   *(Menú: Archivo > Configuración > Configuración regional > Argentina)*  

5. **Control de encabezados:**  
   Se añadieron los nombres de columna conforme al formato modelo proporcionado, facilitando la interpretación y manipulación de los datos.

6.  **colocacion formato: "texto sin formato**
    Antes de ejecutar el script de limpieza, se seleccionaron todas las columnas afectadas y se estableció su formato como “Texto sin formato” para evitar que Google Sheets interpretara automáticamente caracteres especiales o codificaciones como fórmulas, fechas u otros tipos de datos.
    (Menú: Formato > Número > Texto sin formato)  

7. **Eliminación de caracteres especiales en columnas A, B y C (script):**  
   Se detectaron símbolos no deseados como `╝`, `┤`, y caracteres codificados como `\xE2\x96\x84` y `\xE2\x96\x92` que afectaban la calidad del dataset.  
   Para eliminarlos de manera automatizada en las tres primeras columnas (A, B y C), se implementó el siguiente script en Google Apps Script:

   ```javascript
   function limpiarCaracteres() {
     const hoja = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     const rango = hoja.getDataRange();
     const valores = rango.getValues();

     // Caracteres a eliminar
     const charsAEliminar = [
       "╝",
       "┤",
       "\u2584",  // Unicode equivalente a \xE2\x96\x84
       "\u2592"   // Unicode equivalente a \xE2\x96\x92
     ];

     function limpiarTexto(texto) {
       if (typeof texto !== 'string') return texto;
       let limpio = texto;
       charsAEliminar.forEach(c => {
         const re = new RegExp(c, 'g');
         limpio = limpio.replace(re, '');
       });
       return limpio;
     }

     const colsALimpiar = [0, 1, 2]; // Columnas A, B y C

     for (let i = 0; i < valores.length; i++) {
       colsALimpiar.forEach(col => {
         valores[i][col] = limpiarTexto(valores[i][col]);
       });
     }

     rango.setValues(valores);
   }

8. **Formato a moneda en columna precios y ordenamiento de mayor a menor:**  
   La tabla fue ordenada en orden descendente según los valores de precio para optimizar la visualización y el análisis.  
   *(Seleccionar la columna c > Menú Datos > Ordenar intervalo por columna "c" Z → A)*

9. **Formato visual:**  
    Se aplicaron formatos visuales para mejorar la presentacion


# Atajos y tips usados

- **Ctrl + A:** Seleccionar todo el rango activo (presionar dos veces para seleccionar toda la hoja).  
- **Ctrl + Shift + ↓:** Seleccionar todas las celdas hacia abajo desde la celda activa.  
- **Ctrl + C:** Copiar celdas seleccionadas.  
- **Ctrl + X:** Cortar celdas seleccionadas.  
- **Ctrl + Mayús + V:** Pegado especial — Pegar solo valores, sin fórmulas ni formatos.  
- **Ctrl + Z:** Deshacer última acción.  

---

- **Datos > Crear filtro:** Para aplicar filtros personalizados en columnas.  
- **Filtro por condición > Está vacío:** Para detectar y eliminar filas vacías.  
- **Datos > Ordenar intervalo por columna "D" Z → A:** Para ordenar datos de mayor a menor según la columna D.  
- **Archivo > Configuración > Configuración regional > Argentina:** Para ajustar formatos numéricos y monetarios regionales.  

---
- **Extensiones > Apps Script:** Para ejecutar scripts personalizados que automatizan tareas como limpieza masiva de caracteres o manipulación de datos.

---

## Fórmulas para eliminar espacios en Google Sheets

- Para eliminar todos los espacios (normales y especiales) en toda la columna A (desde A2 hacia abajo), usando `ARRAYFORMULA`:

```excel
=ARRAYFORMULA(REGEXREPLACE(A2:A; "\s+"; ""))
