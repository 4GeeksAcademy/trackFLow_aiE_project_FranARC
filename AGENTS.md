# AGENTS.md — Reglas de Gobernanza para Agentes de IA (TrackFlow)

Este archivo define las instrucciones obligatorias, límites de seguridad y flujos de trabajo que cualquier agente de IA debe respetar al operar dentro del monorepo de **TrackFlow** (`trackFLow_aiE_project_FranARC`).

---

## 1. Protocolo Obligatorio de Lectura de Contexto

Antes de proponer arquitectura, escribir código o modificar cualquier archivo, el agente **DEBE** leer en este orden:

1. `memory-bank/projectBrief.md` (para alinear la tarea con el alcance de **Experiencia del Cliente** y **Última Milla**).
2. `memory-bank/techContext.md` (para respetar el stack y las decisiones técnicas).
3. `memory-bank/progress.md` (para conocer el estado actual y evitar duplicar trabajo).

---

## 2. Restricciones Estrictas de Modificación y Seguridad

- **Prohibición de Secretos:** Nunca escribir, mostrar ni confirmar claves de API, tokens, contraseñas o archivos `.env` en el código fuente. Verificar siempre que `.env` esté listado en `.gitignore`.
- **Respeto al Alcance:** No generar código ni documentación para departamentos fuera del alcance definido en `company_choice.md` (Almacén, RR.HH. o Dirección Ejecutiva), salvo solicitud explícita del desarrollador.
- **Control Humano (_Man-in-the-Loop_):** Ningún agente puede ejecutar `git push`, fusionar ramas (`merge`) ni borrar archivos estructurales (`briefing.md`, `company_choice.md`, `.devcontainer/`) sin confirmación expresa del desarrollador.
- **Cero Suposiciones:** Si falta información sobre un endpoint de transportista (UPS, FedEx, MRW, SEUR, DHL) o regla de negocio, preguntar antes de inventar esquemas de datos.

---

## 3. Flujo Obligatorio de Commit (Mínimo 4 Pasos)

Cada vez que se complete una tarea o unidad lógica de trabajo, el agente debe guiar o ejecutar exactamente este flujo de control de versiones:

1. **Verificación de Estado y Seguridad (`git status` / `git diff`):** Comprobar qué archivos han sido creados o modificados y auditar que no existan credenciales expuestas ni archivos temporales basura.
2. **Validación Técnica y Actualización de Memoria:** Verificar que el código o documentación cumple con la especificación y actualizar `memory-bank/progress.md` reflejando el nuevo avance.
3. **Preparación Selectiva (`git add <archivos>`):** Añadir al área de preparación (_staging_) únicamente los archivos correspondientes a la tarea atómica actual (evitar `git add .` a ciegas).
4. **Registro Semántico (`git commit`):** Confirmar los cambios utilizando mensajes claros siguiendo el estándar _Conventional Commits_ (ej. `feat:`, `docs:`, `fix:`, `chore:`).
5. **Sincronización Remota (`git push origin <rama>`):** Subir los cambios a la rama de trabajo activa (nunca directamente a `main`) previa aprobación del desarrollador.
