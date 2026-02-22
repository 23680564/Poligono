# Generar un poligono 2D

## Explicacion para crear el poligono

Este ejercicio consiste en la creacion un poligono 2D usando **Python** en Blender mediante la API bpy
El codigo genera una malla personalizada calculando los vertices mediante trigonometria y conectandolos a traves de aristas para formar una figura cerrada.

--

# Objetivo de la creacion del proyecto

-Comprender y analizar el uso de la API bpy de Blender.
-Generar mallas manualmente mediante el uso de python.
-Automatizar la creacion de la geometria dentro de Blender.
-Aplicar la conversion de coordenadas polares  a cartesianas.

--

# Explicacion del codigo

# Importacion de librerias de Python

`import bpy
import math`

- bpy: Nos permite interactuar con Blender a nivel interno
- math: Esta se utiliza para realizar calculos automaticos como seno, coseno y pi

# Creacion de malla y el objeto

`malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)
bpy.context.collection.objects.link(objeto)

Aqui se:

- Se crea una nueva estructura de malla
- Crea un objeto de usa la malla
- Vinculamos el objeto a la coleccion activa de la escena

  # Calculo de vertices

  `for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio *  math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) #Z = 0 para mantenerlo en 2D
  `

  Se realiza:

  -Division del circulo completo en (2pi radianes) entre el numero de lados.
  -Conversion de coordenadas polares a cartesianas
  -Se fija Z = 0 para mantener la figura en el plano 2D.

  # Creacion de aristas

  `for i in range(lados):
            aristas.append((i, (i + 1) % lados))`
  Cada vertice se conecta con el siguiente.
  El operador modulo (%) permite que el ultimo vertice se conecte nuevamente con el primero, cerrando la figura

  # Carga de datos en la malla
  `malla.from_pydata(vertices, aristas, [])
    malla.update()`

  Aqui se cargan:
  Lista de vertices
  Lista de aristas
  Lista de caras (vacia en este caso)

  # Limpieza de escena

  `bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()`

Se eliminan todos los objetos antes de crear el nuevo poligono para evitar superposicion

# Llamada final

`crear_poligono_2d("Poligono2D", lados=6, radio=5)
`

## Como ejecuta el codigo

1. Abrir Blender.
2. Ir a la pestaña **Scripts**

   <img width="1056" height="28" alt="image" src="https://github.com/user-attachments/assets/f90ca054-a144-4938-b5d1-87c6d368459d" />
3. Generar un nuevo scripts
4. Generar codigo
5. Darle en el icono de **Run**
   <img width="35" height="30" alt="image" src="https://github.com/user-attachments/assets/954d90a7-6ba0-4a0d-926b-18b5840ce8f9" />
6. Esperar que se ejecute el codigo

   ---

   # Parametros configurales
   En la ultima linea del codigo se puede modificar python

   crear_poligono_2d("Poligono2D", lados=6, radio=5)

   - Lados -> l numero de lados del poligono
   - radio -> El tamaño del poligono
  
     ---

     # Codigo completo
     <img width="512" height="546" alt="image" src="https://github.com/user-attachments/assets/91176203-e303-4413-9d6e-3d201a11158a" />
```import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    #Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    
    #Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)
    
    vertices = []
    aristas = []
    
    #Calculo de vertices usando coordernadas palares cartesianas
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio *  math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) #Z = 0 para mantenerlo en 2D
        
     # Definir las conexiones (aristas) entre los vertices
    for i in range(lados):
            aristas.append((i, (i + 1) % lados))
            
    # Cargar los datos en la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()
            
# Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
            
# Llamada a la funciom : UN hexagono de radio de 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
---

## Resultado

   <img width="398" height="499" alt="image" src="https://github.com/user-attachments/assets/caa3fdb4-1779-4955-9917-b518f8b73987" />

