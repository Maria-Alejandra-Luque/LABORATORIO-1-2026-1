# LABORATORIO-1
## ESTADISTICA

## PARTE A

## PARTE B
Durante la segunda parte de nuestra practica, una señal fisiológica fue producida experimentalmente por medio del generador de señales biológicas del laboratorio.
Se empleó un sistema de adquisición de datos (DAQ) para obtenerlo, el cual fue conectado físicamente al PC por medio de USB y configurado con el controlador NI-DAQmx.
El DAQ recibió la señal analógica del generador, y esta fue transformada a digital. continuando la señal fue importada y procesada para asi realizar el correcto análisis 
estadístico y poder realizar su grafica correspondiente.De esta manera, se calcularon los parámetros estadísticos obtenidos en la Parte A y se comparó la señal descargada
de Physionet con la señal capturada usando el DAQ, lo que evidenció sus semejanzas y diferencias.
### ALGORITMO 
### CODIGO
#### Grafica de la señal 
Se importó la señal generada mediante el generador biológico y capturada con la STM32. La señal fue almacenada en formato .txt y 
posteriormente graficada en el dominio del tiempo.<br>

```
import numpy as np
import matplotlib.pyplot as plt
data = np.loadtxt("aleja.txt")
tiempo = data[:,0]     # primera columna
ecg = data[:,1]        # segunda columna
```
Este fragmento de código carga los datos contenidos en el archivo “aleja.txt” utilizando la función `np.loadtxt`, almacenándolos en una matriz llamada `data`.
Luego, separa las columnas del archivo: la primera se asigna a la variable `tiempo`, que representa el eje temporal, y la segunda a `ecg`, que corresponde a la amplitud 
de la señal. De esta manera, los datos quedan organizados para su posterior análisis o graficación. <br>

```
plt.figure(figsize=(12,4))
plt.plot(tiempo, ecg)
plt.title("Señal ECG")
plt.xlabel("Tiempo")
plt.ylabel("Amplitud")
plt.grid()
plt.show()
```
Este código se encarga de graficar la señal ECG en función del tiempo. Primero, se crea una figura con un tamaño de 12x4 pulgadas para mejorar la visualización.
Luego, se traza la señal utilizando `plt.plot(tiempo, ecg)`, donde el eje horizontal corresponde al tiempo y el eje vertical a la amplitud. Finalmente, se añaden el título,
las etiquetas de los ejes, una cuadrícula para facilitar la lectura de la gráfica y se muestra el resultado en pantalla con `plt.show()`.<br>

<img width="625" height="234" alt="image" src="https://github.com/user-attachments/assets/87fae637-af57-4d9f-b6f3-4377257cabd0" /><br>

#### Calculos Estadisticos
Se realizó un análisis estadístico descriptivo de la señal ECG con el objetivo de evaluar su comportamiento y variabilidad. Para ello se calcularon la media, varianza, desviación estándar, coeficiente de variación, asimetría y curtosis, además de analizar su distribución mediante un histograma.<br>

##### Estadistica Basica
```
media = np.mean(ecg)
varianza = np.var(ecg)
desviacion = np.std(ecg)
maximo = np.max(ecg)
minimo = np.min(ecg)

print("Media:", media)
print("Varianza:", varianza)
print("Desviación estándar:", desviacion)
print("Valor máximo:", maximo)
print("Valor mínimo:", minimo)
 
```
El código calcula estadísticas básicas de la señal capturada ECG utilizando funciones de **NumPy**. <br>
Se obtiene la media con `np.mean`<br>
la varianza con `np.var`<br>
la desviación estándar con `np.std`<br>
así como el valor máximo y mínimo mediante `np.max` y `np.min` respectivamente.<br> 
Finalmente, cada uno de estos resultados se imprime en pantalla, permitiendo realizar un análisis descriptivo de la señal
en términos de tendencia central, dispersión y valores extremos. <br>

| ESTADISTICO     | VALOR   |
|-----------------|----------|
| Media          | -1.4836  |
| Desviación estandar | 0.6316   |
|Varianza | 0.3989  |
| Maximo | 2.2227   |
| Minimo | -2.5081  |

- La media negativa indica la presencia de un desplazamiento DC en la señal, probablemente debido al sistema de adquisición o al generador biológico.<br>
- La desviación estándar refleja la variabilidad de la señal alrededor de su media, asociada a la amplitud de los complejos P-Q-R-S-T. <br>
- Eso indica que la amplitud total pico a pico es: 2.22 - (-2.50) ≈ 4.72 unidades <br>

###### Offset
Se eliminó el offset de la señal restando su valor medio.
Posteriormente, la media de la señal centrada fue aproximadamente cero, confirmando la correcta eliminación del desplazamiento. <br>

 ```
ecg_centrada = ecg - np.mean(ecg)
print("Nueva media:", np.mean(ecg_centrada))
```
| ESTADISTICO     | VALOR   |
|-----------------|----------|
| Nueva media | -1.865174681370263e-17 |

##### Estadistica Descriptiva Avanzada 



## PARTE C
