Fecha: 24/09/2026
Entrega de P1: 27/09/2026
Estado: Propuesta 1 aprobada — Registro de pagos por Yape para el minimarket

———

## Propuesta 1 — Registro de pagos por Yape para el minimarket

### Usuario

Mi abuela Celia, quien administra un minimarket y recibe pagos por Yape de sus clientes.

### Problema

Cuando un cliente paga por Yape, mi abuela anota en un cuaderno su nombre, el monto y el día del pago. Después debe buscar la anotación y
compararla manualmente con los movimientos de Yape.

Este proceso tarda, puede causar confusiones y hace difícil encontrar pagos antiguos o comprobar cuánto recibió durante el día.

### Alcance mínimo de la v1

La primera versión permitirá:

- Registrar el nombre del cliente.
- Registrar el monto pagado.
- Registrar el día del pago.
- Marcar un pago como pendiente o verificado.
- Buscar pagos por nombre.
- Filtrar pagos por día.
- Mostrar el total recibido durante un día.

La primera versión no incluirá:

- Conexión directa con Yape.
- Acceso a cuentas bancarias.
- Lectura automática de capturas.
- Notificaciones.
- Cuentas para diferentes usuarios.
- Control completo de ventas o inventario.

### Cómo se ve el éxito

Celia puede registrar 20 pagos y encontrar cualquier pago por nombre o día en menos de 30 segundos. También puede ver el total recibido
durante una fecha sin hacer la suma manualmente.

### Tres cosas que no sé hacer todavía

1. Guardar los pagos para que no desaparezcan al cerrar el programa.
2. Crear búsquedas, filtros y totales sin producir resultados incorrectos.
3. Crear pruebas automáticas y configurar CI con GitHub Actions.

———

## Propuesta 2 — Organizador de tareas y horarios escolares

### Usuario

Ariana, estudiante, y posteriormente sus compañeros de clase que tienen dificultades para organizar tareas, clases y evaluaciones.

### Problema

Las tareas y evaluaciones se comunican en diferentes momentos y pueden quedar anotadas en cuadernos, mensajes o recordatorios separados.
Esto dificulta saber qué actividad debe realizarse primero y qué fecha límite está más cerca.

### Alcance mínimo de la v1

La primera versión permitirá:

- Registrar el nombre del curso.
- Registrar una tarea o evaluación.
- Guardar su fecha límite.
- Marcar la actividad como pendiente o completada.
- Mostrar las actividades ordenadas por fecha.
- Filtrar las actividades de hoy y de la semana.
- Señalar visualmente las actividades atrasadas.

La primera versión no incluirá:

- Inicio de sesión.
- Diferentes cuentas de estudiantes.
- Notificaciones por correo o celular.
- Integración con Google Calendar.
- Chats o funciones colaborativas.
- Generación de horarios mediante inteligencia artificial.

### Cómo se ve el éxito

Ariana puede registrar 15 actividades en menos de cinco minutos e identificar las tres fechas límite más próximas en menos de diez
segundos.

### Tres cosas que no sé hacer todavía

1. Ordenar y filtrar correctamente actividades utilizando fechas.
2. Guardar los datos para que permanezcan después de cerrar el programa.
3. Probar automáticamente los casos de tareas atrasadas, completadas y con fechas inválidas.

———

## Propuesta 3 — Control básico de inventario para el minimarket

### Usuario

Mi abuela Celia, quien administra un minimarket y necesita saber qué productos están por agotarse.

### Problema

En un minimarket es difícil recordar la cantidad disponible de cada producto. Si el control se hace de memoria o en papel, algunos
productos pueden agotarse sin que se detecte a tiempo.

### Alcance mínimo de la v1

La primera versión permitirá:

- Registrar el nombre de un producto.
- Registrar su cantidad disponible.
- Definir una cantidad mínima.
- Registrar entradas de productos.
- Registrar salidas de productos.
- Mostrar una lista de productos con poco stock.
- Buscar un producto por nombre.

La primera versión no incluirá:

- Lectura de códigos de barras.
- Facturación.
- Pagos.
- Contabilidad.
- Predicción de ventas.
- Conexión con proveedores.
- Diferentes sucursales o usuarios.

### Cómo se ve el éxito

Celia puede registrar 30 productos en menos de diez minutos y obtener inmediatamente una lista correcta de los productos cuya cantidad
está por debajo del mínimo establecido.

### Tres cosas que no sé hacer todavía

1. Modelar correctamente las entradas y salidas del inventario.
2. Evitar cantidades inválidas o stock negativo.
3. Crear pruebas automáticas para comprobar cuándo un producto debe aparecer en la lista de poco stock.

  ———

## Comparación de las propuestas

  Propuesta                     Usuaria principal    Dificultad    Posibilidad de terminarla para P1
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Registro de pagos por Yape    Celia                      Baja    Alta
────────────────────────────  ───────────────────  ────────────  ───────────────────────────────────
 Organizador escolar           Ariana                     Baja    Alta
────────────────────────────  ───────────────────  ────────────  ───────────────────────────────────
 Control de inventario         Celia                     Media    Media

## Propuesta recomendada

La propuesta recomendada para P1 es Registro de pagos por Yape para el minimarket.

Tiene una usuaria concreta, resuelve un problema real y su alcance es suficientemente pequeño para terminarlo antes del 27 de septiembre.

## Requisitos técnicos comunes

La propuesta elegida deberá incluir:

- Repositorio público.
- README con problema, alcance, exclusiones y decisiones.
- Al menos tres pruebas reales.
- CI en verde mediante GitHub Actions.
- Ramas y Pull Request.
- Instrucciones para ejecutarla con un máximo de tres comandos.
- Defensa de 20 minutos sin IA.

La propuesta más segura para entregar a tiempo es la número 1. No combines pagos e inventario en P1: serían dos proyectos y aumentarían
demasiado el alcance.