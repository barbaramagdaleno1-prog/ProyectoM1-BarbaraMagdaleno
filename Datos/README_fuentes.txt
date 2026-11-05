FUENTES DE DATOS DEL PROYECTO

1. base_clientes_sin_datos_contacto.csv
   Copia anonimizada de la base de clientes entregada para el proyecto. Contiene 30.000 filas y 13 columnas. Se excluyeron nombre, apellido, teléfono y correo electrónico.

2. yelp_miami_consulta_api.csv
   Datos generales de 100 negocios obtenidos mediante una consulta real a Yelp Business Search para restaurants en Miami, Florida. Yelp informó 5.900 resultados posibles, pero la extracción solicitó y recibió 100. La columna city muestra que 83 negocios informan Miami y 17 pertenecen a localidades cercanas.

3. yelp_miami_categorias.csv
   Contiene 202 pares únicos de negocio y categoría. La transformación inicial identificó 270 registros de categorías; al eliminar asociaciones repetidas del mismo negocio y categoría quedaron 202 relaciones únicas.

4. Tablas de Avance 3
   Los CSV adicionales resumen clientes por ciudad, distribución de estratos, gasto estimado por período, preferencias por ciudad, perfil del 25% con mayor gasto estimado, membresías y edades según consumo de alcohol. El notebook explica las fórmulas y limitaciones.

La clave de Yelp se lee desde Google Colab Secrets con el nombre YELP_API_KEY y no está incluida en el repositorio.

5. 3_WebScraping.ipynb y resultados culturales
   La ejecución documentada del 05/11/2026 a las 04:29 UTC obtuvo HTTP 200 y extrajo 16 párrafos (1.079 palabras) de la sección Culture del artículo de Miami en Wikipedia, organizados en siete subsecciones. Los resultados están incluidos en Datos/WebScraping/Resultados_WebScraping/: cultura_miami_wikipedia.csv (detalle), resumen_cultura_miami.csv (resumen) y cultura_miami_wikipedia.txt (texto). El contenido corresponde a la versión en inglés disponible en esa fecha.

6. Evidencias de Selenium
   La ejecución guardó cinco capturas en Datos/WebScraping/evidencias_webscraping/ y un registro en Datos/WebScraping/Resultados_WebScraping/evidencias_selenium.csv. Las imágenes muestran la apertura de Miami, la búsqueda de Chicago, la modificación del tema, el artículo en español y una verificación adicional del tema oscuro. La comprobación técnica reportó la preferencia night y la clase CSS de modo oscuro; el indicador lateral de color aparece visualmente como Claro en la captura, por lo que se conserva también la salida del DOM.

Fuente cultural: https://en.wikipedia.org/wiki/Miami (consulta: 05/11/2026). El contenido puede cambiar y debe interpretarse como contexto cualitativo, no como información individual de clientes.
