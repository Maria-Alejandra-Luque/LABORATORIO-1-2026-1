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
Este fragmento de código se encarga de graficar la señal ECG en función del tiempo. Primero, se crea una figura con un tamaño de 12x4 pulgadas para mejorar la visualización.
Luego, se traza la señal utilizando `plt.plot(tiempo, ecg)`, donde el eje horizontal corresponde al tiempo y el eje vertical a la amplitud. Finalmente, se añaden el título,
las etiquetas de los ejes, una cuadrícula para facilitar la lectura de la gráfica y se muestra el resultado en pantalla con `plt.show()`.
<img width="625" height="234" alt="image" src="https://github.com/user-attachments/assets/87fae637-af57-4d9f-b6f3-4377257cabd0" />


## PARTE C
