# Reglas de Dominio: Experiencia del Cliente y Última Milla (TrackFlow)

## 1. Integración con Transportistas

- Los transportistas soportados oficialmente son: **UPS, FedEx, DHL** (EE. UU.) y **MRW, SEUR, DHL** (España), más dos transportistas locales configurables.
- Toda consulta de seguimiento debe normalizarse a un esquema común (`tracking_number`, `carrier`, `status`, `estimated_delivery`, `last_event`) antes de entregarse al modelo de lenguaje.

## 2. Protocolo de Atención al Cliente y Escalamiento (_Man-in-the-Loop_)

- **Idioma:** Responder en el mismo idioma en el que escriba el usuario (Español o Inglés).
- **Resolución Autónoma:** Si el estado del envío es claro (`IN_TRANSIT`, `DELIVERED`, `OUT_FOR_DELIVERY`), responder directamente con los datos actualizados.
- **Generación Obligatoria de Ticket:** Si el paquete figura como `LOST`, `DELAYED_CRITICAL`, `ADDRESS_ERROR` o si el cliente expresa frustración explícita, el agente **NO debe improvisar soluciones**. Debe generar un ticket en el sistema unificado incluyendo:
  1. Pregunta original del cliente.
  2. Número de seguimiento (`tracking_number`).
  3. Payload crudo consultado al transportista.
