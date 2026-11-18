# Project Brief: TrackFlow AI Engineering Integration

## 1. Contexto General de la Empresa

TrackFlow es una empresa de entrega de última milla y gestión de almacenes fundada en 2009, con operaciones en **Estados Unidos y España** (almacenes en Los Ángeles y Zaragoza). Cuenta con ~130 empleados y factura ~9 millones de euros anuales.
El mandato de **TrackFlow Tech** es unificar sistemas fragmentados y automatizar procesos manuales mediante sistemas inteligentes.

## 2. Foco Estratégico del Proyecto (Alcance Prioritario)

De acuerdo con la definición estratégica del proyecto (`company_choice.md`), el desarrollo se centra en la intersección de dos áreas críticas:

1. **Experiencia del Cliente:** Resolución automática de consultas repetitivas sobre estado de pedidos y devoluciones, evitando la consulta manual en documentos estáticos.
2. **Última Milla y Gestión de Transportistas:** Unificación de consultas de seguimiento entre múltiples transportistas (UPS, FedEx, MRW, SEUR, DHL y locales).

## 3. Flujo Objetivo del Agente de IA Principal

- **Entrada:** Consulta del cliente (B2C o marca B2B) con número de seguimiento.
- **Procesamiento:** El agente consulta de forma unificada el estado disponible en el sistema del transportista correspondiente.
- **Salida / Escalamiento:**
  - Si obtiene respuesta clara, informa directamente al cliente sobre el estado del envío.
  - Si no puede resolver la consulta o detecta una incidencia compleja, genera automáticamente un **ticket unificado** adjuntando la pregunta original, el número de seguimiento y el contexto consultado para que un agente humano continúe la atención (_Man-in-the-Loop_).

## 4. Objetivos Técnicos del Monorepo

- Dotar al repositorio de memoria persistente (`memory-bank/`), reglas de comportamiento (`AGENTS.md` / `.agents/rules/`) y habilidades reutilizables (`skills/`).
- Construir integraciones limpias, documentadas y escalables bajo arquitectura Full Stack + IA.
