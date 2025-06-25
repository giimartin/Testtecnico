# Archivo: Proveedor Anaerobicos

## Descripción general

Este documento detalla el proceso de transformación y limpieza aplicado al archivo `Proveedor anaerobics`, con el objetivo de obtener un dataset estructurado, limpio y estandarizado para análisis o uso posterior.

## Proceso de preparación y carga

- Se creó una copia del archivo original en Google Drive para trabajar sobre ella sin modificar el archivo fuente.  
- El archivo fue abierto en Google Sheets para facilitar la manipulación y limpieza.

## Procesamiento y limpieza de datos

1. **Verificación de filas vacías:**  
   Se revisó que no existieran filas vacías para mantener una estructura tabular continua y evitar inconsistencias.  
   Para esto, se aplicó un filtro a la tabla (**Datos > Crear filtro**) y luego se filtraron las celdas vacías en la columna correspondiente utilizando la opción:  
   **Filtro por condición > Está vacío**.  
   Una vez filtradas, se seleccionaron y eliminaron las filas vacías.

2. **Configuración regional:**  
   Se ajustó la configuración regional en Google Sheets a “Argentina” para asegurar el correcto manejo de formatos numéricos y monetarios.  
   *(Menú: Archivo > Configuración > Configuración regional > Argentina)*  

3. **Separación de columna combinada:**  
   Se identificó una columna que contenía código y descripción del producto juntos.  
   Para separar esta columna, se seleccionó la columna completa y se utilizó la función integrada de Google Sheets:  
   **Datos > Dividir texto en columnas**, con un separador personalizado definido por varios espacios (`       `).  
   Esto dividió la columna en dos: una con el código numérico y otra con la descripción del producto.

4. **Concatenación para normalizar formato:**  
   Se creó una nueva columna que combina el código y la descripción en un solo texto separado por un espacio, utilizando la fórmula:  

   ```excel
   =A2 & " " & B2

5. **Incorporación de encabezados:**  
   Se añadieron los nombres de columna conforme al formato modelo proporcionado, facilitando la interpretación y manipulación de los datos.

6. **Ordenamiento de precios:**  
   La tabla fue ordenada en orden descendente según los valores de precio para optimizar la visualización y el análisis.  
   *(Seleccionar la columna D > Menú Datos > Ordenar intervalo por columna "D" Z → A)*

7. **Eliminación de fórmulas:**  
   Para garantizar que el archivo contenga solo valores estáticos y evitar dependencias, se copiaron todas las celdas con fórmulas (Ctrl + C) y se pegaron solo los valores utilizando pegado especial (Ctrl + Mayús + V).

8. **Formato visual:**  
    Se aplicaron formatos visuales para mejorar la presentación y legibilidad del archivo segun archivo modelo.


## Atajos y funciones utilizadas

- **Ctrl + A** (presionado dos veces): Seleccionar toda la hoja.  
- **Ctrl + C**: Copiar celdas seleccionadas.  
- **Ctrl + Mayús + V**: Pegado especial — Pegar solo valores.  
- **Datos > Dividir texto en columnas**: Para separar valores combinados.  
- **Separador personalizado**: Usado para dividir por múltiples espacios.  
- **=A2 & " " & B2**: Concatenar código y producto en una misma celda.  
- **Datos > Ordenar intervalo por columna "D" Z → A**: Orden descendente por precio.  
- **Archivo > Configuración > Configuración regional > Argentina**: Para asegurar el formato local correcto.  
- **Datos > Crear filtro > Filtro por condición > Está vacío**: Para detectar y eliminar filas vacías.
