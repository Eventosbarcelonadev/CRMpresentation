# Propuesta de Automatizacion y Sistema de Gestion Comercial
## Eventos Barcelona
### Marzo 2026

---

## 1. Resumen Ejecutivo

Eventos Barcelona lleva 15 anos organizando espectaculos y produccion tecnica para eventos corporativos en Barcelona. A dia de hoy, el 80-90% del tiempo del fundador se dedica a adaptar propuestas comerciales (PowerPoints) manualmente para cada lead, y toda la gestion comercial vive en el correo electronico.

**Proponemos un sistema automatizado end-to-end** que:
- Centralice todos los leads en un CRM
- Clasifique automaticamente cada solicitud por tipo de evento y espectaculo
- Genere y envie propuestas comerciales personalizadas de forma automatica
- Conecte el proceso comercial con la facturacion
- Libere al fundador del trabajo operativo repetitivo

**Resultado**: El fundador pasa de dedicar el 80-90% de su tiempo a tareas manuales a supervisar un sistema que funciona solo, donde unicamente necesita ajustar el margen o modificar 1-2 detalles antes de enviar.

---

## 2. Diagnostico de la Situacion Actual

| Area | Situacion actual | Problema |
|------|-----------------|----------|
| Entrada de leads | Email, formulario web, oficina virtual | Todo llega mezclado al correo |
| Clasificacion | Manual por el fundador | No delegable, depende de su experiencia |
| Propuestas comerciales | PowerPoints adaptados a mano | 80-90% del tiempo del fundador |
| Seguimiento | Desde el correo | Sin pipeline, sin visibilidad |
| Base de artistas | Contactos dispersos | Sin BD estructurada tras 15 anos |
| Email marketing | Mailchimp abandonado | Sin segmentacion ni automatizacion |
| Facturacion | Holded (no conectado) | Traspaso manual de datos |
| Delegacion | Imposible | Proceso no documentado ni sistematizado |

---

## 3. Solucion Propuesta: Stack Tecnologico

### Via 1: Lead envia email (flujo actual mejorado)

```
Lead envia email a info@eventosbarcelona.com
     |
     v
GHL captura el email automaticamente (forwarding SMTP)
     |
     v
Workflow GHL detecta lead nuevo
     |
     v
GHL envia respuesta automatica al lead:
"Gracias por contactarnos. Para prepararte una propuesta
 personalizada, rellena este breve formulario: [link]"
     |
     v
Lead rellena el formulario inteligente
(tipo evento, fecha, asistentes, shows de interes)
     |
     v
GHL clasifica automaticamente + genera propuesta web (custom code)
     |
     v
⚠️ HUMAN IN THE LOOP: Xavi recibe notificacion con resumen + link
     |
     v
Xavi revisa la propuesta en GHL:
  → Si esta bien: aprueba con un clic → se envia al cliente
  → Si quiere cambiar algo: edita desde GHL y luego aprueba
     |
     v
Cliente recibe propuesta web personalizada por email
     |
     v
Seguimiento automatico (48h, 5 dias, 10 dias)
     |
     v
Cliente acepta → Workflow GHL crea factura en Holded (custom code)
```

### Via 2: Lead entra por la web (formulario inteligente directo)

```
Lead visita eventosbarcelona.com
     |
     v
Hace clic en "Solicita un presupuesto"
     |
     v
Rellena el formulario inteligente embebido en la web
(tipo evento, fecha, asistentes, shows con fotos y videos)
     |
     v
Lead entra al CRM ya clasificado automaticamente
     |
     v
GHL genera propuesta web automaticamente (custom code)
     |
     v
⚠️ HUMAN IN THE LOOP: Xavi recibe notificacion con resumen + link
     |
     v
Xavi revisa la propuesta en GHL:
  → Si esta bien: aprueba con un clic → se envia al cliente
  → Si quiere cambiar algo: edita desde GHL y luego aprueba
     |
     v
Cliente recibe propuesta web personalizada por email
     |
     v
Seguimiento automatico (48h, 5 dias, 10 dias)
     |
     v
Cliente acepta → Workflow GHL crea factura en Holded (custom code)
```

**Nota:** Ambas vias convergen en el mismo pipeline del CRM. No importa como entre el lead, el proceso a partir de la clasificacion es identico. **Ninguna propuesta se envia sin la aprobacion de Xavi.**

### Herramientas

