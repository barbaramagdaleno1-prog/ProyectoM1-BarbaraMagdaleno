# Proyecto integrador M1 - InsightReach

**Autora:** Bárbara Magdaleno  
**Alcance:** análisis exploratorio de clientes, integración con Yelp y Web Scraping cultural de Wikipedia.

## 1. Objetivo y alcance

En este proyecto analicé una base de clientes, consulté información externa de restaurantes mediante Yelp y sumé una dimensión cultural a través de la extracción de contenido público de Wikipedia. Elegí Miami como ciudad principal porque aparece en la base y fue la ciudad utilizada para la consulta de Yelp. Para la actividad con Selenium seleccioné Chicago como segunda ciudad, que también está presente en la base.

La información cultural se utiliza como **contexto cualitativo**. No la uno fila por fila con los clientes ni la interpreto como una característica individual de cada persona, porque no existe una clave común entre las fuentes.

## 2. Estructura

```text
ProyectoM1_NombreEstudiante/
├── Avances/
│   └── Notebooks/
│       ├── Avance_EDA.ipynb
│       ├── Avance_API_Yelp.ipynb
│       └── 3_WebScraping.ipynb
├── Datos/
│   ├── base_clientes_sin_datos_contacto.csv
│   ├── CSV de resultados del EDA y Yelp
│   ├── WebScraping/
│   │   ├── Resultados_WebScraping/ (CSV y TXT)
│   │   ├── evidencias_webscraping/ (5 capturas PNG)
│   │   └── README_resultados.txt
│   ├── README_fuentes.txt
│   └── METODOLOGIA_CALCULOS.txt
├── Documentacion/
│   ├── README.docx
│   ├── README.pdf
│   ├── Recomendaciones.docx
│   └── Recomendaciones.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

## 3. Qué hice en cada avance

### Avance 1 - EDA

Cargué la base de 30.000 registros y 13 columnas, revisé su estructura, tipos de datos, valores faltantes y duplicados. Elegí Miami y filtré los 3.186 registros correspondientes (10,62% de la base). Identifiqué edades fuera del rango de referencia y frecuencias negativas y las marqué como faltantes, sin eliminar personas. Generé tablas y gráficos de las variables disponibles. La base no contiene duración de sesión ni calificaciones de clientes, por lo que no inventé esas variables.

### Avance 2 - Yelp API

Me conecté a Yelp Business Search mediante una clave API y autenticación Bearer. La clave se lee desde Google Colab Secrets (`YELP_API_KEY`) y no se guarda en el código. La búsqueda informó 5.900 resultados posibles y recuperé 100 negocios en dos solicitudes. Separé los datos generales de las categorías: quedaron 100 negocios y 202 pares únicos negocio-categoría después de depurar repeticiones. De los 100 negocios, 83 informan Miami y 17 localidades cercanas.

### Avance 3 - Análisis integrado y Web Scraping

En `Avance_EDA.ipynb` desarrollé el análisis descriptivo y las preguntas de negocio solicitadas, con gráficos, interpretación y segmentación de clientes de Miami.

En `3_WebScraping.ipynb` incorporé una extracción de la sección **Culture** del artículo de Miami en Wikipedia. En la ejecución adjunta, registrada el 5 de noviembre de 2026 a las 04:29 UTC, la página respondió HTTP 200. Extraje **16 párrafos y 1.079 palabras**, organizados en siete subsecciones: Introducción de cultura (2 párrafos, 223 palabras), Venues (3, 100), Events (4, 202), Music and performing arts (1, 61), Museums and visual arts (1, 61), Cuisine (2, 207) y Dialect (3, 225). La extracción se realizó desde la versión en inglés y conserva URL y fecha.

También utilicé Selenium para abrir Miami, buscar Chicago desde el buscador interno, cambiar el tema de `day` a `night` y navegar al artículo de Chicago en español. La ejecución guardó cinco capturas y el registro `evidencias_selenium.csv`. La comprobación técnica del tema devolvió `guardado=True`, `tema=night` y `claseOscura=True`; la captura muestra la página oscura, aunque el indicador lateral de color aparece visualmente como “Claro”. Por eso conservo tanto la salida del DOM como la imagen. Los CSV, TXT y capturas reales están incluidos en `Datos/WebScraping/`.

Para este avance utilicé IA como apoyo para generar y revisar una primera versión del script. Organicé el código según las tareas y ciudades del proyecto y revisé la lógica y los resultados antes de interpretarlos.

## 4. Resultados principales

| Indicador | Resultado |
|---|---|
| Clientes por ciudad | Chicago: 5.384; Miami: 3.186. |
| Estratos | Medio: 9.325 (31,08%); Alto: 9.038 (30,13%); Bajo: 6.161 (20,54%); Muy Alto: 5.476 (18,25%). |
| Gasto estimado por período registrado | Miami: media de 225,88 unidades de la base. |
| Correlación ingresos-gasto estimado | Pearson ≈ 0,71; asociación, no causalidad. |
| Preferencias en Miami | Mariscos: 26,94%; Vegetariano: 23,95%; Carnes: 16,81%; Vegano: 12,57% (respuestas válidas). |
| Perfil de mayor gasto | 7.080 clientes en el 25% superior; preferencias frecuentes: Carnes, Vegetariano y Mariscos. |
| Membresías premium | Chicago: 2.215 en cantidad; Miami: 53,17% en proporción. |
| Edad y consumo de licor | Media de 45,99 entre quienes declaran consumir y 53,64 entre quienes no. |
| Segmentación de Miami | 2.997 clientes con ambas variables válidas; medianas: frecuencia 5 y gasto por comida 31,59. |
| Extracción cultural Wikipedia | HTTP 200; 16 párrafos; 1.079 palabras; 7 subsecciones (05/11/2026, 04:29 UTC). |

## 5. Integración e interpretación

La integración de clientes y Yelp es contextual. En Miami, Mariscos representa el 26,94% de las preferencias válidas; seis de los 83 negocios que informan Miami tienen la categoría Seafood. En esa muestra no aparecen etiquetas Vegetarian ni Vegan. Esto no significa que esos restaurantes no ofrezcan esos platos: las categorías de Yelp no describen necesariamente todo el menú.

Wikipedia añade contexto sobre influencias gastronómicas latinoamericanas y caribeñas, cocina Floribbean, platos de origen cubano y presencia de restaurantes de mariscos. Utilizo esos elementos para formular ideas que después deben validarse con menús y datos reales. No deduzco identidad cultural, idioma ni preferencias individuales a partir de la ciudad.

## 6. Cómo reproducir el trabajo

1. Instalar dependencias: `pip install -r requirements.txt`.
2. Ejecutar `Avance_EDA.ipynb` en orden.
3. Para repetir Yelp, configurar el Secret `YELP_API_KEY` en Colab y habilitar el acceso desde el notebook. No escribir la clave en el código.
4. Ejecutar `3_WebScraping.ipynb`. Antes, reemplazar `CONTACTO` por un correo válido para identificar las solicitudes en el User-Agent.
5. Para guardar los resultados dentro del proyecto desde Colab, configurar `DIRECTORIO_PROYECTO` con la ruta de la carpeta raíz. El notebook crea `Datos/WebScraping/`; si no encuentra la carpeta, crea `Resultados_WebScraping` en el directorio de trabajo.
6. En esta entrega, revisar los archivos incluidos en `Datos/WebScraping/Resultados_WebScraping/` y las cinco capturas de `Datos/WebScraping/evidencias_webscraping/`. El CSV `evidencias_selenium.csv` contiene las rutas de las capturas dentro del proyecto. Si se repite la ejecución, volver a verificar el contenido y la fecha de los archivos generados.

## 7. Limitaciones

- La base no aclara el período de `frecuencia_visita` ni la moneda de `promedio_gasto_comida`. Por eso calculé `frecuencia_visita × promedio_gasto_comida` y lo llamé **gasto estimado por período registrado**, no gasto mensual confirmado.
- Los 100 resultados de Yelp son una muestra de búsqueda, no el universo de restaurantes de Miami; 17 informan localidades cercanas.
- No hay una clave común para relacionar cada cliente con un restaurante específico.
- Las categorías de Yelp no garantizan la presencia o ausencia de platos en los menús.
- Wikipedia es una fuente enciclopédica de contexto y puede cambiar. La extracción es una captura puntual de 16 párrafos de la sección Culture en inglés, no representa toda la cultura de Miami ni mide preferencias de clientes.
- Las correlaciones no prueban causalidad. Las recomendaciones son hipótesis que deben probarse.
- No utilizo cultura o idioma para inferir atributos sensibles de clientes; las campañas deben basarse en preferencias declaradas y comportamiento observado.

## 8. Fuentes

- Base de clientes entregada para el proyecto (copia sin datos de contacto en `Datos/`).
- [Yelp Business Search](https://docs.developer.yelp.com/reference/v3_business_search)
- [Yelp Places Authentication](https://docs.developer.yelp.com/docs/places-authentication)
- [Wikipedia - Miami](https://en.wikipedia.org/wiki/Miami)
- [Wikipedia - Chicago](https://en.wikipedia.org/wiki/Chicago)
- [Wikipedia - Chicago en español](https://es.wikipedia.org/wiki/Chicago)
- [Política de User-Agent de Wikimedia](https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_User-Agent_Policy)
- [Política de acceso y límites de Wikimedia](https://www.mediawiki.org/wiki/Wikimedia_APIs/Access_policy)
- [Límites de uso de Wikimedia](https://www.mediawiki.org/wiki/Wikimedia_APIs/Rate_limits)
- [Selenium - Esperas explícitas](https://www.selenium.dev/documentation/webdriver/waits/)
