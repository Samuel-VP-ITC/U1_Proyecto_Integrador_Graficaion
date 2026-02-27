# U1_Proyecto_Integrador_Graficaion

Generación Procedimental de Escenarios y Animación de Cámara

1. Resumen Ejecutivo
El script automatiza la creación de un entorno tridimensional consistente en un pasillo curvo generado matemáticamente. No se limita a colocar objetos estáticos, sino que sincroniza la geometría del entorno con una animación de cámara de 10 segundos, simulando un recorrido en primera persona que sigue la curvatura del diseño mediante funciones trigonométricas.

2. Análisis de Funciones Principales
   
A. Gestión de Escena y Materiales
limpiar_escena(): Utiliza operadores de Blender (bpy.ops) para seleccionar y eliminar todo rastro de objetos previos. Esto garantiza que el script sea idempotente (se puede ejecutar varias veces sin acumular basura en la escena).
crear_material(nombre, color_rgb): Esta función es fundamental para la estética. Activa el uso de nodos (el sistema estándar de Blender) y accede al componente Principled BSDF, que es un sombreador físicamente preciso (PBR). Configura el color base usando una tupla RGB.

B. Lógica de Generación (generar_pasillo_y_animar_camara)
Esta es la función "cerebro" del script. Se divide en tres etapas críticas:

Cálculo de la Curvatura (La Matemática):
El pasillo no es recto; sigue una función seno ($x = \sin(y)$).

amplitud_curva: Define qué tan "anchas" son las curvas.

frecuencia_curva: Define qué tan seguido cambia de dirección el pasillo.

Orientación de Objetos (Ángulo de Tangente):
El script calcula el ángulo entre la posición actual y la siguiente (math.atan2). Esto permite que las paredes y el suelo roten para estar siempre alineados con la dirección de la curva, evitando que el pasillo parezca una escalera dentada.

Generación de Geometría:
Crea cubos escalados para las paredes.
Usa un operador de alternancia (i % 2 == 0) para asignar materiales diferentes, creando un patrón visual rítmico.

3. Características Técnicas Destacadas
   Animación Cuadro por Cuadro (Frame-by-Frame)
A diferencia de los métodos tradicionales de "seguir camino" (path constraint) en Blender, este script calcula la posición exacta de la cámara para cada uno de los 240 frames (24 fps * 10s).
Interpolación manual: El script mapea el tiempo (frames) al progreso espacial (metros del pasillo).
Cálculo de Mirada (Look-at Logic): La cámara no solo se mueve, sino que "mira hacia adelante" calculando un punto futuro en la curva (progreso + 0.1). Esto es lo que da la sensación de conducción natural.

 Aspectos Matemáticos Aplicados
El código es un ejemplo perfecto de lo que discutimos en la Unidad 1.3:
Trigonometría: Uso de sin para la forma y atan2 para la rotación.
Transformaciones: Manipulación de location, scale y rotation_euler (Ángulos de Euler).

4. Ficha Técnica de Variables Críticas
Variable
Impacto en la Graficación
largo_pasillo
Define la complejidad de la malla (cantidad de polígonos).
altura_camara
Establece el punto de vista (POV) del usuario.
keyframe_insert
Registra los datos en la línea de tiempo para el renderizado final.

<img width="1903" height="984" alt="image" src="https://github.com/user-attachments/assets/94e49448-cdc0-4bff-9175-67e489785fe4" />
<img width="547" height="340" alt="image" src="https://github.com/user-attachments/assets/d11ec064-669d-4873-87c6-9054a1f0dee5" />



