### Codigo para blender
```python
import bpy
import math

# Limpiar la escena para no encimar objetos en cada ejecución 
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura 
radio = 3 
angulo_actual = 0
paso_angular = 60  # Cada 60 grados para obtener 6 círculos alrededor 

# 1. Círculo Central [cite: 35]
# Se dibuja el círculo base con centro en el origen (0,0,0) [cite: 12]
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0,0,0), vertices=64)

# 2. INICIO DEL PATRÓN REPETITIVO (Ciclo While)
# Establecer un límite: El ciclo se ejecuta mientras el ángulo sea menor a 360 
while angulo_actual < 360:
    
    # Calcular la nueva posición (x, y) convirtiendo coordenadas polares a cartesianas 
    # Se usa math.radians() porque sin() y cos() requieren radianes, no grados 
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    # Llamar a la función de Blender para añadir el círculo en esa nueva ubicación 
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    
    # Actualización de estado: Incrementar el ángulo sumándole el paso (60°) 
    # IMPORTANTE: Si esto falta, se crea un bucle infinito 
    angulo_actual += paso_angular
    
