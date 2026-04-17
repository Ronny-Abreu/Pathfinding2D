## Búsqueda de Salida en Laberinto mediante Exploración Paralela y Recursiva

Este proyecto implementa una solución algorítmica para resolver laberintos representados en matrices bidimensionales, utilizando un enfoque de **computación paralela**. A diferencia de los algoritmos de búsqueda tradicionales secuenciales, este sistema aprovecha la recursividad para disparar hilos o tareas paralelas cada vez que se encuentra una bifurcación.

## 🚀 Características del Proyecto

- **Exploración Multitarea:** Ante cada intersección (bifurcación), el programa no elige un camino al azar; en su lugar, utiliza la recursividad para crear tareas paralelas que exploran todas las rutas simultáneamente.
- **Sincronización de Datos:** Implementa un **Log Global** compartido donde todas las tareas registran sus movimientos y los "callejones sin salida". Se utilizan mecanismos de sincronización para garantizar la integridad de los datos.
- **Descomposición Recursiva:** La lógica de exploración se invoca de manera recursiva por cada nueva ruta disponible, permitiendo una estructura de código limpia y eficiente.
- **Escalabilidad:** El sistema está diseñado para escalar su rendimiento conforme aumenta la complejidad del laberinto y la cantidad de núcleos de procesamiento disponibles.

## 🛠 Arquitectura Técnica

### 1. Representación del Laberinto
El laberinto se define como una matriz de `N x M` donde:
- `0`: Camino libre.
- `1`: Pared / Obstáculo.
- `S`: Punto de inicio.
- `E`: Salida (Exit).

### 2. Estrategia de Paralelismo
Cuando el explorador llega a una coordenada con múltiples direcciones válidas:
1. Identifica las rutas posibles.
2. Genera una nueva tarea/hilo por cada ruta (excepto la actual).
3. Cada tarea hija reporta sus hallazgos al hilo principal y al log global.

### 3. Sincronización y Log Global
Dado que múltiples tareas escriben en un mismo recurso (el log), se han implementado bloqueos (mutex/locks) para prevenir condiciones de carrera (*race conditions*), asegurando que el rastro de la ruta final y los intentos fallidos se registren correctamente.

## 📊 Métricas de Rendimiento
El proyecto incluye un módulo de evaluación para comparar:
- **Explorador Single-Thread:** Tiempo de resolución utilizando una búsqueda en profundidad (DFS) estándar.
- **Explorador Parallel:** Tiempo de resolución utilizando la ejecución concurrente de rutas.

*Se espera una reducción significativa en el tiempo de ejecución en laberintos con alta densidad de bifurcaciones y gran tamaño.*
