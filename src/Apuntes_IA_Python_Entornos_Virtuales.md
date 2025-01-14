# Apuntes Entornos virtuales en Python

Como establecer ambientes en Python

## Cómo crear un ENTORNO VIRTUAL en Visual Code con Python 2024 

https://www.youtube.com/watch?v=Fo-jkW8rPs8&t=434s


~~~
pip install virtualenv

virtualenv env

cd env/Scripts

Activate




~~~




---

## Por qué y cómo crear Ambientes Virtuales de Python usando venv y conda

https://www.youtube.com/watch?v=pSiPhHBw9yo


crear un ambiente virtual web
~~~
python -m venv web



python -m venv datos

# activar ambientes

cd web/scripts

Activate

python -m pip install request

# salir del ambiente

deactivate


# borrar un ambiente

rmdir /s datos





~~~


con anaconda manejar ambientes:

~~~

conda env list

conda create -n web

conda activate web

# para desactivar o salir del ambiente

conda deactivate

# para eliminar un ambiente

conda remove -n web





~~~




---




~~~


~~~




---
