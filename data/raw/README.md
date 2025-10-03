# Bitácora Técnica — Scraping de Noticias (BBC Mundo Tecnología)

## 1. Elección del sitio

Elegí la sección de Tecnología de BBC Mundo (https://www.bbc.com/mundo/topics/cyx5krnw38vt) porque fue el sitio que mostraba una estructura HTML más limpia y consistente para las noticias. Las primeras opciones (Reuters, El Universal) presentaron bloqueos anti-scraping o HTML inconsistente, dificultando la automatización.

## 2. Flujo de Adquisición de Datos

- **Fase 1:** Selección y análisis de la estructura HTML del sitio objetivo.
- **Fase 2:** Implementación del scraper en Python usando `requests` y `BeautifulSoup`.
- **Fase 3:** Serialización de los resultados en formato JSONL en el archivo `data/raw/noticias.jsonl`.
- **Fase 4:** Perfilado de calidad y contrato de datos (`data/raw/noticias_data_contract.yaml`).

### Archivos y scripts relacionados
- `notebooks/tareas/WB1.5 Scraping de Noticias y Serialización en JSONL.ipynb`: Notebook principal con el código de scraping, serialización y perfilado.
- `data/raw/noticias.jsonl`: Archivo de salida con las noticias extraídas.
- `data/raw/noticias_data_contract.yaml`: Contrato de datos para validar el dataset.

## 3. Construcción del Scraper

- Se utilizó Python con las librerías `requests` y `BeautifulSoup`.
- El scraper identifica los elementos `<li class="bbc-t44f9r">` para cada noticia.
- Extrae título, URL, fecha, resumen (alt de la imagen o título) y, accediendo a cada noticia, el autor.
- Cada noticia se serializa como un objeto JSON en una línea del archivo `.jsonl`.

## 4. Problemas encontrados

- **Bloqueos anti-scraping:** Reuters y otros medios internacionales bloquean peticiones automatizadas o requieren headers/cookies avanzados.
- **HTML inconsistente:** Algunos sitios cambian la estructura de sus noticias entre la portada y las páginas internas, dificultando la extracción masiva.
- **Carga dinámica:** Algunos autores solo están disponibles accediendo a la página individual de la noticia, lo que requiere múltiples requests.