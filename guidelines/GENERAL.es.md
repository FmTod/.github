# DIRECTRICES ESTRICTAS

Por favor, lee estas directrices detenidamente. Estas directrices son innegociables y deben ser cumplidas sin excepción.

## Comunicación (Slack)

- Enviar informes diarios de progreso puntualmente al comienzo y al final de cada día.
- La notificación inmediata de cualquier obstáculo o desafío es obligatoria.
  - Nuestro equipo está disponible para ayudar, asegurando una resolución rápida (Trabajamos en equipo).
- Comunicar de manera proactiva cualquier retraso en los plazos de hitos.
  - No se tolerará la falta de comunicación al respecto.

## Gestión de tareas (Asana)

- Todos los proyectos deben ser meticulosamente desglosados en tareas/subtareas más pequeñas.
  - Especificar los tiempos estimados de finalización para cada tarea.
- Asegurarse de que las tareas incluyan tiempo adecuado para investigación, implementación, pruebas, documentación, etc.

## GitHub

- Cada corrección de error o característica requiere su propio PR.
- Basar todos los PR en la rama master/main por defecto.
- El código debe ser subido a GitHub al final de cada día, independientemente de su completitud.
- Nuevamente, el código debe ser subido a GitHub al final de cada día, independientemente de su completitud.
- Todo el código comentado o no utilizado debe ser eliminado antes de enviar un PR, con justificación si es necesario.

## Codificación

- Seguir un estilo de codificación consistente en todo el proyecto para uniformidad.
- Priorizar la eficiencia y optimización del código para mejorar el rendimiento.
- Enfatizar la legibilidad y mantenibilidad del código a través de comentarios claros y descriptivos.

## Validación

- La mayoría de las entradas de usuario deben ser validadas.
- La validación debe realizarse en el backend y reflejarse en el frontend utilizando [Laravel Precognition](https://laravel.com/docs/11.x/precognition).
- Las reglas de validación personalizadas deben seguir la estructura descrita en la [documentación de Laravel](https://laravel.com/docs/validation#custom-validation-rules).


## Pruebas

- Un nuevo test debe acompañar a cada característica.
- Asegurar el 100% de cobertura de la funcionalidad de la clase. (https://github.com/FmTod2/pestphp-docker)
- Crear pruebas faltantes para clases existentes al trabajar en correcciones de errores/cambios.
- Implementar acciones de GitHub para ejecutar pruebas en entornos Windows y Linux.

## Documentación
- Proveer documentación completa para cada nueva implementación o adición de código.
- Asegurarse de que toda la documentación esté escrita en formato Markdown.
- Incluir un diagrama que ilustre el flujo general de la funcionalidad añadida, abarcando tanto los aspectos del backend como del frontend.

## Convenciones de nomenclatura

- Apegarse estrictamente a las convenciones de nomenclatura existentes en proyectos en curso.
- Seleccionar y aplicar consistentemente una convención de nomenclatura para nuevos proyectos.

## Laravel ([Leer Más](./PHP.md))

- Priorizar las metodologías de Laravel sobre las convenciones de PHP puro para consistencia y eficiencia.
- Evitar duplicar funcionalidades que estén fácilmente disponibles dentro del framework.
