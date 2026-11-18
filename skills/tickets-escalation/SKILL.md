---
name: tickets-escalation
description: Estandariza la creación y formateo de tickets de soporte cuando el agente de TrackFlow no puede resolver una consulta de seguimiento de forma autónoma.
---

# Instrucciones para Escalamiento de Tickets (TrackFlow)

Cuando una consulta de seguimiento requiera intervención humana, genera un objeto JSON estructurado con los siguientes campos obligatorios antes de confirmar al usuario que su caso ha sido derivado:

- `ticket_id`: Generado con formato `TF-SUP-<TIMESTAMP>`.
- `priority`: `HIGH` (si es pérdida o cliente B2B) o `MEDIUM` (incidencia estándar B2C).
- `tracking_number`: Número de guía consultado.
- `carrier`: Transportista asociado (UPS, FedEx, MRW, SEUR, DHL, LOCAL).
- `customer_query`: Texto literal de la consulta del usuario.
- `carrier_raw_status`: Último estado técnico devuelto por la API de seguimiento.
- `assigned_team`: `Customer_Experience_LA` (si el envío es en EE. UU.) o `Customer_Experience_ZGZ` (si el envío es en España).
