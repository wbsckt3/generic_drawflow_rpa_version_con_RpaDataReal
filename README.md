Funcionalidades Principales

    Visualización de Nodos RPA: Representación gráfica de cada instalación RPA con su estado actual

    Panel de Configuración: Para establecer conexión con la API

    Sistema de Filtros: Para visualizar nodos por estado o tipo

    Panel de Detalles: Muestra información específica de cada RPA seleccionado

    Acciones de Control: Permite iniciar, detener y reiniciar RPAs

    Panel de Logs: Muestra eventos y actividades del sistema

    Conexión en Tiempo Real: Usa Socket.IO para actualizaciones en vivo

Estructura de Conexiones y Flujo de Datos

    Configuración Inicial:

        API Base: URL base del endpoint

        User Email: Email de autenticación

        Company ID: Identificador de la compañía

        Plan ID: Identificador del plan RPA

    Flujo de Datos:

        La aplicación carga la configuración guardada en localStorage

        Realiza una petición a la API para obtener datos del plan RPA

        Consulta el endpoint de monitoreo para obtener el estado actual

        Renderiza los nodos en el canvas según los datos recibidos

        Establece conexión Socket.IO para recibir actualizaciones en tiempo real

Puntos Clave para Integración con Nuevos Endpoints

    Modificar Configuración de API:

        Los endpoints se configuran en loadRpaPlan() y loadRpaData()

        La URL base se toma del campo apiEndpoint

        Los headers de autenticación usan el userEmail

    Estructura de Datos Esperada:

        El endpoint de plan debe devolver: maxSessions y planName

        El endpoint de monitoreo debe devolver un array rpas con objetos que contengan:

            id, name, type, status, machine, lastExecution, connections

    Eventos de Socket.IO:

        rpa_execution_started: Cuando un RPA inicia

        rpa_execution_ended: Cuando un RPA finaliza

        rpa_execution_progress: Para actualizar el progreso

Cómo Conectar una Nueva API

    Adaptar las Funciones de Carga:

        Modificar loadRpaPlan() y loadRpaData() para mapear la estructura de la nueva API

        Ajustar los parámetros de autenticación si son diferentes

    Actualizar el Formato de Datos:

        Asegurar que los datos devueltos sigan la estructura esperada por drawRpaNodes()

        Los nodos inactivos se crean automáticamente basados en maxSessions

    Configurar Eventos de Socket:

        Si la nueva API usa diferentes eventos, actualizar setupSocketListeners()

        Ajustar los manejadores de eventos para procesar la data correctamente

Elementos Visuales a Conservar

    Diseño oscuro con gradientes y tarjetas translúcidas

    Nodos con bordes redondeados y efectos visuales según estado

    Sistema de colores para estados (verde=ejecutando, rojo=error, gris=detenido)

    Barra de progreso para operaciones en curso

    Panel de logs con timestamp

Consideraciones Técnicas

    La aplicación usa Drawflow solo para visualización, no para crear flujos

    Los nodos son estáticos y representan instalaciones RPA físicas/virtuales

    El sistema está preparado para manejar errores de conexión mostrando datos de ejemplo