| Herramienta | Funcion | Reemplaza |
|-------------|---------|-----------|
| **GoHighLevel (Starter)** | CRM, pipeline, formularios, workflows, email marketing, custom code | Mailchimp + gestion manual por email + Make.com |
| **Mailgun (Foundation)** | Envio de emails (SMTP) con alta deliverability | SMTP de Mailchimp |
| **Holded (existente)** | Facturacion y contabilidad | Ya en uso |

**Nota:** Usamos **GHL custom code** (JavaScript dentro de los workflows) para las integraciones con Holded y la generacion de propuestas web. Esto elimina la necesidad de Make.com y Google Slides, reduciendo costes y dependencias externas. Las propuestas se generan como **paginas web personalizadas** (no PDFs) directamente desde los datos del CRM.

---

## 4. Catalogo de Shows Identificado

Para la clasificacion automatica de leads y la generacion de propuestas, hemos mapeado el catalogo completo:

### Categorias principales

| Categoria | Shows incluidos |
|-----------|----------------|
| **Shows Visuales y Mapping** | Holovortex (Hologramas), Flamenco Mapping, Barcelona Video Mapping, 3D Dreams (Dance + Mapping), Light Boxes Show |
| **Percusion y Musical** | Water Drummers, LED Percussionists, Laser Harp Show, Laser Violin Show |
| **Danza** | Salsa, Glamm Dancers, Brazilian Show, Flamenco, Bollywood, Hip-hop & Breakdance, Ballet, Cabaret & Burlesque, Pole Dance, Funky Fever, EB Street Dancers, Pulsar Dancers, Shadows of the Future, Silk Road Burlesque, Olympian Odyssey |
| **Danza Aerea** | Aerial Dance, LED Hula Hoop |
| **Luz y Laser** | Laser Shows, Light Art Show, Light Painting Artist |
| **Espectaculos Alternativos** | Sand Artist, Fire Painting |
| **Acrobacias y Malabares** | LED Juggling Show, Natacion Sincronizada |
| **Produccion Tecnica** | Iluminacion, Sonido, Pantallas LED, Escenarios |

### Tipos de evento

- Cenas de gala y entregas de premios
- Lanzamientos de producto
- Convenciones y congresos
- Galas institucionales
- Family Days corporativos
- Inauguraciones
- Eventos deportivos
- Fiestas tematicas (casino, etc.)

---

## 5. Detalle de la Implementacion

### FASE 1: CRM y Pipeline (Semanas 1-2)

**Configuracion de GoHighLevel:**

- **Custom Fields del contacto:**
  - Tipo de evento (gala, lanzamiento, convencion, family day, inauguracion, etc.)
  - Tipo de espectaculo preferido (categorias del catalogo)
  - Fecha del evento
  - Numero de asistentes
  - Presupuesto aproximado
  - Ubicacion
  - Origen del lead (web, email directo, telefono)

- **Pipeline de ventas con etapas:**
  1. New Lead (entrada automatica desde formulario inteligente)
  2. Propuesta Enviada (propuesta generada y enviada al cliente)
  3. Negociacion (cliente respondio, ajustes en curso)
  4. Won (evento confirmado y presupuesto aceptado)
  5. Lost (oportunidad no convertida)

- **Pipeline de artistas (separado):**
  1. Solicitud Recibida
  2. Portfolio Revisado
  3. Artista Aprobado
  4. En Catalogo Activo
  5. No Apto

- **Tags automaticos:** por tipo de show, tipo de evento, rango de presupuesto, ubicacion

### FASE 2: Formulario Inteligente + Web (Semanas 2-3)

**Formulario para clientes (embebido o linked desde eventosbarcelona.com):**

- Paso 1: Datos basicos (nombre, empresa, email, telefono)
- Paso 2: Tipo de evento (selector con las categorias)
- Paso 3: Tipo de espectaculo de interes (con imagenes, logica condicional)
- Paso 4: Detalles (fecha, asistentes, presupuesto, ubicacion)
- Paso 5: Comentarios adicionales

El formulario se integra con el CRM y clasifica el lead automaticamente.

**Formulario para artistas (separado):**

- Datos personales
- Tipo de espectaculo / disciplina
- Portfolio / video / reel
- Disponibilidad
- Tarifa orientativa

### FASE 3: Generacion de Propuestas Web + Human in the Loop (Semanas 3-5)

**Este es el nucleo del proyecto** — donde se elimina el 80-90% del trabajo manual.

**Como funciona:**

