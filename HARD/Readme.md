# Archivo: Hard.xls

## Descripción general

Este documento describe el proceso de transformación y limpieza aplicado al archivo `Hard.xls`, entregado como parte de la prueba técnica. El objetivo principal fue convertir un archivo original en formato `.csv` en un archivo estructurado, limpio y debidamente formateado, listo para su análisis o integración posterior.

## Proceso de conversión y carga

- El archivo original fue provisto en formato `.csv`.
- Se realizó la conversión a formato `.xls` utilizando Microsoft Excel, conforme a los requerimientos establecidos.
- Posteriormente, el archivo convertido fue importado a Google Sheets para facilitar el procesamiento y la aplicación de formatos regionales.

## Procesamiento y limpieza de datos

1. **Eliminación de filas vacías:**  
   Se aplicó un filtro en la hoja (Menú: Datos > Crear filtro), luego se utilizó un filtro especial para mostrar solo las filas vacías en la columna correspondiente (Filtro por condición > Está vacío).  
   Una vez filtradas, se seleccionaron y eliminaron esas filas para mantener una estructura tabular continua y evitar inconsistencias.

2. **Incorporación de encabezados:**  
   Se añadieron los nombres de columna conforme al formato modelo proporcionado, facilitando la interpretación y manipulación de los datos.

3. **Configuración regional:**  
   Se ajustó la configuración regional de Google Sheets a “Argentina” para garantizar el correcto manejo de formatos numéricos y monetarios.  
   *(Menú: Archivo > Configuración > Configuración regional > Argentina)*

4. **Normalización de precios:**  
   Los valores originales de precios presentaban una escala incorrecta. Para corregir esta situación se aplicó la siguiente fórmula en Google Sheets:  

   ```excel
   =ARRAYFORMULA(F2:F / 100)
5. **Ordenamiento:**  
   La tabla fue ordenada en orden descendente según los valores de precio para optimizar su visualización y análisis.  
   *(Seleccionar la columna G > Menú Datos > Ordenar intervalo por columna "G" Z → A)*

6. **Eliminación de las fórmulas:**  
   Para garantizar que el archivo contenga solo valores estáticos y evitar dependencias de fórmulas, se seleccionaron todas las celdas con fórmulas, se copiaron (Ctrl + C) y luego, utilizando la función de pegado especial (Ctrl + Mayús + V), se pegó solo el valor, reemplazando las fórmulas por sus resultados.

7. **Ajuste final:**  
   Se aplicaron formatos y estilos para asegurar que el archivo final coincidiera con el modelo de referencia proporcionado (tipografía, alineación, formato numérico, etc.).


## Atajos y tips usados

- **Ctrl + A**: Seleccionar todo el rango activo (presionar dos veces para seleccionar toda la hoja).  
- **Ctrl + Shift + ↓**: Seleccionar todas las celdas hacia abajo desde la celda activa.  
- **Ctrl + C**: Copiar celdas seleccionadas.  
- **Ctrl + X**: Cortar celdas seleccionadas.  
- **Ctrl + Mayús + V**: Pegado especial — Pegar solo valores, sin fórmulas ni formatos.  
- **Ctrl + Z**: Deshacer última acción.  

- **Datos > Crear filtro**: Para aplicar filtros personalizados en columnas.  
- **Filtro por condición > Está vacío**: Para detectar y eliminar filas vacías.  
- **Datos > Ordenar intervalo por columna "G" Z → A**: Para ordenar datos de mayor a menor según la columna G.  
- **Archivo > Configuración > Configuración regional > Argentina**: Para ajustar formatos numéricos y monetarios regionales.  

- **ARRAYFORMULA**: Para aplicar operaciones a rangos completos sin copiar la fórmula una por una.  
  Ejemplo:  
  ```excel
  =ARRAYFORMULA(F2:F / 100)
