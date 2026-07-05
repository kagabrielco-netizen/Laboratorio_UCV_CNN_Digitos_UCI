# Laboratorio CNN - Clasificación de Dígitos UCI

## Descripción
Modelo de Red Neuronal Convolucional (CNN) para clasificar imágenes de 
dígitos escritos a mano (8x8 píxeles), usando el dataset Optical Recognition 
of Handwritten Digits de UCI.

## Dataset
UCI ML Repository - Optical Recognition of Handwritten Digits 
(1797 imágenes de 8x8 píxeles, 10 clases: dígitos 0-9).

## Ejemplos del dataset
<img width="1221" height="98" alt="image" src="https://github.com/user-attachments/assets/872f5824-2c71-4fc0-b48d-c818ffc4d390" />


## Entrenamiento del modelo base
<img width="552" height="349" alt="image" src="https://github.com/user-attachments/assets/42458f3b-00b9-4e7a-a2a5-ebbdccff5fb3" />

<img width="530" height="351" alt="image" src="https://github.com/user-attachments/assets/5161d5f4-a91b-487b-bac0-5cb699dfb406" />


## Evaluación
<img width="137" height="32" alt="image" src="https://github.com/user-attachments/assets/484efa2e-9026-477b-b48d-f333a9c84f25" />

<img width="344" height="235" alt="image" src="https://github.com/user-attachments/assets/5a1daf5a-2a6b-45f6-9d62-d607a0a63454" />


## Matriz de confusión
<img width="380" height="341" alt="image" src="https://github.com/user-attachments/assets/f4e7fef1-245f-4e5b-81d2-efed65946cd4" />


## Predicciones individuales
<img width="717" height="416" alt="image" src="https://github.com/user-attachments/assets/a39129a5-9359-45c9-ac1f-7fbb1f031a84" />

<img width="698" height="407" alt="image" src="https://github.com/user-attachments/assets/12ebb997-0323-425b-ad48-0a34a63da600" />

## Comparación CNN vs red densa simple
<img width="178" height="28" alt="image" src="https://github.com/user-attachments/assets/f80eafb9-969a-437c-b9ae-25ff15fbc0b3" />


## Reto: Comparación de 3 variantes CNN

Se entrenaron y compararon tres arquitecturas CNN distintas:

1. **CNN básica** con una sola capa convolucional.
2. **CNN con dos capas convolucionales**.
3. **CNN con Dropout y más neuronas densas**.

### Tabla comparativa

| Variante | Accuracy | Loss | Errores |
|---|---|---|---|
| 1 capa Conv2D | 0.9786 | 0.0700 | 36 |
| 2 capas Conv2D | 0.9798 | 0.0734 | 34 |
| Dropout + más densas | 0.9840 | 0.0561 | 27 |

### Dígitos más confundidos

En las tres variantes, el par **5 y 9** fue el más confundido, seguido por 
confusiones puntuales entre **3 y 8**. Esto es consistente con la naturaleza 
visual de dígitos manuscritos representados en solo 8x8 píxeles, donde las 
curvas de estos números pueden parecerse.

### Arquitectura elegida: Dropout + más neuronas densas

Esta variante logró el mejor accuracy (0.984), el menor loss (0.056) y menos 
errores (27), gracias a que el Dropout reduce el sobreajuste al apagar 
aleatoriamente neuronas durante el entrenamiento, permitiendo que el modelo 
generalice mejor en lugar de memorizar el set de entrenamiento.

### Pregunta central

> Si tuviera que implementar este modelo en un sistema OCR real, ¿qué 
arquitectura elegiría y por qué?

Elegiría la arquitectura con Dropout y más neuronas densas, ya que combina 
el mejor desempeño general con mecanismos que reducen el sobreajuste, siendo 
más confiable ante dígitos escritos con variaciones no vistas en el 
entrenamiento.

## Preguntas de análisis

1. **¿Qué diferencia existe entre una red densa y una CNN?**
La red densa trata cada píxel como una variable independiente; la CNN usa filtros que detectan patrones espaciales locales (bordes, curvas) aprovechando la estructura de la imagen.

2. **¿Qué función cumple una capa convolucional?**
Aplica filtros que recorren la imagen detectando patrones visuales como bordes, líneas o texturas.

3. **¿Qué representa un filtro en una CNN?**
Es una pequeña matriz de pesos que se ajusta durante el entrenamiento para detectar un patrón visual específico.

4. **¿Qué función cumple MaxPooling?**
Reduce el tamaño de la imagen conservando solo la información más relevante, disminuyendo cómputo y evitando sobreajuste.

5. **¿Por qué normalizamos los valores de píxeles?**
Para que estén en una escala pequeña (0-1) y la red neuronal entrene más rápido y de forma más estable.

6. **¿Por qué usamos `softmax` en la capa de salida?**
Porque convierte las salidas en probabilidades que suman 1, ideal para elegir una clase entre las 10 posibles (0-9).

7. **¿Qué dígitos se confundieron más en la matriz de confusión?**
Principalmente el 5 y el 9, y en menor medida el 3 y el 8, por similitud visual en sus curvas.

8. **¿Por qué algunos dígitos escritos a mano son difíciles de clasificar?**
Porque distintas personas los escriben con formas, grosores e inclinaciones diferentes, y en baja resolución (8x8) esas diferencias se pierden más fácilmente.

9. **¿Qué ventajas tendría usar imágenes de mayor resolución?**
Capturaría más detalles de la forma de cada dígito, reduciendo la confusión entre números visualmente similares como 5 y 9.

10. **¿Qué limitaciones tiene este laboratorio frente a un sistema OCR real?**
Usa un dataset pequeño y controlado (8x8 píxeles, escritura limpia), mientras un OCR real debe manejar imágenes más grandes, ruido, distintos tipos de letra y condiciones variables de escaneo.

## Conclusión

El modelo CNN logró un desempeño alto y consistente en la clasificación de 
dígitos, superando a una red densa simple gracias a su capacidad de detectar 
patrones visuales locales mediante filtros convolucionales.

Al comparar tres variantes de arquitectura, la que incluyó Dropout y más 
neuronas densas obtuvo el mejor resultado (accuracy 0.984, solo 27 errores), 
demostrando que técnicas de regularización como Dropout ayudan a generalizar 
mejor, no solo a memorizar el set de entrenamiento.

El par de dígitos 5 y 9 fue el más difícil de distinguir en las tres 
variantes, evidenciando una limitación esperable al trabajar con imágenes de 
baja resolución (8x8 píxeles). Para un sistema OCR real, sería necesario usar 
imágenes de mayor resolución, más datos y técnicas de aumento de datos.
