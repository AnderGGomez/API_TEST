# Instrucciones Copilot para Agente de Pruebas de API

## ⚠️ OBLIGACIONES CRÍTICAS (LEER PRIMERO)

### ❌ PROHIBIDO: NUNCA escribir resultados en el chat
### ✅ OBLIGATORIO: SIEMPRE crear archivos físicos usando create_file

### ARCHIVOS OBLIGATORIOS A GENERAR (USAR create_file):
1. **api_test_report.md** - Informe principal con formato EXACTO del ejemplo (ARCHIVO FÍSICO EN RAÍZ)
2. **api_test_requests.md** - Todos los comandos cURL ejecutados (ARCHIVO FÍSICO EN RAÍZ)

### ⚠️ REGLA CRÍTICA DE SALIDA:
- **NUNCA** mostrar el contenido del informe en el chat
- **SIEMPRE** usar la herramienta `create_file` para generar ambos archivos en `c:\Users\USUARIO\Documents\DemoMCP\`
- **OBLIGATORIO** verificar con `list_dir` que los archivos fueron creados exitosamente
- **SOLO** después de crear los archivos, confirmar al usuario que fueron generados

### CADA CASO DE PRUEBA DEBE INCLUIR:
- ✅ Descripción detallada
- ✅ Resultado con emoji (🟢 ÉXITO / 🔴 FALLO / 🟡 ADVERTENCIA)
- ✅ Petición enviada COMPLETA (método, URL, headers, body)
- ✅ **Comando cURL funcional e importable en Postman**
- ✅ Respuesta recibida COMPLETA (código de estado, headers, body)
- ✅ Separador `---` entre secciones

### PROCESO SECUENCIAL OBLIGATORIO:
1. Leer `api_test.prompt.md` y seguir sus 6 fases
2. Analizar `resource/precredit.json`
3. Planificar 5 casos generales por endpoint
4. Ejecutar todas las pruebas
5. **USAR create_file** para generar `api_test_report.md` con formato exacto (ARCHIVO FÍSICO)
6. **USAR create_file** para generar `api_test_requests.md` con todos los cURL (ARCHIVO FÍSICO)
7. **USAR list_dir** para verificar que ambos archivos existen en el directorio raíz
8. Confirmar al usuario que los archivos fueron creados exitosamente

---

## Contexto del Proyecto
Este workspace contiene un agente especializado en pruebas de calidad de APIs REST. El agente está diseñado para analizar documentación de APIs (OpenAPI/Swagger), ejecutar casos de prueba exhaustivos y generar informes técnicos detallados siguiendo estrictamente el formato definido en `api_test.prompt.md`.

## Estructura del Workspace
```
DemoMCP/
├── .github/
│   ├── prompts/
│   │   └── api_test.prompt.md     # Prompt principal del agente (OBLIGATORIO SEGUIR)
│   └── copilot-instructions.md    # Este archivo
├── resource/
│   └── precredit.json            # Documentación OpenAPI de la API a probar
├── api_test_report.md            # ⚠️ OBLIGATORIO: Informe principal de pruebas
└── api_test_requests.md          # ⚠️ OBLIGATORIO: Archivo con comandos cURL
```

## Herramientas Requeridas
- **rest-api**: Herramienta MCP para realizar peticiones HTTP a APIs REST
- **mcp_rest-api_test_request**: Función específica para testing de endpoints
- **create_file**: Para generar los archivos de reporte obligatorios

## Flujo de Trabajo del Agente (OBLIGATORIO SEGUIR EN ORDEN)

### ⚠️ REGLA CRÍTICA: Seguir estrictamente el prompt api_test.prompt.md
El agente DEBE ejecutar las 6 fases secuenciales definidas en `api_test.prompt.md` sin omitir ningún paso:

### 1. Activación del Agente
Para ejecutar el agente de pruebas de API, el usuario DEBE proporcionar:
- **Credenciales de autenticación** (Bearer token, API key, etc.) - OBLIGATORIO
- **Casos de prueba específicos** (opcional, además de los casos generales)

### 2. Proceso de Ejecución Secuencial (OBLIGATORIO)

#### FASE 1: Análisis de Entradas
- ✅ Leer y procesar `resource/precredit.json` (documento OpenAPI)
- ✅ Identificar TODOS los endpoints y métodos HTTP
- ✅ Extraer esquemas de request/response de cada endpoint
- ✅ Procesar credenciales de autenticación proporcionadas
- ✅ Asimilar casos de prueba específicos del usuario

#### FASE 2: Planificación de Pruebas
Para CADA endpoint identificado, planificar estos 5 casos de prueba generales:
- a) ✅ Validar que el servicio está creado (responde correctamente)
- b) ✅ Validar método HTTP correcto y rechazar incorrectos
- c) ✅ Validar petición con información faltante en body o parámetros
- d) ✅ Validar petición con tipos de datos inválidos
- e) ✅ Validar petición completa y válida según documentación

Además, integrar los **casos de prueba específicos** del usuario.

#### FASE 3: Ejecución de Pruebas
- ✅ Ejecutar SECUENCIALMENTE cada caso de prueba planificado
- ✅ Incluir credenciales de autenticación en headers de TODAS las peticiones
- ✅ Registrar petición completa (método, URL, headers, body)
- ✅ Registrar respuesta completa (código de estado, headers, body)
- ✅ Generar comando cURL funcional para cada petición ejecutada

#### FASE 4: Generación del Informe Principal (api_test_report.md)
⚠️ **OBLIGATORIO**: **USAR create_file** para crear archivo físico `api_test_report.md` en `c:\Users\USUARIO\Documents\DemoMCP\api_test_report.md` con:
- ✅ Título principal: "# Informe de Pruebas API Precrédito"
- ✅ Una sección por cada caso de prueba ejecutado
- ✅ Cada sección separada por `---`
- ✅ Estructura EXACTA del ejemplo en api_test.prompt.md:
  * Caso de Prueba: [ID] - [ENDPOINT] - [DESCRIPCIÓN]
  * Descripción detallada
  * Resultado: 🟢 ÉXITO / 🔴 FALLO / 🟡 ADVERTENCIA
  * Petición Enviada (método, URL, headers, body)
  * **Comando cURL funcional (OBLIGATORIO)**
  * Respuesta Recibida (código de estado, body)
- ❌ **NUNCA** mostrar este contenido en el chat
- ✅ **SIEMPRE** crear el archivo físico usando `create_file`

#### FASE 5: Generación del Archivo de Comandos cURL (api_test_requests.md)
⚠️ **OBLIGATORIO**: **USAR create_file** para crear archivo físico `api_test_requests.md` en `c:\Users\USUARIO\Documents\DemoMCP\api_test_requests.md` con:
- ✅ TODOS los comandos cURL ejecutados durante las pruebas
- ✅ Comandos agrupados por endpoint
- ✅ Cada comando debe ser funcional y listo para ejecutarse
- ✅ Formato compatible para importar en Postman
- ✅ Incluir todos los headers necesarios (Content-Type, Accept, Authorization)
- ✅ Para POST/PUT: incluir `--data` con el body completo
- ✅ Para GET: incluir solo headers relevantes
- ❌ **NUNCA** mostrar este contenido en el chat
- ✅ **SIEMPRE** crear el archivo físico usando `create_file`

#### FASE 6: Verificación Final
- ✅ **USAR list_dir** en `c:\Users\USUARIO\Documents\DemoMCP\` para verificar que `api_test_report.md` existe
- ✅ **USAR list_dir** en `c:\Users\USUARIO\Documents\DemoMCP\` para verificar que `api_test_requests.md` existe
- ✅ Verificar que se probaron TODOS los endpoints
- ✅ Verificar que cada caso tiene su comando cURL
- ✅ Confirmar que el formato coincide con el ejemplo del prompt
- ✅ **Confirmar al usuario**: "✅ Archivos generados exitosamente en c:\Users\USUARIO\Documents\DemoMCP\"

## Formato de Entrada Esperado

### Credenciales de Autenticación
```
Credenciales: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Casos de Prueba Específicos (Opcional)
```
Casos específicos:
1. Probar endpoint /login con credenciales inválidas
2. Validar rate limiting en endpoint /evaluate
3. Verificar paginación en endpoint /customers
```

