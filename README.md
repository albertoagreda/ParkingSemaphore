# 🚗 Control de Acceso Concurrente a un Aparcamiento con Semaphore

## 📘 Descripción General
Este proyecto simula el acceso concurrente de varios coches a un aparcamiento con plazas limitadas.  
Se utiliza la clase `java.util.concurrent.Semaphore` para controlar cuántos coches pueden aparcar al mismo tiempo.

## 🎯 Objetivos
- Comprender el uso de la clase **Semaphore** para gestionar recursos limitados.  
- Implementar sincronización de hilos para controlar el acceso concurrente a un recurso compartido.  
- Simular la entrada y salida de vehículos de forma concurrente y segura.

## 🧩 Estructura del Proyecto
```
src/
└── parking/
    ├── Aparcamiento.java      # Controla el acceso a las plazas mediante un Semaphore
    ├── Coche.java             # Representa cada vehículo que intenta aparcar
    └── PrincipalParking.java  # Crea y ejecuta los hilos que simulan los coches
```

## ⚙️ Clases Principales

### 🅰️ Aparcamiento
- Usa un `Semaphore` con capacidad de **3 permisos**.  
- Gestiona cuántos coches pueden entrar al mismo tiempo.  
- Métodos:
  - `entrar(String nombreCoche)`: intenta adquirir una plaza.
  - `salir(String nombreCoche)`: libera la plaza ocupada.

### 🚘 Coche
- Implementa `Runnable`.  
- Simula un coche que:
  1. Intenta entrar al aparcamiento.  
  2. Permanece aparcado un tiempo aleatorio (1–4 segundos).  
  3. Sale y libera la plaza.

### 🏁 PrincipalParking
- Punto de entrada del programa.  
- Crea un aparcamiento con **3 plazas**.  
- Lanza **7 hilos** que representan coches.  
- Espera a que todos terminen antes de finalizar la simulación.

## 🧠 Lógica del Funcionamiento
- Solo **3 coches** pueden estar aparcados simultáneamente.  
- El resto espera a que se libere una plaza.  
- Cuando un coche sale, el semáforo libera un permiso y permite entrar al siguiente coche.

## 🧪 Ejemplo de Salida Esperada
```
[1731251234567][HILO-2] Coche-2 ha ENTRADO. Ocupadas=1 | Libres=2
[1731251234581][HILO-3] Coche-3 ha ENTRADO. Ocupadas=2 | Libres=1
[1731251234590][HILO-1] Coche-1 ha ENTRADO. Ocupadas=3 | Libres=0
[1731251237620][HILO-2] Coche-2 ha SALIDO. Ocupadas=2 | Libres=0
[1731251237621][HILO-4] Coche-4 ha ENTRADO. Ocupadas=3 | Libres=0
...
Simulación finalizada.
```

## 💡 Decisiones de Diseño
- `Semaphore(capacidad, true)` activa la política **justa (FIFO)** para evitar que hilos esperen indefinidamente.  
- Se usa `synchronized` en los logs y contador `ocupadas` para mantener trazas consistentes.  
- Bloque `try/finally` en `Coche.run()` asegura que siempre se libere la plaza aunque haya interrupciones.

## ▶️ Cómo Ejecutar
1. Abrir el proyecto en **IntelliJ IDEA** con JDK 17 o superior.  
2. Ejecutar la clase `PrincipalParking`.  
3. Observar en consola que nunca hay más de 3 coches dentro simultáneamente.

## 📈 Posibles Mejoras
- Registrar tiempos de espera y aparcamiento en un fichero CSV.  
- Permitir definir número de coches y plazas por argumentos del programa.  
- Añadir interfaz gráfica o panel de estado en tiempo real.

## 🧑‍💻 Autor
Proyecto de repaso Tema 07 – **Semáforos en Java (Programación de Servicios y Procesos)**  
Desarrollado con IntelliJ IDEA.
