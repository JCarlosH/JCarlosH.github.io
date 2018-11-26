---
layout: post
title: Python Json
date: 2018-11-25 05:41:01 -0500
---

Trabajando con json desde python.En [Wikipedia](https://es.wikipedia.org/wiki/JSON) podemos leer lo siguiente:

> JSON (acrónimo de JavaScript Object Notation, «notación de objeto de JavaScript») es un formato de texto ligero para el intercambio de datos. JSON es un subconjunto de la notación literal de objetos de JavaScript aunque hoy, debido a su amplia adopción como alternativa a XML, se considera un formato de lenguaje independiente.

Sobre la libreria json de python encontramos en [recursospython.com](https://recursospython.com/guias-y-manuales/json/) lo siguiente:

>A partir de la versión 2.6 Python incorpora en su librería estándar el módulo json, con una API similar a la de pickle, para codificar y decodificar información en el formato JSON. “Codificar” y “decodificar” deben ser entendidos como convertir de un objeto Python a JSON y viceversa.

## Empezando
primero debemos importar la libreria json dentro de nuestro archivo python de la siguiente manera:
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json
```

Nuestra estructura de carpetas deberia se la siguiente:  
carpeta
1. pythonfile.py
2. file.json

dentro de nuestro arhivo json tendremos los siguiente:
```json
{
	"colores":["verde","rojo","azul","amarillo"],
    "alimentos":{
    	"bebidas":["soda","te","chocolate"],
    	"comidas":["sopa","arroz"]
    }
}
```

### Leer json
Desde python añadimos las siguientes lineas para leer nuestro archivo json desde python:
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json


# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# Todo
print(diccionario)

# vemos su contenido de un elemento
print(diccionario["pais"])

#En un for
for item in diccionario["pais"]:
	print(item)
```

Con esto nos dara el resultado que hemos guardado dentro del json.  
```bash
{u'colores': [u'verde', u'rojo', u'azul', u'amarillo'], u'alimentos': {u'bebidas': [u'soda', u'te', u'chocolate'], u'comidas': [u'sopa', u'arroz']}}

[u'Mexico', u'Peru', u'Chile']

Mexico
Peru
Chile

```

### Añadir datos a json
Basicamente el proceso es:
1. Abrir archivo json
2. Almacenar el contenido en una variable de tipo diccionario
3. Trabajar con nuestro diccionario
4. Rescribir de nuevo el diccionario en nuestro archivo json



#### Añadir un dato al diccionario
Lo basico seria añadir un simple dato al archivo json, como lo haremos a continuacion
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json


# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

#creamos un key
dato = "propietario"

# creamos un valor
valor= "Kiko"

#agregamos estos datos al diccionario
diccionario[dato] = valor

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```
si revisamos el archivo json veremos el cambio
```json
{
	"propietario": "Kiko", 
	"colores": ["verde", "rojo", "azul", "amarillo"], 
	"alimentos": 
	{
		"bebidas": ["soda", "te", "chocolate"], 
		"comidas": ["sopa", "arroz"]
	}
}
```
#### Añadir una lista al diccionario
Lo que añadiremos son un key llamado pais y su valor sera una lista con datos como se muestra en nuestro codigo:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json


# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

#creamos un key
estado = "pais"

# creamos los values
valor= ["Mexico","Peru","Chile"]

#agregamos estos datos al diccionario
diccionario[estado] = valor

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```

Si vamos a nuestro archivo podemos encontrar que nuestro key de pais se ha añadido correctamente:
```json
{
	"pais": ["Mexico", "Peru", "Chile"], 
	"propietario": "Kiko", 
	"colores": ["verde", "rojo", "azul", "amarillo"], 
	"alimentos": 
	{
		"bebidas": ["soda", "te", "chocolate"], 
		"comidas": ["sopa", "arroz"]
	}
}
```


#### Añadir un diccionario
En este ejemplo colocamos un diccionario dentro de otro diccionario, si bien existen otros ejemplos que talvez
puedan serte de ayuda qui lo haremos de la suguiente manera:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json

# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

# creamos un diccionario para los coches
coches = {}

# llenamos el diccionario con listas, o puede se un dato normal
coches["Nombre"] = ["Nissan","Ford"] 
coches["Estado"] = ["Nuevo","Usado"] 

# fusionamos el diccionario json mas el diccionario creado
diccionario["coches"]=coches

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```

Si vamos a nuestro archivo podemos encontrar que nuestro diccionario añadido.
```json
{
	"coches": 
	{
		"Nombre": ["Nissan", "Ford"], 
		"Estado": ["Nuevo", "Usado"]
	}, 
	"propietario": "Kiko", 
	"colores": ["verde", "rojo", "azul", "amarillo"], 
	"pais": ["Mexico", "Peru", "Chile"], 
	"alimentos": 
	{
		"bebidas": ["soda", "te", "chocolate"], 
		"comidas": ["sopa", "arroz"]
	}
}
```

Otros ejemplos practicos como añadir directamente a un lugar especifico

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json

# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

# Agregar a la lista un elemento mas
diccionario["alimentos"]["bebidas"].append("Atole")

# Actualizar un elemento de la lista
diccionario["alimentos"]["comidas"][1] = "Arroz"

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```

### Quitar elementos
Eliminar elementos de un diccionario es facil, solo basta colocar 
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json

# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

#
diccionario.pop("coches")

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```
y asi de simple eliminamos un key
```json
{
	"propietario": "Kiko", 
	"colores": ["verde", "rojo", "azul", "amarillo"], 
	"pais": ["Mexico", "Peru", "Chile"], 
	"alimentos": 
	{
		"bebidas": ["soda", "te", "chocolate"], 
		"comidas": ["sopa", "arroz"]
	}
}
```

o asi:
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json

# abrimos nuestro archivo json
with open("file.json","r") as file:
	diccionario = json.load(file)

# vemos su contenido
print(diccionario)

# eliminamos "soda" de bebidas-alimentos
diccionario["alimentos"]["bebidas"][0].pop()

#vemos como quedo el array
print(diccionario)

# Escribimos el nuevo diccionario en el archivo
with open("file.json","w") as file:
	json.dump(diccionario,file)
```
```json
{
	"propietario": "Kiko", "colores": ["verde", "rojo", "azul", "amarillo"], 
	"alimentos": 
	{
		"bebidas": ["te", "chocolate"], 
		"comidas": ["sopa", "arroz"]
	}, 
	"pais": ["Mexico", "Peru", "Chile"]
}
```


## Metodos del diccionario python

```python
# Declaración de un diccionario
diccionario = dict()

# Devuelve el numero de elementos que tiene el diccionario
len(dict)

# Compara el número de elementos distintos que tienen los dos 
cmp (dict1,dict2)

# Devuelve una lista con las claves del diccionario
dict.keys()

# Devuelve una lista con los valores del diccionario
dict.values()

# Devuelve el valor del elemento con clave key. Sino devuelve default
dict.get(key, default=None)

# Inserta un elemento en el diccionario clave:valor. Si la clave existe no lo inserta
dict.setdefault(key, default=None)

# Insertamos un elemento en el diccionario con su clave:valor
dict['key'] = 'value'

# Eliminamos el elemento del diccionario con clave key
dict.pop('key',None)

# Devuleve la copia de un diccionario dict2 = dict.copy()
dict.copy()

# Elimina todos los elementos de un diccionario
dict.clear()

# Crea un nuevo diccionario poniendo como claves las que hay en la lista y los valores por defecto si se les pasa
dict.fromkeys(list, defaultValue)

# Devuelve true si existe la clave. Sino devuelve false
dict.has_key(key)

# devuelve un lista de tuplas formadas por los pares clave:valor
dict.items()

# Añade los elementos de un diccionario a otro
dict.update(dict2)
```