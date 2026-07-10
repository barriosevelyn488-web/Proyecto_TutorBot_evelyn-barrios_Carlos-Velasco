
# README: Flujo de Automatización - TutorBot Académico

**Descripción:** Este documento detalla el funcionamiento del flujo de n8n diseñado para gestionar el registro, las consultas y la matriculación de estudiantes en servicios de asesoría académica mediante Telegram.

## 1. Introducción
Este sistema automatiza la interacción con estudiantes universitarios mediante un bot de Telegram. El flujo se divide en dos grandes pilares de entrada: **Webhooks** para formularios externos y **Telegram Triggers** para interacciones directas en el chat. Todo el sistema está sincronizado con una hoja de cálculo de Google (Google Sheets) que actúa como base de datos central.

## 2. Componentes Principales

### A. Webhook (`/webhook`)
*   **Función:** Recibe los datos enviados desde un formulario web externo (`https://barriosevelyn488-web.github.io/Proyecto_TutorBot_evelyn-barrios_Carlos-Velasco/`).
*   **Proceso:** Al recibir una solicitud POST, el nodo `Obtener ultimo ID` consulta la hoja "Estudiantes" para generar automáticamente un nuevo código de estudiante (ej. `E001`) siguiendo una secuencia. Luego, `validacion de datos.` filtra si es una operación de `registro` o `matricula` y maneja errores (ej. email duplicado o código inexistente).

### B. Telegram Trigger
*   **Función:** Escucha todos los mensajes y `callback_querys` enviados por los usuarios en Telegram.
*   **Proceso:** El nodo `diferenciar por etiquetas` analiza el contenido del mensaje o el `callback_data` (la parte después del símbolo `#`).
    *   Si el mensaje es un código de formato `E000`, se interpreta como una acción de `matricularse`.
    *   Si es un botón, extrae el tipo de acción (`menu`, `lista`, `materia`, etc.) para dirigir el flujo hacia el nodo `Switch` correspondiente.

## 3. Integración y Lógica de Flujo

El sistema se complementa mediante una arquitectura dirigida por eventos:

1.  **Triggers como Punto de Entrada:**
    *   **Webhook Trigger:** Maneja el registro formal de datos desde la interfaz HTML.
    *   **Telegram Trigger:** Maneja la navegación del usuario (Menú principal, consulta de horarios, selección de materias).

2.  **Google Sheets como Núcleo:**
    *   Todas las acciones (registrar, consultar, matricular) realizan lecturas y escrituras en hojas específicas (`Estudiantes`, `Materias`, `Horarios`, `matricula`).
    *   Los nodos `Code` actúan como la capa de lógica, formateando los datos leídos de las hojas para presentarlos como mensajes claros en Markdown en Telegram.

3.  **Comunicación con el Usuario (HTTP Requests):**
    *   Todos los nodos de `HTTP Request` se comunican con la API de Telegram para enviar las respuestas al `chat_id` del usuario, utilizando `inline_keyboard` para crear una experiencia de usuario interactiva y navegable.

## 4. Complemento con el HTML
El formulario HTML (`Proyecto_TutorBot`) es indispensable para el flujo de `registro`:
*   El usuario solicita registrarse vía Telegram.
*   El bot responde con un enlace único que incluye su `chatId` como parámetro GET.
*   El HTML captura los datos personales y los envía al Webhook de n8n.
*   n8n procesa estos datos y notifica al usuario en Telegram sobre el éxito del registro.

**Elaborado por:** 
- Carlos Elias Tzoy Velasco
- Evelyn Noemi Barrios