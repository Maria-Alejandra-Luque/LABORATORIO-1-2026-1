# LABORATORIO-1
## ESTADISTICA

## PARTE A
En esta primera etapa se procedió a seleccionar y descargar una señal fisiológica desde la plataforma PhysioNet, verificando previamente que su duración fuera suficiente para permitir el cálculo adecuado de los estadísticos solicitados. Posteriormente, la señal fue cargada en el entorno de Python y se emplearon librerías como * matplotlib * para su visualización gráfica. Este proceso constituyó el punto de partida del estudio estadístico, apoyándose en herramientas computacionales que permiten caracterizar de manera precisa las principales propiedades de la señal analizada.
### CÓDIGO
Para el inicio del código para poder leer y procesar la señal fisiológica como un electrocardiograma (ECG), proveniente de un sitio web como fisionet, inicialmente se descargó la señal en los formatos. dat y .hea, estos formatos se guardaron en la misma carpeta del archivo. Posteriormente a eso se procedió a la instalación de la librería wfdb a través de anaconda prompt.ademas se hizo uso de la librería matplotlib para su visualización, en la gráfica se observan características típicas de un ECG como la onda P, el complejo QRS y las ondas T.
![Señal ECG](anacondaprompt.jpeg)
![Señal ECG](imagenecg.jpeg)
## PARTE B
Durante la segunda parte de nuestra practica, una señal fisiológica fue producida experimentalmente por medio del generador de señales biológicas del laboratorio.
Se empleó un sistema de adquisición de datos (DAQ) para obtenerlo, el cual fue conectado físicamente al PC por medio de USB y configurado con el controlador NI-DAQmx.
El DAQ recibió la señal analógica del generador, y esta fue transformada a digital. continuando la señal fue importada y procesada para asi realizar el correcto análisis 
estadístico y poder realizar su grafica correspondiente.De esta manera, se calcularon los parámetros estadísticos obtenidos en la Parte A y se comparó la señal descargada
de Physionet con la señal capturada usando el DAQ, lo que evidenció sus semejanzas y diferencias.
### ALGORITMO 
<img width="353" height="272" alt="image" src="https://github.com/user-attachments/assets/e1a0fc87-31bd-466e-b6f5-eec42b3aa14c" /><br>

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

```
from scipy.stats import skew, kurtosis
# Coeficiente de variación (usar señal original)
cv = np.std(ecg) / abs(np.mean(ecg))
print("Coeficiente de variación:", cv)
# Asimetría
print("Asimetría:", skew(ecg_centrada))
# Curtosis
print("Curtosis:", kurtosis(ecg_centrada))
```
Este código importa las funciones `skew` y `kurtosis` de la librería **SciPy** para calcular medidas estadísticas de la señal.
Primero, calcula el coeficiente de variación dividiendo la desviación estándar entre el valor absoluto de la media de la señal 
original (`ecg`). Luego, obtiene la asimetría y la curtosis de la señal centrada (`ecg_centrada`). Finalmente, imprime en pantalla cada uno de estos resultados. <br>

```
# Histograma
plt.figure(figsize=(6,4))
plt.hist(ecg_centrada, bins=30)
plt.title("Histograma de la señal ECG")
plt.xlabel("Amplitud")
plt.ylabel("Frecuencia")
plt.grid()
plt.show()
```
Este fragmento de código genera un histograma de la señal ECG centrada (`ecg_centrada`). Primero, se crea una figura con un tamaño de 6x4 pulgadas. Luego, se utiliza `plt.hist` para representar la distribución de los valores de la señal en 30 intervalos (bins), lo que permite observar la frecuencia con la que aparecen ciertas amplitudes. Finalmente, se agregan el título, las etiquetas de los ejes, una cuadrícula para facilitar la lectura y se muestra la gráfica en pantalla.<br>

| ESTADISTICO     | VALOR   |
|-----------------|----------|
|Coeficiente de variación | 0.4256958700697329 |
|Asimetría | 4.203297970920634 |
|Curtosis | 19.41228280465075 

<img width="425" height="282" alt="image" src="https://github.com/user-attachments/assets/d4bfe223-183f-456a-be18-5e8b51bfc25a" />

- El coeficiente de variación indica una variabilidad moderada de la señal respecto a su valor promedio, asociada principalmente a la presencia de los complejos QRS.<br>
- La asimetría positiva elevada indica que la distribución de amplitudes no es simétrica, presentando valores extremos positivos asociados a los picos R del complejo QRS. <br>
- La curtosis alta indica que la mayoría de los valores de la señal están concentrados cerca del promedio, pero existen algunos picos muy grandes. En el caso del ECG, esto se debe a los picos R del complejo QRS, que tienen una amplitud mayor que el resto de la señal. <br>

En general, el análisis estadístico permitió entender mejor el comportamiento de la señal ECG. Se observó que la mayoría de los valores se concentran alrededor de la línea base, pero existen picos altos asociados a los latidos, lo que hace que la distribución no sea normal. La variabilidad y los valores extremos obtenidos son coherentes con la forma típica de una señal electrocardiográfica. En conjunto, los resultados muestran que la señal fue correctamente adquirida y procesada. <br>


## PARTE C
