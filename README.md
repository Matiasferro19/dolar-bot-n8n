# Bot de actualización del precio del dólar 💵

Este workflow de **n8n** obtiene el precio del dólar desde una API pública y envía automáticamente un mensaje a un canal de Discord con la cotización actualizada.

## Tecnologías
- n8n
- API REST
- Discord Bot

## Nodos del Workflow

1. **Trigger de hora (Cron Trigger) ⏰**
   - Dispara el workflow cada día a las 14:17 (2:17pm).  
   - Configuración: método GET, URL de la API de dólar pública.  

2. **Crear nuevas variables (Set Node) 📝**
   - Procesa la respuesta de la API y crea variables:  
     - `rates.USD` → precio del dólar en USD  
     - `rates.ARS` → precio del dólar en ARS  
     - `date` → fecha de actualización  

3. **Formato de fecha (Function / Date Node) 📅**
   - Modifica el formato de la fecha obtenida de la API.  
   - Formato de salida: `MMMM DD YYYY`  
   - Campo de salida: `formattedDate`  

4. **Mensaje del bot (Discord Node) 🤖**
   - Envía el mensaje al canal de Discord `precio-dolar😭`.  
   - Contenido del mensaje:  
     ```
     Un dólar vale {{ $('Crear nuevas variables').item.json.rates.ARS }} $ ARS.
     ```
   - Usa las credenciales de tu **Discord Bot** para conectarse al servidor y canal.  

---

## Cómo usarlo
1. Importar `bot-dolar.json` en tu instancia de n8n.  
2. Configurar tus credenciales de Discord Bot.  
3. Ejecutar el workflow.  

## Screenshots
![Workflow en n8n](screenshots/Workflow.png)

---