1. Se crean **templates HTML de propuestas** alojadas en un subdominio (ej: propuestas.eventosbarcelona.com)
   - Diseno profesional que replica el estilo de la web de Eventos Barcelona
   - Variables dinamicas: nombre_cliente, empresa, tipo_evento, fecha, shows, precios, etc.
   - Cada propuesta tiene una URL unica (ej: propuestas.eventosbarcelona.com/zurich-gala-2026)

2. Cuando un lead es clasificado en GHL, un **workflow con custom code**:
   - Selecciona los shows relevantes segun tipo de evento y preferencias del lead
   - Calcula precios con el margen configurado
   - Genera la pagina web de la propuesta con los datos del lead
   - **Mueve el lead a etapa "Pendiente de revision"**

3. **Human in the loop — Xavi revisa antes de enviar:**
   - Recibe notificacion (app GHL / email / WhatsApp) con resumen del lead y link a la propuesta
   - Abre la propuesta y revisa shows, precios, textos
   - **Si quiere modificar:** edita directamente en GHL (custom fields del contacto):
     - Cambiar shows incluidos (selector multiple)
     - Ajustar margen/precio (campo numerico)
     - Anadir nota personalizada (campo texto)
     - Al guardar, la propuesta web se regenera automaticamente
   - **Cuando esta listo:** hace clic en "Aprobar y enviar" → workflow envia email al cliente con el link

4. **Ningun lead recibe una propuesta sin la aprobacion explicita de Xavi**

**Precios y margenes:**
- Los precios base de cada show se guardan como **custom values en GHL** (no hace falta Google Sheets)
- El margen se configura por tipo de evento o se ajusta manualmente por lead
- Xavi puede cambiar precios globales desde GHL sin tocar codigo

### FASE 4: Automatizaciones, Secuencias y Newsletters (Semanas 4-5)

**Workflows automaticos en GHL:**

| Trigger | Accion |
|---------|--------|
| Nuevo lead entra (via formulario inteligente) | Clasificacion + tag + mover a pipeline |
| Lead clasificado | Generar propuesta web (custom code) + notificar a Xavi |
| Xavi aprueba propuesta | Enviar email al cliente con link a la propuesta |
| Propuesta enviada | Email de seguimiento a las 48h |
| Sin respuesta 5 dias | Segundo seguimiento automatico |
| Sin respuesta 10 dias | Tercer seguimiento + oferta especial opcional |
| Cliente responde | Notificacion a Xavi + mover etapa |
| Evento confirmado (Won) | Crear contacto + factura en Holded (custom code via API) |
| Evento completado | Email de agradecimiento + solicitar resena |

**Campanas de newsletter:**
- Newsletters periodicas a la base de contactos segmentada
- Contenido: nuevos shows, casos de exito, tendencias en eventos
- Automatizacion de envio programado desde GHL
- Segmentacion por tipo de evento, tipo de cliente y nivel de engagement

**Revision y aprobacion de propuestas — todo en la misma pagina web:**

Xavi recibe un email con el link a la propuesta. La abre y ve **exactamente** lo que vera el cliente, pero con una barra de admin arriba (solo visible para el via token en la URL).

**Flujo:**

1. GHL genera la propuesta → envia email a Xavi con link de revision
2. Xavi abre: `propuestas.eventosbarcelona.com/zurich-gala?admin=token123`
3. Ve la propuesta completa + barra de admin con dos botones: **[Aprobar y enviar]** y **[Modificar]**
4. Si pulsa **"Aprobar"** → el servidor envia la propuesta al cliente (URL limpia, sin barra de admin)
5. Si pulsa **"Modificar"** → se despliega un chat con agente IA en la misma pagina:

```
💬 ¿Que quieres cambiar?

👤 Xavi: Quita el violin, pon los Alien Businessmen y baja el margen al 10%

🤖 IA: Hecho. He actualizado la propuesta:
   • LED Dancers — 3.000€
   • Alien Businessmen — 3.750€
   • DJ & VJ — 1.800€
   Margen: 10% | Total: 9.405€
   Revisa los cambios arriba.

👤 Xavi: Perfecto, envia

🤖 IA: ✅ Propuesta enviada a carlos@zurich.es
   Seguimiento automatico programado en 48h
```

6. La propuesta se actualiza en tiempo real mientras Xavi chatea
7. Al aprobar, el cliente recibe la URL limpia por email

**Cero apps externas. Sin Telegram. Sin panel separado.** Xavi revisa, modifica con IA y aprueba desde la misma propuesta web.

