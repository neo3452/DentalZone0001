# ESTADO_ACTUAL — Dental Zone OS

Última actualización base: 2026-09-30

## Propósito

Este documento mantiene el estado operativo resumido de Dental Zone OS.

No contiene reglas de comportamiento del agente.  
Las reglas permanentes están en `AGENTS.md`.

Este archivo debe permitir a un agente entender rápidamente:

- qué existe;
- qué está terminado;
- qué está en curso;
- qué está pendiente;
- qué componentes son autoridades reales del sistema.

---

## Plataforma

- VPS Hostinger con Docker.
- n8n 2.26.8 Self Hosted.
- Chatwoot 4.15.1 Docker.
- PostgreSQL 16.
- Redis.
- Qdrant.
- Gotenberg.
- Dominio humano principal: `os.dentalzone.gt`.

---

## Arquitectura general

Dental Zone OS integra principalmente:

Paciente / personal
→ interfaces Dental Zone
→ n8n
→ PostgreSQL
→ Chatwoot / WhatsApp / Twilio
→ Google Calendar / Gmail
→ servicios clínicos e inventario

Principio obligatorio:

No crear sistemas paralelos cuando ya exista una autoridad real dentro de Dental Zone.

---

## Módulos principales

### Expediente Clínico

Existe y es autoridad clínica principal.

Incluye:

- consultas / visitas clínicas;
- procedimientos;
- notas;
- fotografías;
- materiales;
- rectificaciones;
- citas relacionadas.

El Odontograma debe integrarse con este expediente y no duplicarlo.

### Odontograma

Estado: EN DESARROLLO.

Principios confirmados:

- forma parte del Expediente Clínico;
- identidad dental FDI;
- estado inicial y final por consulta;
- autoguardado continuo;
- procedimientos usan el catálogo existente;
- notas, fotos y consultas no se duplican;
- contexto anatómico se agrega como información asociada;
- reconstrucción histórica del estado de cada pieza.

Interfaz 3D actualmente en trabajo.

FDI 11:
- miniatura y cámaras funcionales.

FDI 12:
- funcional con ajustes visuales pendientes.

Pendiente:
- continuar desarrollo de las demás piezas;
- integrar completamente historial y persistencia clínica.

### Inventario / Kits

Existe configuración de materiales por procedimiento.

Autoridad principal:

`DZ_configuracion_materiales_procedimiento_v1`

Reglas:

- KIT se congela por consulta;
- cambios posteriores no son retroactivos;
- EXTRAS se registran por separado;
- existe una bodega general.

### Centro de Contacto

Chatwoot conectado con Dental Zone.

Existe control de atención humana y automatizada.

Atributos relevantes:

- `desactiva_bot`
- `emergencia`

Existe transferencia a atención humana mediante workflow dedicado.

### Agenda

Google Calendar integrado.

Horario operativo principal:

Lunes a viernes, 08:00–16:00.

Existe antecedente de vencimiento semanal de OAuth mientras el proyecto Google permanecía en Testing.

### Personal

Existe gestión de empleados, puestos y profesionales.

PostgreSQL valida credenciales.

Dental Zone OS mantiene autoridad adicional sobre empleados y configuración operativa.

---

## Git / Cursor

Repositorio actual:

`neo3452/DentalZone0001`

Repositorio local:

`E:\20Cursor\DentalZone0001`

Rama principal:

`main`

Cursor se está configurando como entorno principal de desarrollo de largo plazo.

Archivo de reglas permanentes:

`AGENTS.md`

---

## Estado inmediato

Objetivo actual:

Configurar correctamente Cursor antes de trasladar trabajo productivo de Dental Zone.

Todavía no:

- hacer deploy;
- modificar producción;
- reconstruir arquitectura;
- importar masivamente código;
- crear automatizaciones de Cursor;
- habilitar Subagents;
- habilitar Hooks.

---

## Regla de actualización

Actualizar este documento cuando cambie el estado real de un módulo.

No registrar aquí hipótesis como hechos.

Cuando exista contradicción:

evidencia real actual
→ prevalece sobre este documento