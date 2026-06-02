# Sistema de Web Scraping y Análisis de Precios de Vivienda en la Ciudad de México

## Descripción General

Este proyecto fue desarrollado con el objetivo de construir una base de datos integral del mercado inmobiliario de la Ciudad de México mediante técnicas de web scraping, integración de fuentes externas y modelado econométrico.

El sistema recopila información de anuncios de viviendas en venta publicados en Mercado Libre Inmuebles, extrae variables estructurales y geográficas de cada propiedad, incorpora información de accesibilidad a servicios cercanos y posteriormente enriquece los datos mediante cruces con fuentes oficiales como el Directorio Postal de México y el Índice de Precios de Vivienda del INEGI.

La información obtenida fue utilizada para desarrollar modelos econométricos, modelos ARIMA, técnicas de reducción dimensional y algoritmos de clusterización orientados al análisis del comportamiento de los precios de vivienda en la Ciudad de México.

---

## Objetivos del Proyecto

* Automatizar la recopilación de información inmobiliaria.
* Construir una base de datos limpia y estructurada para análisis económico.
* Incorporar variables espaciales y de accesibilidad urbana.
* Relacionar precios actuales de vivienda con información histórica oficial.
* Desarrollar modelos predictivos y explicativos del precio de venta de viviendas.

---

## Flujo General del Sistema

### 1. Extracción de anuncios

El sistema accede automáticamente al portal de Mercado Libre Inmuebles y navega por los anuncios de viviendas en venta ubicadas en la Ciudad de México.

Para cada anuncio se obtiene:

* Precio de venta.
* Descripción completa del inmueble.
* Número de recámaras.
* Número de baños.
* Superficie en metros cuadrados.
* Número de unidades disponibles en venta.

---

### 2. Obtención de información geográfica

Dentro de cada anuncio existe un mapa interactivo que proporciona información espacial de la propiedad.

A partir de este componente se extraen:

* Latitud.
* Longitud.
* Código postal.
* URL geográfica.

Adicionalmente se desarrolló un proceso de transformación de URLs para generar enlaces compatibles con Google Maps, permitiendo abrir directamente la ubicación de cada inmueble.

---

### 3. Extracción de accesibilidad urbana

Cada anuncio contiene una sección de lugares cercanos organizados en diferentes categorías.

El sistema recopila información de:

* Transporte.
* Educación.
* Salud.
* Comercio y supermercados.
* Áreas verdes.

Para cada categoría se extrae:

* Nombre del establecimiento.
* Tiempo estimado de traslado.
* Distancia al inmueble.

La información se almacena tanto de forma agregada como individual para cada establecimiento identificado.

---

### 4. Construcción de indicadores de accesibilidad

A partir de los lugares cercanos identificados se calculan indicadores resumen para cada categoría:

* Tiempo promedio de acceso.
* Distancia promedio.

Estos indicadores permiten cuantificar el nivel de accesibilidad urbana de cada vivienda.

---

### 5. Integración con Directorio Postal

Los códigos postales obtenidos durante el scraping se cruzan con una base de datos postal nacional para identificar:

* Alcaldía o municipio correspondiente.
* Información territorial asociada.

---

### 6. Integración con información oficial del INEGI

Se realizó un proceso de limpieza y preparación de la base de datos del Índice de Precios de Vivienda del INEGI.

Las etapas incluyeron:

* Filtrado exclusivo para la Ciudad de México.
* Eliminación de registros pertenecientes a otras entidades federativas.
* Estandarización de periodos trimestrales.
* Integración con la base inmobiliaria generada por el scraping.

La información histórica utilizada cubre el periodo:

2005 - 2025

con frecuencia trimestral.

---

### 7. Construcción de la Base Analítica Final

Posteriormente se integraron todas las fuentes de información en una sola base de datos para análisis.

La base final incluye:

* Características físicas de la vivienda.
* Variables geográficas.
* Indicadores de accesibilidad.
* Variables territoriales.
* Indicadores históricos de precios de vivienda.

Asimismo, se eliminaron variables redundantes y se reorganizó la estructura para facilitar su utilización en modelos estadísticos.

---

## Modelado Econométrico

Se desarrolló un modelo econométrico semilogarítmico para analizar los determinantes del precio de venta de las viviendas.

Las variables explicativas consideradas incluyen:

### Características del inmueble

* Número de recámaras.
* Número de baños.
* Superficie.

### Indicadores de accesibilidad

* Tiempo promedio a transporte.
* Distancia promedio a transporte.
* Tiempo promedio a escuelas.
* Distancia promedio a escuelas.
* Tiempo promedio a áreas verdes.
* Distancia promedio a áreas verdes.
* Tiempo promedio a comercios.
* Distancia promedio a comercios.
* Tiempo promedio a servicios de salud.
* Distancia promedio a servicios de salud.

### Variables territoriales

* Variables dummy por alcaldía/municipio.

### Efectos espaciales

* Interacciones entre superficie y ubicación geográfica.

---

## Análisis Complementarios

Además del modelo econométrico principal se desarrollaron:

### Modelos ARIMA

Utilizados para analizar y proyectar el comportamiento temporal de los precios de vivienda.

### Clusterización

Aplicada para identificar grupos de viviendas con características similares.

### Reducción Dimensional

Implementada para explorar estructuras latentes dentro del conjunto de variables y facilitar el análisis multivariado.

---

## Tecnologías Utilizadas

* Python
* Web Scraping
* Selenium
* Bases de datos relacionales
* Integración de datos
* Econometría
* Series de tiempo
* Modelos ARIMA
* Machine Learning no supervisado
* Análisis estadístico
* Procesamiento de datos geográficos

---

## Resultados

El proyecto permitió construir una base de datos enriquecida del mercado inmobiliario de la Ciudad de México integrando información estructural, geográfica, territorial y económica, proporcionando una plataforma sólida para análisis econométrico y modelado predictivo de precios de vivienda.