**Stack tecnico:**

| Componente | Funcion | Coste |
|------------|---------|-------|
| Servidor Node.js (Railway) | Genera propuestas web, sirve paginas, gestiona chat IA, conecta con GHL | ~5€/mes |
| GPT-4o mini (API OpenAI) | Interpreta instrucciones de Xavi en lenguaje natural | ~2€/mes |
| GHL API | Lee/escribe datos del lead, dispara workflows de envio y seguimiento | Incluido en GHL |
| **Total** | | **~7€/mes** |

El servidor es codigo nuestro, desplegado en Railway. Sin dependencias externas. Nosotros lo desarrollamos, desplegamos y mantenemos.

**Ningun lead recibe una propuesta sin que Xavi pulse "Aprobar".**

### FASE 5: Mailgun + Email Marketing (Semana 5-6)

- Configurar dominio eventosbarcelona.com en Mailgun (SPF, DKIM, DMARC)
- Conectar Mailgun como SMTP en GHL
- Migrar contactos de Mailchimp a GHL
- Crear segmentos: clientes anteriores, leads frios, leads calientes, por tipo de evento
- Disenar templates de newsletter en GHL
- Configurar campanas de reactivacion para leads antiguos

### FASE 6: Integracion con Holded (Semana 6-7)

Via GHL custom code + API de Holded:

1. **Cuando un evento se confirma en GHL:**
   - Crear/actualizar contacto en Holded
   - Generar presupuesto o factura con los datos del evento
   - Sincronizar estado

2. **Datos que se envian:**
   - Nombre y datos fiscales del cliente
   - Descripcion del servicio contratado
   - Importe acordado
   - Fecha del evento

### FASE 7: Documentacion y Formacion (Semana 7-8)

- Manual de uso del sistema para la persona que gestionara los leads
- Documentacion de cada workflow y automatizacion
- Videos tutoriales del proceso
- Sesion de formacion en directo (2h)

---

## 6. Donde Vive el Contexto de la Empresa

Todo el conocimiento del negocio se integra en el sistema de la siguiente manera:

| Tipo de conocimiento | Donde se almacena |
|---------------------|-------------------|
| Catalogo de shows y descripciones | Custom Fields + Custom Values en GHL |
| Precios base de cada show | Custom Values en GHL (fuente unica de verdad) |
| Margenes por tipo de evento | Custom Values en GHL |
| Templates de propuestas | Templates HTML generadas por custom code en GHL |
| Proceso comercial | Pipeline de GHL (etapas definidas) |
| Secuencias de seguimiento | Workflows de GHL |
| Base de artistas | Pipeline de artistas en GHL con custom fields |
| Contactos y segmentos | CRM de GHL (migrados de Mailchimp) |
| Facturacion | Holded (sincronizado via API con custom code) |
| Reglas de clasificacion | Logica del formulario + workflows de GHL |

**El fundador solo necesita:**
1. Mantener actualizados los precios y margenes en GHL (Custom Values)
2. Revisar y aprobar cada propuesta antes de enviarla (human in the loop)
3. Editar shows, margen o notas desde los custom fields del contacto si quiere modificar algo

---

## 7. Presupuesto

### Costes de herramientas (mensuales recurrentes)

| Herramienta | Plan | Coste mensual | Notas |
|-------------|------|---------------|-------|
| GoHighLevel | Starter | $97/mes (~89 EUR) | CRM, pipeline, formularios, workflows, custom code, email marketing |
| Mailgun | Foundation | $35/mes (~32 EUR) | 50.000 emails/mes, ampliamente suficiente |
| Servidor propio | Railway + GPT-4o mini | ~7 EUR/mes | Propuestas web + chat IA para revision |
| Holded | (existente) | $0 adicional | Ya en uso |
| **TOTAL MENSUAL** | | **~128 EUR/mes** | |

*Vs Mailchimp + gestion manual: ahorro de tiempo estimado de 25-30h/semana del fundador*

### Coste de implementacion (unico)

