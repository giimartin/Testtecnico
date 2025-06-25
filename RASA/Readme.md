## Descripción general

Este documento detalla el proceso de transformación y limpieza aplicado al archivo Proveedor RASA, con el objetivo de obtener un dataset estructurado, limpio y estandarizado para análisis o uso posterior.

## Proceso de preparación y carga

# Conversión y limpieza de archivo TXT a XLS - Flujo de trabajo

1. Descargar el archivo `.txt`.
2. Abrirlo con Microsoft Excel y utilizar el asistente de importación de texto para delimitar correctamente los datos y distribuirlos en columnas adecuadas.
3. Guardar el archivo en formato `.xls`.
4. Subir o abrir el archivo `.xls` en Google Sheets para continuar con la manipulación y limpieza de datos.

## Procesamiento y limpieza de datos

1. **Verificación de filas vacías:**  
   Se revisó que no existieran filas vacías para mantener una estructura tabular continua y evitar inconsistencias.

2. **Colocación formato "Texto sin formato":**  
   Antes de ejecutar el script de limpieza, se seleccionaron todas las columnas afectadas y se estableció su formato como “Texto sin formato” para evitar que Google Sheets interpretara automáticamente caracteres especiales o codificaciones como fórmulas, fechas u otros tipos de datos.  
   *(Menú: Formato > Número > Texto sin formato)*

3. **Configuración regional:**  
   Se ajustó la configuración regional en Google Sheets a “Argentina” para asegurar el correcto manejo de formatos numéricos y monetarios.  
   *(Menú: Archivo > Configuración > Configuración regional > Argentina)*

4. **Eliminación de caracteres especiales (script):**  
   Se detectaron caracteres no deseados en el dataset, incluyendo el símbolo codificado `\xe2\x86\x92` (que corresponde a la flecha →), y los caracteres `伃` y `厲`. Para asegurar la limpieza y calidad de los datos, se implementó un script en Google Apps Script que recorre toda la hoja y elimina estos caracteres de todas las celdas con texto.

```javascript
function limpiarCaracteres() {
  const hoja = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const rango = hoja.getDataRange();
  const valores = rango.getValues();

  // Caracteres a eliminar
  const caracteresABorrar = ['→', '伃', '厲'];

  for (let i = 0; i < valores.length; i++) {
    for (let j = 0; j < valores[i].length; j++) {
      if (typeof valores[i][j] === 'string') {
        caracteresABorrar.forEach(caracter => {
          valores[i][j] = valores[i][j].split(caracter).join('');
        });
      }
    }
  }
  rango.setValues(valores);
}
```

5. **Formateo y ordenamiento de datos clave:**

Durante la preparación de los datos en Google Sheets, se aplicaron las siguientes acciones para asegurar la correcta visualización y organización de la información:

- **Columna Código:**  
  Se utilizó un formato numérico personalizado con ceros a la izquierda (por ejemplo, `00000`) para mantener la longitud estándar de los códigos y asegurar que se correspondieran con el archivo modelo original.

- **Columna Precio:**  
  Se aplicó un formato de número con dos decimales y separador de miles, facilitando la lectura y el análisis de los valores monetarios.

- **Ordenamiento por Precio:**  
  Se ordenaron los datos de mayor a menor según la columna Precio para facilitar la identificación rápida de los valores más altos dentro del dataset.

Estas acciones permitieron mantener la integridad, claridad y usabilidad del dataset para las etapas posteriores de análisis y limpieza.

6. **Creación de columna combinada:**

Se creó una nueva columna que concatena los datos de las columnas A y B para facilitar el análisis conjunto de ambas variables. Para esto, se utilizó la fórmula de Google Sheets:

```plaintext
=ARRAYFORMULA(A:A & " " & B:B)
```

7. **Eliminación de fórmulas:**  
   Para garantizar que el archivo contenga solo valores estáticos y evitar dependencias, se copiaron todas las celdas con fórmulas (Ctrl + C) y se pegaron solo los valores utilizando pegado especial (Ctrl + Mayús + V).

8. **Formato visual:**  
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
- **Datos > Ordenar intervalo por columna "H" Z → A:** Para ordenar datos de mayor a menor según la columna H.  
- **Archivo > Configuración > Configuración regional > Argentina:** Para ajustar formatos numéricos y monetarios regionales.  

---
- **Extensiones > Apps Script:** Para ejecutar scripts personalizados que automatizan tareas como limpieza masiva de caracteres o manipulación de datos.

---

## Fórmulas para concatenar

```excel
=ARRAYFORMULA(A:A & " " & B:B)