## Comandos de Activación

### ⚠️ Comando CORRECTO para ejecutar el agente:
```
Ejecuta las pruebas de API según el prompt api_test.prompt.md usando estas credenciales: [CREDENCIALES]
```

O con casos específicos:
```
Ejecuta las pruebas de API según api_test.prompt.md con:
- Credenciales: [CREDENCIALES]
- Casos específicos: [LISTA_DE_CASOS]
```

### Para solo analizar documentación (sin ejecutar pruebas):
```
Analiza la documentación en resource/precredit.json y lista todos los endpoints
```

## Restricciones y Consideraciones

### ⚠️ OBLIGACIONES CRÍTICAS DEL AGENTE
1. **SIEMPRE usar create_file para generar DOS archivos físicos obligatorios:**
   - `c:\Users\USUARIO\Documents\DemoMCP\api_test_report.md` - Informe principal con todos los detalles
   - `c:\Users\USUARIO\Documents\DemoMCP\api_test_requests.md` - Todos los comandos cURL ejecutados
   - ❌ **PROHIBIDO** mostrar el contenido en el chat
   - ✅ **OBLIGATORIO** crear archivos físicos con `create_file`

2. **Cada caso de prueba en el informe DEBE incluir:**
   - Descripción completa del caso
   - Resultado con emoji (🟢 ÉXITO / 🔴 FALLO / 🟡 ADVERTENCIA)
   - Petición completa (método, URL, headers, body)
   - **Comando cURL funcional e importable en Postman**
   - Respuesta completa (código de estado, headers, body)

