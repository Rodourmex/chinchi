# Planner de Composicion Corporal

## Descripcion

Aplicacion web en un solo archivo HTML para capturar datos de composicion corporal, interpretar resultados y generar reportes PDF.

El flujo principal incluye:

- Captura de datos antropometricos y segmentales.
- Clasificaciones automaticas (grasa, grasa visceral, musculo).
- Calculos automaticos (promedios segmentales, peso, grasa corporal en kg, MLG).
- Generacion de texto de diagnostico editable.
- Resumen para paciente con recomendaciones editables.
- Exportacion a PDF respetando el diseno visual del HTML.

## Archivos

- index.html: interfaz, estilos, logica de calculo, reglas y exportacion a PDF.

## Como usar

1. Abre index.html en el navegador.
2. Captura sexo, IMC y estatura.
3. El sistema calcula automaticamente:

- Peso actual (kg).
- Grasa corporal (kg) = peso actual \* (% grasa / 100).
- MLG (kg) = peso actual - grasa corporal (kg).

4. Captura el resto de campos (grasa visceral, musculo total, datos segmentales, abdomen).
5. Revisa:

- Interpretaciones por campo.
- Diagnostico antropometrico.
- Resumen para paciente.
- Recomendaciones (editables).

6. Usa los botones de exportacion para generar PDF.

## Persistencia local

- La informacion se guarda en localStorage de forma especifica por archivo (incluye la ruta del archivo en la llave de guardado).
- Si copias `index.html` a otra carpeta, esa copia inicia con su propio almacenamiento independiente.

## Campos calculados automaticamente

- Promedio de brazos (%): promedio de brazo derecho e izquierdo.
- Promedio de piernas (%): promedio de pierna derecha e izquierda.
- Peso actual (kg): desde IMC y estatura.
- Grasa corporal (kg): desde porcentaje de grasa y peso actual.
- MLG (kg): peso actual menos grasa corporal (kg).

## Reglas de interpretacion implementadas

### Grasa corporal

Depende de sexo (hombre o mujer) con rangos de:

- Baja
- Normal-baja
- Normal
- Pre obesidad
- Obesidad grado 1
- Obesidad grado 2
- Obesidad grado 3

### Grasa visceral

Rangos:

- Optimo
- Normal
- Elevada
- Muy elevada

### Musculo total y segmental

Rangos:

- Bajo
- Normal-bajo
- Normal
- Normal-alto
- Optimo

## Diagnostico antropometrico

Se genera texto automaticamente con:

- Clasificacion de musculo total.
- Desequilibrios (brazos, piernas, trenes).
- Clasificacion de grasa corporal.
- Clasificacion de grasa visceral.
- Nota adicional por IMC bajo segun sexo.

El textarea es editable por el usuario.

## Resumen para paciente

Incluye:

- Nombre, valor e interpretacion por parametro principal.
- Musculo segmental mostrado por promedios.
- Datos adicionales.
- Recomendaciones automaticas editables.

## Recomendaciones automaticas

Se generan segun:

- Grado de grasa corporal.
- Grasa visceral elevada o muy elevada.
- Musculo total bajo o normal-bajo.
- Diferencias de desequilibrio en brazos, piernas y entre trenes.
- Objetivos de control de grasa y musculo (kg) con base en estandares estimados.

Puedes editar recomendaciones manualmente y restaurar las automaticas con el boton correspondiente.

## Exportacion PDF

La exportacion usa:

- html2canvas para capturar el DOM renderizado.
- jsPDF para crear el archivo PDF.

Comportamiento de exportacion:

- Respeta estilos visibles del HTML.
- Convierte textareas a bloques de texto para exportar todo el contenido.
- Pagina automaticamente en varias hojas cuando el contenido excede una pagina.

## Dependencias CDN

Cargadas en index.html:

- https://cdn.jsdelivr.net/npm/jspdf@2.5.1/dist/jspdf.umd.min.js
- https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js

## Mantenimiento rapido

Si actualizas reglas o rangos:

1. Ajusta funciones de evaluacion en index.html.
2. Verifica mensajes del diagnostico y recomendaciones.
3. Prueba exportacion PDF con contenido corto y largo.
4. Asegura que los campos calculados sigan sincronizados.

## Sugerencias de prueba manual

- Caso sin datos: diagnostico vacio.
- Caso con solo IMC y estatura: se calcula peso.
- Caso con % grasa: se calcula grasa corporal kg y MLG.
- Caso con asimetria alta en brazos/piernas/trenes: revisar recomendaciones especificas.
- Caso con muchas recomendaciones editadas: validar que PDF exporte todas las lineas.
