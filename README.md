[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=l23212181-creator/MSFP4)

# Práctica 4: Modelado y control del sistema endócrino

**Tecnológico Nacional de México — Instituto Tecnológico de Tijuana**  
**Departamento de Ingeniería Eléctrica y Electrónica — Ingeniería Biomédica**  
**Asignatura:** Modelado de Sistemas Fisiológicos  
**Docente:** Dr. Paul Antonio Valle Trujillo

**Alumno:** Jesús Geovanny Bautista Paz  
**Número de control:** 23212181  
**Correo institucional:** l23212181@tectijuana.edu.mx

Departamento de Ingeniería Eléctrica y Electrónica, Tecnológico Nacional de México/IT Tijuana, Blvd. Alberto Limón Padilla s/n, Tijuana, C.P. 22454, B.C., México.
## Contenido

1. [Resumen](#resumen)
2. [Competencia y objetivos](#objetivos)
3. [Relación con el temario](#temario)
4. [Modelo físico y analogía eléctrica](#analogia)
5. [Formulación matemática](#modelo)
6. [Análisis temporal y de estabilidad](#analisis)
7. [Señales de entrada y condiciones de simulación](#senales)
8. [Implementación en MATLAB, Simulink y Simscape](#matlab)
9. [Control en lazo cerrado y sintonización PID](#pid)
10. [Reproducción en Python](#python)
11. [Controlador analógico y laboratorio](#laboratorio)
12. [Resultados y verificación cruzada](#resultados)
13. [Flujo de trabajo](#flujo)
14. [Actividades del estudiante](#actividades)
15. [Estructura del repositorio](#estructura)
16. [Requisitos](#requisitos)
17. [Reproducibilidad y entregables](#reproducibilidad)
18. [Referencias](#referencias)

## Resumen

En esta práctica se desarrolla un modelo eléctrico equivalente de segundo orden para representar de manera simplificada la dinámica del sistema endócrino. Se consideran los procesos de estímulo fisiológico, secreción, transporte, almacenamiento y respuesta hormonal mediante una fuente de entrada, resistencias, un capacitor y un inductor. Se comparan dos condiciones: control y caso, modificando la capacitancia y la resistencia asociada con la utilización o eliminación de la señal. A partir de las funciones de transferencia se estudian el error en estado estacionario, los polos y la estabilidad. Finalmente, se implementa un controlador PID para aproximar la respuesta del caso a la respuesta de referencia y se comparan los resultados de MATLAB/Simulink, Python y laboratorio.

**Palabras clave:** sistema endócrino; modelado fisiológico; analogía eléctrica; circuito RLC; función de transferencia; sistema de segundo orden; estabilidad; error en estado estacionario; controlador PID; MATLAB; Simulink; Python; osciloscopio; respuesta hormonal.

## Competencia y objetivos

### Competencia a desarrollar

Modelizar sistemas fisiológicos mediante analogías eléctricas, ecuaciones diferenciales y funciones de transferencia para analizar su comportamiento dinámico y diseñar estrategias de control mediante técnicas de control clásico. En esta práctica se interpreta una descripción simplificada de los procesos de secreción, transporte, almacenamiento y respuesta hormonal, comparando una condición de referencia con una condición alterada.

### Objetivo general

Formular y analizar un circuito eléctrico equivalente de segundo orden que represente la dinámica simplificada del sistema endócrino, comparar las condiciones control y caso y diseñar un controlador PID que reduzca la diferencia entre sus respuestas.

### Objetivos específicos

- Identificar la correspondencia entre los procesos hormonales y los elementos del circuito equivalente.
- Obtener las funciones de transferencia para las condiciones control y caso.
- Calcular el error en estado estacionario y determinar la estabilidad mediante el análisis de polos.
- Simular las respuestas del sistema mediante MATLAB/Simulink y Python.
- Diseñar y sintonizar un controlador PID para aproximar la respuesta del caso a la respuesta de referencia.
- Contrastar las respuestas computacionales con las señales observadas en el laboratorio.

## Relación con el temario

La práctica integra el modelado de sistemas fisiológicos, la representación mediante circuitos eléctricos, la formulación de ecuaciones diferenciales, la transformada de Laplace, el análisis de sistemas de segundo orden y el diseño de controladores clásicos.

| Contenido | Aplicación en la práctica |
|---|---|
| Modelado fisiológico | Representación simplificada de la dinámica hormonal |
| Analogías eléctricas | Representación de transporte, almacenamiento y respuesta mediante R, C y L |
| Ecuaciones integro-diferenciales | Descripción de las relaciones entre entrada, salida y flujos |
| Transformada de Laplace | Obtención de las funciones de transferencia |
| Sistemas de segundo orden | Análisis de polos, estabilidad y respuesta temporal |
| Control clásico | Diseño y sintonización de un controlador PID |
| Simulación y experimentación | Comparación de MATLAB/Simulink, Python y osciloscopio |

## Modelo físico y analogía eléctrica

El modelo representa el estímulo fisiológico mediante una fuente de voltaje $V_e(t)$. La resistencia $R_1$ representa la oposición efectiva asociada al transporte hormonal. El capacitor $C$, conectado entre el nodo de salida y la referencia, representa la capacidad de almacenamiento temporal de la señal. La rama formada por el inductor $L$ y la resistencia $R_2$, conectados en serie, representa la dinámica retardada y la oposición asociada con la respuesta, utilización o eliminación de la señal en el órgano diana.

La salida $V_s(t)$ se mide en el nodo posterior a $R_1$, común al capacitor y a la rama $L-R_2$. El flujo de entrada se representa mediante $F_e(t)$, mientras que el flujo de salida se representa mediante $F_s(t)$. La analogía es fenomenológica: permite reproducir propiedades dinámicas como almacenamiento, disipación, retardo e inercia, sin establecer una equivalencia directa entre los valores eléctricos y parámetros hormonales medidos.

### Diagrama biológico

El diagrama relaciona el estímulo fisiológico, la glándula endócrina, el transporte hormonal, el almacenamiento y la respuesta del órgano diana con los elementos del circuito equivalente. También muestra la comparación entre la condición de control y la condición alterada.

![Diagrama BioRender de la Práctica 4: modelo del sistema endócrino en control y caso de hipertiroidismo](BIORENDER.jpeg)

### Parámetros utilizados

| Componente | Control | Caso |
|---|---:|---:|
| $R_1$ | 1 kΩ | 1 kΩ |
| $L$ | 100 mH | 100 mH |
| $C$ | 1 µF | 1000 µF |
| $R_2$ | 100 kΩ | 1 kΩ |

La condición control representa la referencia. En el caso se incrementa la capacitancia y se reduce $R_2$, modificando la dinámica y el valor final de la respuesta.

## Formulación matemática

### 1. Ecuaciones del circuito

A partir de las leyes de Kirchhoff, las relaciones del circuito equivalente pueden expresarse como:

$$
V_e(t)=R_1F_e(t)+\frac{1}{C}\int [F_e(t)-F_s(t)]\,dt
$$

$$
\frac{1}{C}\int [F_e(t)-F_s(t)]\,dt
=L\frac{dF_s(t)}{dt}+R_2F_s(t)
$$

La salida se expresa mediante la rama inductiva-resistiva:

$$
V_s(t)=L\frac{dF_s(t)}{dt}+R_2F_s(t)
$$

### 2. Función de transferencia

Aplicando la transformada de Laplace con condiciones iniciales nulas, se obtiene:

$$
G(s)=\frac{V_s(s)}{V_e(s)}
=\frac{Ls+R_2}
{R_1LCs^2+(L+R_1R_2C)s+(R_1+R_2)}
$$

Para la condición control, utilizando $R_1=1\,k\Omega$, $L=0.1\,H$, $C=1\,\mu F$ y $R_2=100\,k\Omega$:

$$
G_{\mathrm{control}}(s)=
\frac{0.1s+100000}
{0.0001s^2+100.1s+101000}
$$

Para la condición caso, utilizando $R_1=1\,k\Omega$, $L=0.1\,H$, $C=1000\,\mu F$ y $R_2=1\,k\Omega$:

$$
G_{\mathrm{caso}}(s)=
\frac{0.1s+1000}
{0.1s^2+1000.1s+2000}
$$

Estas funciones corresponden a las expresiones implementadas en el programa de Python mediante `control.tf`.

## Análisis temporal y de estabilidad

### 1. Error en estado estacionario

Para una entrada escalón unitario, la ganancia en estado estacionario se obtiene evaluando la función de transferencia en $s=0$:

$$
G(0)=\frac{R_2}{R_1+R_2}
$$

El error final respecto a la entrada unitaria es:

$$
e_{ss}=1-G(0)=\frac{R_1}{R_1+R_2}
$$

| Condición | Ganancia final | Error en estado estacionario |
|---|---:|---:|
| Control | 0.990099 | 0.009901 (aprox. 0.99 %) |
| Caso | 0.5 | 0.5 (50 %) |

La diferencia entre los valores finales de las respuestas control y caso es aproximadamente 0.490099 V para una entrada de 1 V.

### 2. Polos y estabilidad

Los polos se determinan mediante las raíces del denominador de cada función de transferencia. Para la condición control, el denominador es $0.0001s^2+100.1s+101000$; para el caso, es $0.1s^2+1000.1s+2000$. Los polos de ambos sistemas se encuentran en el semiplano izquierdo, por lo que las dos condiciones presentan estabilidad.

### 3. Interpretación de la respuesta temporal

La condición control alcanza un valor final cercano a 1 V, mientras que la condición caso se aproxima a 0.5 V. Esta diferencia permite observar el efecto de los cambios en los elementos de almacenamiento y disipación del modelo. El controlador se utiliza para reducir la diferencia entre la respuesta del caso y la respuesta de referencia.

## Señales de entrada y condiciones de simulación

La señal de entrada utilizada es un escalón unitario:

$$
V_e(t)=u(t)
$$

En Python se establece un intervalo de simulación de 0 a 10 segundos, con un paso de $1\times10^{-3}$ s y 10001 muestras. En MATLAB/Simulink se utiliza un tiempo de simulación de 10 s, el solucionador `ode15s` y un paso máximo de `1e-3` s.

## Implementación en MATLAB, Simulink y Simscape

La implementación de MATLAB/Simulink se encuentra en el modelo `sistemap5.slx`. La ejecución se realiza desde el cuaderno `Bautista23212181_4.mlx`, configurando el tiempo de simulación, el solucionador y el paso máximo.

```matlab
clc; clear; close all; warning('off','all')
open_system('sistemap5')
parameters.StopTime = '10';
parameters.Solver = 'ode15s';
parameters.MaxStep = '1e-3';
x = sim('sistemap5',parameters);
```

Las señales se representan mediante la función `plotsignals`, utilizando las salidas de control, caso, tratamiento PID y entrada:

```matlab
plotsignals(x.control,x.CE,x.FT,x.PID,x.Ve,'Caso')
```

La evidencia de MATLAB/Simulink muestra las cuatro señales en el intervalo de 0 a 10 segundos. La respuesta del caso alcanza aproximadamente 0.5 V, mientras que la referencia y la respuesta tratada se mantienen próximas a 1 V.


## Control en lazo cerrado y sintonización PID

### 1. Esquema de control

La respuesta del sistema en condición control se utiliza como referencia para el sistema en condición caso. El controlador PID actúa sobre la planta del caso para aproximar su respuesta a la referencia. El error de seguimiento se define como:

$$
e(t)=V_{s,\mathrm{control}}(t)-V_{s,\mathrm{caso}}(t)
$$

### 2. Parámetros del controlador

La captura de PID Tuner muestra la configuración PIDF y los parámetros del bloque:

| Parámetro | Valor mostrado |
|---|---:|
| $P$ | 2.617 |
| $I$ | 10.49 |
| $D$ | -0.0459 |
| $N$ | 6.016 |

La gráfica de sintonización presenta la respuesta ajustada y la respuesta del bloque ante una referencia escalón. La respuesta ajustada muestra un sobreimpulso antes de aproximarse al valor de referencia.


### 3. Implementación del controlador en Python

En el script de Python se utilizan las ganancias:

$$
k_P=13209.9564,\qquad
k_I=32316525.9285,\qquad
k_D=0.18118
$$

A partir de estas ganancias y de los componentes $C_r$, $R_e$, $R_r$ y $C_e$, se construye la función de transferencia del controlador. Posteriormente, se conecta en serie con la planta del caso y se obtiene el sistema en lazo cerrado mediante realimentación unitaria.

## Reproducción en Python

El archivo `Bautista23212181_4.py` reproduce las funciones de transferencia de control y caso, construye el controlador PID y calcula las respuestas temporales mediante la biblioteca `control`.

### Bibliotecas utilizadas

```python
import numpy as np
import math as m
import control as ctrl
import matplotlib.pyplot as plt
```

### Parámetros de simulación

```python
x0, t0, tend, dt, w, h = 0, 0, 10, 1E-3, 10, 5
N = round(tend/dt) + 1
t = np.linspace(t0, tend, N)
u = np.ones(N)
```

### Obtención de las plantas

La función `sis(C, R2, nombre)` utiliza $R_1=1\,k\Omega$ y $L=100\,mH$, y calcula los coeficientes del numerador y denominador para cada condición:

```python
def sis(C, R2, nombre):
    R1, L = 1E3, 100E-3
    num = [L, R2]
    den = [C*L*R1, C*R1*R2+L, R1+R2]
    sys = ctrl.tf(num, den)
    print(f"Función de transferencia {nombre}: {sys}\n")
    return sys

sysControl = sis(1E-6, 100E3, "Control")
sysCaso = sis(1000E-6, 1E3, "Caso")
```

### Respuestas del sistema

El programa calcula la respuesta de cada planta ante el escalón unitario y la respuesta del sistema controlado. Finalmente, genera la gráfica comparativa y guarda el resultado como `Control_caso_python4.pdf`.

[Consultar la gráfica generada por Python](Control_caso_python4.pdf)

## Controlador analógico y laboratorio

Se realizó la comparación experimental de las señales mediante el osciloscopio OWON. La captura muestra las respuestas medidas para las condiciones implementadas en el circuito, con escalas verticales de 500 mV por división y una base de tiempo de 1.0 s por división.

La señal experimental permite observar la diferencia entre la respuesta de referencia y la respuesta del caso, así como el comportamiento de la señal tratada. La medición complementa los resultados obtenidos mediante las simulaciones computacionales.


## Resultados y verificación cruzada

Los resultados de las distintas representaciones permiten comparar las condiciones control y caso y observar el efecto del controlador PID.

| Representación | Evidencia | Resultado observado |
|---|---|---|
| Análisis matemático | Funciones de transferencia y cálculos | Ganancia final de aproximadamente 0.9901 para control y 0.5 para caso |
| MATLAB/Simulink | `Captura_Matlab.pdf` | La respuesta control se mantiene próxima a 1 V y el caso se aproxima a 0.5 V |
| Python | `Control_caso_python4.pdf` | Se reproducen las respuestas de ambas plantas y el tratamiento PID |
| PID Tuner | `PID controller.jpg` | Se muestra el ajuste del controlador y el seguimiento de referencia |
| Laboratorio | `Señal_Lab.jpeg` | Se observan las señales medidas experimentalmente con el osciloscopio |

La comparación confirma que la condición caso presenta una respuesta final menor que la condición control. La acción del controlador busca aproximar la salida del caso a la respuesta de referencia. Las diferencias entre las representaciones pueden asociarse con las condiciones de simulación y las características no ideales de los componentes e instrumentos utilizados.

## Flujo de trabajo

1. Interpretar la descripción fisiológica del sistema endócrino.
2. Proponer el circuito eléctrico equivalente e identificar $R_1$, $C$, $L$ y $R_2$.
3. Formular las ecuaciones integro-diferenciales mediante las leyes de Kirchhoff.
4. Aplicar la transformada de Laplace y obtener las funciones de transferencia.
5. Calcular el error en estado estacionario y analizar los polos de control y caso.
6. Implementar las plantas en MATLAB/Simulink y Python.
7. Diseñar y sintonizar el controlador PID para el seguimiento de la respuesta de referencia.
8. Obtener las respuestas experimentales con el osciloscopio.
9. Comparar y documentar los resultados en el repositorio.

## Actividades del estudiante

- [x] Construcción del circuito eléctrico equivalente para las condiciones control y caso.
- [x] Obtención de las funciones de transferencia.
- [x] Análisis del error en estado estacionario.
- [x] Análisis de estabilidad mediante los polos.
- [x] Bosquejo y comparación de las respuestas temporales.
- [x] Formulación del modelo mediante ecuaciones integro-diferenciales.
- [x] Implementación y simulación en MATLAB/Simulink.
- [x] Reproducción de las respuestas mediante Python.
- [x] Diseño y sintonización del controlador PID.
- [x] Obtención de evidencia experimental mediante osciloscopio.
- [x] Elaboración del diagrama biológico.
- [x] Documentación de resultados y evidencias para el repositorio.

## Estructura del repositorio

```text
MSFP4/
├── README.md
├── CITATION.cff
├── sistemap5.slx
├── Bautista23212181_4.mlx
├── Bautista23212181_4.py
├── Captura_Matlab.pdf
├── Control_caso_python4.pdf
├── PID controller.jpg
├── Señal_Lab.jpeg
└── Sistema endocrino.png
```

Los nombres del árbol corresponden a los archivos entregados para documentar la práctica. Se recomienda conservarlos sin cambios o actualizar los enlaces del README si se renombran.

## Requisitos

Para reproducir las simulaciones se requiere:

- MATLAB con Simulink.
- Python 3.
- Bibliotecas de Python: `numpy`, `control` y `matplotlib`.
- El modelo `sistemap5.slx`.
- El archivo de código `Bautista23212181_4.py`.
- El cuaderno de MATLAB `Bautista23212181_4.mlx`.

Instalación de las bibliotecas de Python:

```bash
pip install numpy control matplotlib
```

## Reproducibilidad y entregables

Para reproducir los resultados, colocar los archivos del modelo, el cuaderno y el código Python en el directorio de trabajo correspondiente. Ejecutar el modelo de Simulink desde MATLAB con el solucionador `ode15s`, tiempo final de 10 segundos y paso máximo de `1e-3` s. Para la reproducción en Python, ejecutar `Bautista23212181_4.py`.

Los entregables documentados en el repositorio son:

- Diagrama biológico del sistema endócrino.
- Desarrollo matemático y funciones de transferencia.
- Modelo de Simulink y cuaderno de MATLAB.
- Código fuente de Python.
- Gráficas de las respuestas de MATLAB/Simulink y Python (`Captura_Matlab.pdf` y `Control_caso_python4.pdf`).
- Captura de la sintonización PID.
- Evidencia experimental obtenida con el osciloscopio.
- Archivo `README.md` y archivo `CITATION.cff`.

## Referencias

1. M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.
2. F. C. Hoppensteadt and C. S. Peskin, *Modeling and Simulation in Medicine and the Life Sciences*, Springer.
3. J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.
4. K. Ogata, *Ingeniería de Control Moderna*, 5.ª ed., Pearson Educación, 2010.
5. N. S. Nise, *Control Systems Engineering*, 8th ed., John Wiley & Sons, 2020.
6. P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México, Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2026.
7. Tecnológico Nacional de México, *Programa de estudio de la asignatura Modelado de Sistemas Fisiológicos*, IBF-1020.

## Uso académico

Este repositorio se presenta con fines académicos como evidencia del desarrollo de la Práctica 4 de la asignatura Modelado de Sistemas Fisiológicos, del programa de Ingeniería Biomédica del Tecnológico Nacional de México, Instituto Tecnológico de Tijuana.