3. **Formato del comando cURL (OBLIGATORIO):**
   - Para POST/PUT:
     ```bash
     curl --location 'https://qa.back.pre-credit.com/api/endpoint' \
     --header 'Content-Type: application/json' \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer {{bearerToken}}' \
     --data '{
       "field": "value"
     }'
     ```
   - Para GET:
     ```bash
     curl --location 'https://qa.back.pre-credit.com/api/endpoint' \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer {{bearerToken}}'
     ```

### Restricciones de Seguridad
- NO ejecutar pruebas destructivas (DELETE) sin autorización explícita
- NO modificar datos del servidor
- Usar solo credenciales proporcionadas por el usuario
- Todas las peticiones DEBEN incluir headers de autenticación

### Consideraciones Técnicas
- El informe principal debe seguir EXACTAMENTE el formato del ejemplo en api_test.prompt.md
- Cada sección debe estar separada por `---`
- Los comandos cURL deben ser funcionales y compatibles con Postman
- Usar emojis para indicar estado: 🟢 ÉXITO, 🔴 FALLO, 🟡 ADVERTENCIA
- Registrar peticiones y respuestas COMPLETAS (no resumir)

## Estructura del Informe de Salida

### ⚠️ ARCHIVO 1: api_test_report.md (OBLIGATORIO)
```markdown
# Informe de Pruebas API Precrédito

## Caso de Prueba: 1.1 - [POST /evaluate] - Ejecución con información inválida
* **Descripción:** Se prueba la respuesta del endpoint al recibir un tipo de dato incorrecto en el campo 'customerId'. Se espera un error 400 (Bad Request).
* **Resultado:** 🟢 ÉXITO

---
### Petición Enviada (Request)
* **Método:** `POST`
* **URL:** `https://api.example.com/v1/evaluate`
* **Headers:**
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer [TOKEN_UTILIZADO]"
    }
    ```
* **Body:**
    ```json
    {
      "customerId": "esto-no-es-un-numero",
      "loanAmount": 5000
    }
    ```

### cURL Command
```bash
curl --location 'https://api.example.com/v1/evaluate' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer [TOKEN_UTILIZADO]' \
--data '{
  "customerId": "esto-no-es-un-numero",
  "loanAmount": 5000
}'
```

---
### Respuesta Recibida (Response)
* **Código de Estado:** `400 Bad Request`
* **Body:**
    ```json
    {
      "error": "Invalid data type",
      "message": "Field 'customerId' must be an integer."
    }
    ```
```

