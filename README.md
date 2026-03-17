## INTEGRANTES
-- Nelson Javier Mejia Lemus
-- Brayan Isaac Carranza Amaya

## Situación problematica

En algunas ocaciones dentro de la Universidad Gerardo Barrios, nosotros como estudiantes tenemos algunas dificultades al momento de solicitar asesorías academicas, cuando se solicita apoyo o refuerzo en materias complicadas, normalmente estas solicitudes se hacen por mensajes informales, grupos de chat o de forma verbal, lo que provoca desorganización, pérdida de información o poca claridad sobre quién solicitó la asesoría, en qué materia, para qué fecha y en qué modalidad desea recibirla. Esto afecta tanto a los estudiantes como a los docentes, ya que no hay un medio centralizado para registrar y visualizar las solicitudes.

### Sectores a los que va dirigida la solución
- Sector educativo
- Universidades

### Solución propuesta
Se creo una aplicación web llamada **Asesorías U**, esta permite registrar solicitudes de asesoría académica de forma ordenada. El sistema permite ingresar el nombre del estudiante, la materia, la modalidad, la fecha solicitada y una descripción del problema académico. Además, valida la información ingresada, muestra las solicitudes registradas, permite filtrarlas por materia y cambiar su estado entre pendiente y atendida.

## Preguntas 

### 1. Explique con sus propias palabras qué es Vue.js y cuál es su función dentro de la página web desarrollada.

Vue.js es un framework de JavaScript que sirve para crear interfaces web dinámicas e interactivas de una forma más ordenada y sencilla. En este proyecto su función fue permitir que los datos ingresados por el usuario se reflejaran automáticamente en la interfaz, controlar eventos del formulario, validar información y mostrar la lista de solicitudes sin recargar la página.

### 2. Describa qué variables reactivas utilizó en su aplicación y cuál es la función de cada una dentro del sistema.

Las variables reactivas utilizadas fueron:

- `titulo`: guarda el nombre principal del sistema.
- `subtitulo`: muestra una breve descripción de la aplicación.
- `nombre`: almacena el nombre del estudiante.
- `materia`: guarda la materia para la cual se solicita asesoría.
- `modalidad`: almacena si la asesoría será presencial, virtual o híbrida.
- `fecha`: guarda la fecha solicitada.
- `descripcion`: almacena el detalle del problema académico.
- `filtroMateria`: sirve para filtrar las solicitudes por nombre de materia.
- `errores`: almacena los mensajes de validación cuando un dato está incorrecto.
- `mensajeExito`: muestra un aviso cuando la solicitud se registra correctamente.
- `solicitudes`: guarda todas las solicitudes registradas en el sistema.

### 3. Explique la diferencia entre las directivas utilizadas en su proyecto: v-bind y v-model.

La directiva `v-bind` se utiliza para enlazar atributos HTML con datos de Vue de forma dinámica. Por ejemplo, se usó para desactivar el botón cuando faltan datos y para cambiar clases CSS según el estado.

La directiva `v-model` se utiliza para crear un enlace bidireccional entre el input y la variable reactiva. Es decir, cuando el usuario escribe algo, la variable se actualiza automáticamente, y si la variable cambia, también cambia el valor mostrado en el campo.

### 4. Mencione al menos un ejemplo de evento utilizado dentro de su aplicación.

Un evento utilizado fue `@submit.prevent="registrarSolicitud"`, que sirve para capturar el envío del formulario y registrar la solicitud sin recargar la página.

También se utilizó `@click="cambiarEstado(solicitud.id)"` para cambiar el estado de cada solicitud.

### 5. Explique para qué utilizó la directiva v-for dentro de su aplicación.

La directiva `v-for` se utilizó para recorrer y mostrar de forma dinámica la lista de solicitudes registradas. También se utilizó para mostrar los mensajes de error cuando una validación falla.

### 6. Describa en qué situación utilizó v-if y qué problema resuelve dentro de su interfaz.

La directiva `v-if` se utilizó para mostrar u ocultar elementos dependiendo de una condición. Por ejemplo, se usó para mostrar los errores de validación solo cuando existen, mostrar el mensaje de éxito cuando se registra una solicitud y mostrar un mensaje cuando no hay resultados en la lista filtrada. Esto mejora la interfaz porque evita mostrar información innecesaria.

### 7. Explique cómo se realiza la validación de datos en su aplicación y por qué es importante validar la información ingresada por el usuario.

La validación se realiza dentro del método `validarFormulario()`. En este método se revisa que los campos obligatorios no estén vacíos, que el nombre tenga un mínimo de caracteres, que la fecha no sea anterior al día actual y que la descripción tenga suficiente información.

Validar los datos es importante porque evita registros incompletos o incorrectos, mejora la calidad de la información y ayuda a que el sistema funcione de forma más confiable.


