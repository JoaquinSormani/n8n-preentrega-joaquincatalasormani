# Pre-entrega: Monitor de Precio de Criptomonedas

## Descripción del Caso
Este workflow automatiza la verificación del precio de Bitcoin. Permite al usuario definir un "precio objetivo" mediante una llamada externa y recibir una notificación solo si el valor de mercado actual supera dicho umbral.

## Estructura del Workflow
El flujo sigue la estructura: **Webhook → API → IF → Email**.

### Disparador (Trigger)
- **Tipo:** Webhook (POST).
- **Función:** Recibe un JSON desde Postman con el parámetro `precio_objetivo`.

### Nodos
1. **HTTP Request:** Consulta la API pública de CoinDesk (`api.coindesk.com`) para obtener la cotización actual del BTC en USD. No requiere autenticación.
2. **IF (Condicional):** Compara el valor `rate_float` (API) vs `precio_objetivo` (Webhook).
   - *Condición:* Si `Precio Actual` > `Precio Objetivo` → Pasa a True.
3. **Gmail:** Envía una alerta al correo configurado notificando el valor actual.

### Buenas Prácticas
- **Seguridad:** Las credenciales de Gmail están gestionadas internamente en n8n y no se exponen en el código.
- **Eficiencia:** Se utilizan APIs sin autenticación para reducir la complejidad en la fase de prototipo.
- **Datos:** Se normalizan los valores numéricos para asegurar una comparación correcta en el nodo IF.