### ⚠️ ARCHIVO 2: api_test_requests.md (OBLIGATORIO)
```markdown
# Comandos cURL - Pruebas API Precrédito

## Endpoint: POST /evaluate

### Caso 1: Petición con tipo de dato inválido
```bash
curl --location 'https://api.example.com/v1/evaluate' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{bearerToken}}' \
--data '{
  "customerId": "esto-no-es-un-numero",
  "loanAmount": 5000
}'
```

### Caso 2: Petición válida completa
```bash
curl --location 'https://api.example.com/v1/evaluate' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{bearerToken}}' \
--data '{
  "customerId": 12345,
  "loanAmount": 5000
}'
```

## Endpoint: GET /health

### Caso 1: Health check básico
```bash
curl --location 'https://api.example.com/v1/health' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {{bearerToken}}'
```
```

## Variables de Configuración
- **API_BASE_URL**: Extraída de precredit.json
- **AUTH_TYPE**: Bearer, API Key, Basic Auth, etc.
- **TIMEOUT**: 30 segundos por defecto
- **MAX_RETRIES**: 3 intentos por defecto

## Manejo de Errores
- **Network errors**: Reportar como fallo con detalles del error
- **Authentication errors**: Verificar credenciales y reportar
- **Timeout errors**: Reintentar hasta MAX_RETRIES
- **Invalid responses**: Registrar respuesta completa para análisis

## Archivos de Salida (OBLIGATORIOS)

### ⚠️ 1. api_test_report.md
- **Ubicación**: Raíz del proyecto
- **Contenido**: Informe completo con todos los casos de prueba ejecutados
- **Formato**: Seguir EXACTAMENTE el ejemplo del prompt api_test.prompt.md
- **Secciones obligatorias por cada caso**:
  * Título del caso con ID, endpoint y descripción
  * Descripción detallada
  * Resultado (🟢 ÉXITO / 🔴 FALLO / 🟡 ADVERTENCIA)
  * Petición enviada completa
  * **Comando cURL funcional**
  * Respuesta recibida completa

### ⚠️ 2. api_test_requests.md
- **Ubicación**: Raíz del proyecto
- **Contenido**: Todos los comandos cURL ejecutados, agrupados por endpoint
- **Formato**: Comandos funcionales e importables en Postman
- **Debe incluir**:
  * Todos los headers necesarios
  * Body completo para POST/PUT con flag `--data`
  * Organización clara por endpoint y caso de prueba

## Comandos Útiles para el Usuario

### Preparación del entorno:
```powershell
# Verificar estructura del workspace
Get-ChildItem -Path .\resource\
Get-ChildItem -Path .\.github\prompts\

# Leer el prompt del agente
Get-Content .\.github\prompts\api_test.prompt.md

# Leer la documentación de la API
Get-Content .\resource\precredit.json
```

### Para revisar reportes generados:
```powershell
# Ver el informe principal de pruebas
Get-Content .\api_test_report.md

# Ver los comandos cURL generados
Get-Content .\api_test_requests.md
```

### Para probar comandos cURL manualmente:
```powershell
# Los comandos cURL de api_test_requests.md se pueden ejecutar directamente
# Reemplazar {{bearerToken}} con el token real antes de ejecutar
```

## Notas Importantes
- El agente debe completar TODAS las 6 fases antes de generar los archivos finales
- **OBLIGATORIO**: Crear ambos archivos (api_test_report.md y api_test_requests.md)
- Cada caso de prueba debe tener su propia sección en el informe
- **OBLIGATORIO**: Incluir comando cURL funcional en cada caso de prueba
- Los casos específicos se integran con los casos generales
- El formato de salida debe seguir exactamente el ejemplo proporcionado en api_test.prompt.md
- Los comandos cURL deben ser compatibles con Postman para facilitar su importación
- Nunca omitir la generación del archivo api_test_requests.md
- Los comandos cURL deben usar `{{bearerToken}}` como placeholder para tokens