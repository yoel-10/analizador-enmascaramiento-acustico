# Analizador Espectral de Enmascaramiento Acústico

## README v0: Idea Inicial
El objetivo inicial del proyecto es desarrollar una herramienta computacional que audite mezclas de audio de forma automatizada. Específicamente, se busca resolver el problema de las colisiones de frecuencia (enmascaramiento psicoacústico) en la zona de graves, un desafío crítico en la producción musical.

## README v1: Pregunta + Datos
**Pregunta Principal:** ¿Es posible detectar y cuantificar matemáticamente las frecuencias exactas donde el Bombo enmascara al Bajo, sin depender exclusivamente del monitoreo auditivo?

**Datos:** 
Para la investigación se utilizan archivos `.wav`exportados directamente desde un proyecto:
- `kick.wav` (Señal principal / Enmascarador)
- `Bajo.wav` (Señal secundaria / Enmascarada)

## README v2: Primer Análisis
El primer abordaje consistió en sacar las señales del dominio del tiempo y llevarlas al dominio de la frecuencia. Utilizando la Transformada Rápida de Fourier (FFT) mediante las librerías `librosa` y `numpy`, se calculó la energía espectral promedio de ambas señales. 

El resultado fue un gráfico de "Amplitud Percibida (dB) vs. Frecuencia (Hz)" que permitió confirmar visualmente las áreas donde el nivel de energía del bombo superaba críticamente al del bajo entre los 20 Hz y 250 Hz.

## README v3: Pipeline Actualizado
El código en Python se reestructuró para dejar de ser un script estático y convertirse en una aplicación interactiva. Se integró la librería `streamlit` para construir el archivo `app.py`. 
El pipeline actual permite:
1. Carga dinámica de cualquier par de archivos de audio.
2. Cálculo de superposición de matrices de datos.
3. Dibujo de un área sombreada ("Sugerencia de Sidechain") exactamente en el rango frecuencial del conflicto.
4. Extracción de métricas: cálculo de la frecuencia fundamental (pico máximo) de cada pista.

## README Final: Estado, Resultados y Próximos Pasos

**Estado del Proyecto:** 
El analizador se encuentra operativo en su fase de visualización y diagnóstico. La aplicación se ejecuta de manera local en el navegador y procesa exitosamente los audios ingresados, generando un reporte visual claro de la colisión acústica.

**Resultados Obtenidos:**
El sistema logra traducir un problema psicoacústico abstracto en un reporte de datos concretos. Identifica matemáticamente las zonas de enmascaramiento, entregando los Hertz (Hz) y Decibeles (dB) exactos de conflicto, lo cual agiliza la toma de decisiones al momento de aplicar compresión sidechain o ecualización dinámica en la mezcla.

**Próximos Pasos (DSP Avanzado):**
- **Filtros Automatizados:** Programar un algoritmo de reducción de ganancia utilizando `scipy.signal` para que el programa, además de mostrar el problema, lo corrija matemáticamente en la señal del bajo.
- **Exportación de Audio:** Añadir la funcionalidad de guardar la matriz de datos corregida en un nuevo archivo `.wav` para reincorporarlo a la sesión de mezcla.