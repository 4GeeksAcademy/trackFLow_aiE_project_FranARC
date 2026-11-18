---
name: tickets-escalation
description: Estandariza la creación y formateo de tickets de soporte cuando el agente de TrackFlow no puede resolver una consulta de seguimiento de forma autónoma.
---

# Skill: Escalamiento de Tickets (`tickets-escalation`)

## 1. Objetivo Único

Transformar una incidencia de seguimiento no resuelta por el agente de primera línea en un ticket JSON estructurado y listo para su enrutamiento humano (_Man-in-the-Loop_) hacia los equipos de Experiencia del Cliente de TrackFlow (Los Ángeles o Zaragoza).

## 2. Inputs Documentados

Antes de ejecutar esta skill, el agente debe disponer de los siguientes parámetros de entrada:

- `customer_query` _(string, obligatorio)_: Mensaje literal enviado por el cliente (B2C) o marca (B2B).
- `tracking_number` _(string, obligatorio)_: Identificador único del envío consultado.
- `carrier` _(string, obligatorio)_: Transportista asociado (`UPS`, `FedEx`, `MRW`, `SEUR`, `DHL` o `LOCAL`).
- `carrier_raw_status` _(object, obligatorio)_: Último payload o código de estado devuelto por la API del transportista (ej. `LOST`, `DELAYED_CRITICAL`, `ADDRESS_ERROR`).
- `customer_type` _(string, opcional, por defecto `B2C`)_: Tipo de cliente (`B2B` o `B2C`).
- `destination_country` _(string, obligatorio)_: País de destino (`US` o `ES`) para determinar el equipo asignado.

_(Si falta `tracking_number` o `customer_query`, el agente debe solicitarlo al usuario antes de invocar esta skill)._

## 3. Instrucciones de Ejecución y Formato de Salida

Generar un objeto JSON válido siguiendo estrictamente el esquema de referencia en `resources/ticket_schema_example.json`:

- `ticket_id`: Formato `TF-SUP-<TIMESTAMP_UNIX>`.
- `priority`: Asignar `HIGH` si el estado es `LOST` o si `customer_type == "B2B"`; asignar `MEDIUM` para incidencias estándar `B2C`.
- `assigned_team`: Asignar `Customer_Experience_LA` si `destination_country == "US"`, o `Customer_Experience_ZGZ` si `destination_country == "ES"`.

## 4. Criterios de Aceptación (Verificables)

Para considerar válida la ejecución de esta skill, el resultado debe superar estas comprobaciones:

- [ ] **Validez sintáctica:** La salida es un objeto JSON parseable sin errores de sintaxis y contiene las 8 claves definidas en `resources/ticket_schema_example.json`.
- [ ] **Trazabilidad completa:** Los valores de `tracking_number`, `customer_query` y `carrier_raw_status` coinciden exactamente con los inputs recibidos, sin alteraciones ni datos inventados.
- [ ] **Enrutamiento correcto:** El campo `assigned_team` corresponde al país de destino (`LA` para EE. UU., `ZGZ` para España) y `priority` respeta la regla `B2B`/`LOST` -> `HIGH`.
- [ ] **Confirmación al usuario:** Se informa al cliente en su mismo idioma (español o inglés) el `ticket_id` generado antes de cerrar la interacción.
