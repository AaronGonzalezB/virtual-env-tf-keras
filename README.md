# Virtual env with Python/Tensorflow/Keras
### How to set a virtual env to work without headaches


The file contain the details to set a virtual env with Python, then explain how to install TF inside the env and finally Keras to work with it.

#### 1.  Crear un entorno virtual con Anaconda

Permite instalar paquetes individuales como TensorFlow y Keras con Python 3.6

```conda create -n myenv python=3.6```
#### 2. Crear un entorno virtual con pip

Para esto debes tener anadido al PATH tanto Python como pip, por cmd se anaden asi:

1. Anadir pip en este equipo:

```setx PATH "%PATH%;C:\ProgramData\Anaconda3\Scripts```

2. Anadir Python en este equipo (usando la version instalada con Anaconda):

```setx PATH "%PATH%;C:\ProgramData\Anaconda3\python.exe```

3. Ahora instalamos el virtualenv con pip:

```pip install virtualenv```

4. Creamos un directorio para almacenar los entornos virtuales creados

```mkdir virtualenviroment```

5. Creamos el entorno virtual, este vendra con la distribucion de Python instalada dentro de la maquina

```virtualenv env```

6. Ingresamos a la carpeta donde creamos el entorno, y la activamos:

```
cd env
activate
```

### 3. Instalar tensorflow dentro del entorno virtual

Dentro del entorno virtual creado con Python 3.6 (la version 3.7 aun no es compatible con tf):

1. Instalamos tensorflow con pip:

```pip install tensorflow```

Probamos dentro de la consola de Python si permite importar la libreria:

```python
>>> import tensorflow as tf
```

Si presenta el siguiente error:

```python
ImportError: DLL load failed: The specified module could not be found.
```

2. Intentamos actualizar la instalacion de tensorflow

```pip install --upgrade tensorflow```

3. Si la falla continua, es necesario instalar el complemento ``` tensorflow-1.6.0-cp36-cp36m-win_amd64.whl ``` que se encuentra en el siguiente enlace:

https://github.com/fo40225/tensorflow-windows-wheel/tree/master/1.6.0/py36/CPU/sse2

Dentro del directorio donde esta el complemento, instalar con pip:

```pip install tensorflow-1.6.0-cp36-cp36m-win_amd64.whl```

4. (Opcional) si la falla aun persiste, es necesario verificar la version del paquete ```protobuf``` e instalar la version 3.6

```pip install protobuf==3.6.0```

Con esto al probar importar tensorflow dentro de la consola de Python deberia funcionar. En caso de que se presenten algun Warning como este:

```python
FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
```

En este caso la advertencia indica que la version de numpy que tenemos en el entorno no es compatible con la version de tensorflow instalada (las versiones de numpy aceptadas por tensorflow hasta ahora son entre ``` >=1.13.3 y <=1.14.5 ```), por ende es recomendable hacer un downgrade de la version de numpy:

```
pip uninstall numpy 
pip install numpy==1.16.4
```

Esto aplicable para otras librerias que probablemente no sean compatibles. Con esto se tendria el entorno configurado para trabajar con la version actual de tensorflow

### 4. Instalar keras dentro del entorno

Keras es compatible con la version 3.7 actual de Python. Se recomienda crear un entorno virtual aparte:

1. Crear el entorno virtual con conda (recomendado):

```conda create -n keras```

2. Activar el entorno:

```activate keras```

3. Garantizar que el entorno tenga las siguientes dependencias:

Son necesarias para la posterior instalacion de keras, en caso de no tener alguna instalarla manualmente con pip (aunque si el ambiente fue creado con conda este viene con estas librerias por defecto)

* Numpy.
* Pandas.
* Scikit-learn.
* Matplotlib.
* Scipy.
* Seaborn.

4. Instalar keras con conda:

```conda install -c anaconda keras```

5. Verificar la instalacion desde la consola de Python importando algun paquete:

```python
from keras.models import Sequential
```

### 5. Activar el entorno virtual dentro de Jupyter Notebook

Se debe tener cerrado Jupyter. Para trabajar bajo el entorno virtual ya creado en los paso anteriores:

1. Activar el entorno virtual con el que se desea trabajar en Jupyter.

2. Instalar el paquete para integrar el entorno con pip:

```pip install --user ipykernel```

3. Implementar un nuevo kernel en Jupyter con las caracteristicas del entorno virtual en el que estamos:

```python -m ipykernel install --user --name keras_jupyter --display-name "Python (Keras_jupyter)"```

4. Abrir Jupyter Notebook y en el menu Kernel verificar que el entorno haya quedado guardado.
