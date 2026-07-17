
# README: Flujo de Automatización - TutorBot Académico (Examen) evelyn


## 4. Flujo de Coordinación (Nuevo)

Esta es la funcionalidad solicitada en el examen, diseñada para ofrecer una vista rápida del estado de las tutorías.

*   **Punto de Entrada (`Telegram Trigger`):** Un nuevo disparador escucha los comandos del coordinador.
*   **Procesamiento:**
    1.  **Leer Datos (`Google Sheets`):** El nodo lee todos los registros de la hoja `matricula`.
    2.  **Filtrar por Semana (No implementado en el JSON, pero es el siguiente paso lógico):** Se debería añadir un nodo de código para filtrar solo los registros de la semana actual.
    3.  **Agrupar y Contar (`Resumen por Materia`):** Un nodo de código itera sobre los registros, los agrupa por el nombre de la materia y cuenta cuántas solicitudes hay para cada una.
    4.  **Formatear Salida:** El mismo nodo construye un mensaje de texto con un formato profesional, mostrando el conteo por materia y el total de la semana.
*   **Salida (`Telegram`):** El mensaje formateado se envía al chat del coordinador.

Este flujo demuestra una arquitectura robusta y escalable, separando las responsabilidades por roles y automatizando procesos clave para mejorar la eficiencia de la gestión académica.


SE HICIERON DOS PRUEBAS

SE USO EL SIGUIENTE GOOGLE SHEETS A LA PRIMERA 
https://docs.google.com/spreadsheets/d/1JPDkVmouJN6cY2HncSp6WqG0-ePqXMkOW1HdidmXJA8/edit?usp=sharing


SE USO EL SIGUIENTE ENLACE PARA LA PRINCIPAL

https://docs.google.com/spreadsheets/d/1O6cW5A7rbP6rQoUwLzqxJ07OiWXifCDN6a4Gg6PIFwo/edit?pli=1&gid=1016863471#gid=1016863471