| Fase | Descripcion | Horas est. | Precio |
|------|-------------|------------|--------|
| Fase 1 | CRM, pipeline, custom fields, tags | 8h | 600 EUR |
| Fase 2 | Formularios inteligentes + integracion web | 8h | 600 EUR |
| Fase 3 | Generacion de propuestas web + human in the loop (GHL custom code) | 18h | 1.350 EUR |
| Fase 4 | Workflows, newsletters + servidor propuestas web con chat IA | 16h | 1.200 EUR |
| Fase 5 | Mailgun + migracion email marketing | 6h | 450 EUR |
| Fase 6 | Integracion Holded via API | 8h | 600 EUR |
| Fase 7 | Documentacion + formacion | 6h | 450 EUR |
| | **TOTAL IMPLEMENTACION** | **70h** | **5.250 EUR** |

### Opciones de pago

| Opcion | Detalle | Precio |
|--------|---------|--------|
| **Pago unico** | Todo incluido | 5.250 EUR |
| **2 pagos** | 50% al inicio + 50% al completar | 2.625 EUR x 2 |
| **Mensual (3 meses)** | Dividido en 3 pagos | 1.750 EUR x 3 |

### Mantenimiento mensual (opcional)

| Servicio | Precio |
|----------|--------|
| Soporte tecnico + ajustes menores | 200 EUR/mes |
| Soporte + nuevas automatizaciones + optimizacion | 400 EUR/mes |

---

## 8. Fases Futuras (no incluidas en esta propuesta)

### Agente de Voz IA (sustituir oficina virtual)
- Atencion telefonica 24/7 con IA conversacional
- Clasificacion automatica de llamadas
- Integracion directa con GHL (crea el lead automaticamente)
- **Estimacion:** 1.500-2.500 EUR implementacion + coste por minuto de llamada
- GHL tiene integraciones nativas con proveedores de voz IA

### Campanas SEO
- Actualmente gestionado por otra agencia
- En un futuro podemos asumir la estrategia SEO
- Ventaja: control total del funnel desde la atraccion hasta la conversion

### WhatsApp Business
- Canal adicional de entrada de leads
- Respuestas automaticas y seguimiento via GHL
- **Estimacion:** 300-500 EUR implementacion

---

## 9. ROI Estimado

| Metrica | Actual | Con el sistema |
|---------|--------|---------------|
| Tiempo del fundador en propuestas | 80-90% (~35h/semana) | 5-10% (~3h/semana) |
| Tiempo de respuesta a leads | Variable (horas/dias) | < 15 minutos (automatico) |
| Leads sin seguimiento | Desconocido (muchos) | 0% (seguimiento automatico) |
| Capacidad de delegacion | Imposible | 1 persona puede gestionar todo |
| Visibilidad del pipeline | Nula | Total en tiempo real |
| Newsletters enviadas | 0 (abandonado) | Campanas regulares automatizadas |

**Con 2-3 leads/dia y una mejora del 20% en conversion gracias al seguimiento automatico, el sistema se paga solo en 1-2 meses.**

---

## 10. Calendario de Implementacion

```
Semana 1-2:  [====] Fase 1 - CRM y Pipeline
Semana 2-3:  [====] Fase 2 - Formulario Inteligente
Semana 3-5:  [======] Fase 3 - Generador de Propuestas (nucleo)
Semana 4-5:  [====] Fase 4 - Automatizaciones
Semana 5-6:  [====] Fase 5 - Mailgun + Email Marketing
Semana 6-7:  [====] Fase 6 - Integracion Holded
Semana 7-8:  [====] Fase 7 - Documentacion + Formacion
```

**Tiempo total: 8 semanas desde el inicio**

---

## 11. Prototipos Funcionales

Hemos creado dos prototipos interactivos para que veas como funcionaria el sistema en la practica:

### Propuesta web con revision IA
👉 [Ver prototipo de propuesta](ejemplo-propuesta.html)
- Propuesta web completa con shows, precios y resumen
- Barra de admin para Xavi: **Aprobar y enviar** o **Modificar**
- Chat con IA que modifica precios, quita shows y recalcula totales en tiempo real

### Formulario inteligente para leads
👉 [Ver prototipo de formulario](formulario-inteligente.html)
- Formulario paso a paso con experiencia visual
- Seleccion de tipo de evento con iconos
- Seleccion de shows con fotos
- Detalles del evento (fecha, asistentes, presupuesto)

---

## 12. Proximos Pasos

1. **Aprobacion de la propuesta**
2. **Kickoff meeting** - Acceso a cuentas (GHL, Holded, dominio, web)
3. **Recopilacion de materiales** - PowerPoints actuales, lista de precios, contactos de artistas
4. **Inicio Fase 1** - Setup del CRM

---

*Propuesta preparada en marzo 2026.*
*Validez: 30 dias.*
