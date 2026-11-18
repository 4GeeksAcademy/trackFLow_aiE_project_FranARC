# Technical Context: TrackFlow AI Engineering Integration

## 1. Stack Tecnológico General (Monorepo)
- **Entorno de Desarrollo:** GitHub Codespaces (`bug-free train`) sobre contenedor Docker (`devcontainer`).
- **Control de Versiones:** Git y GitHub (Rama activa: `feature/agent-memory-bank`).
- **Lenguajes principales:** 
  - Python / TypeScript (según la capa de servicios y agentes).
- **Gestión de Dependencias y Paquetes:** Estructura de monorepo organizada en carpetas (`services/`, `shared/`, `agents/`, `skills/`).

## 2. Tecnologías Clave para el Alcance Seleccionado
- **Capa de Agentes e IA:** Modelos de lenguaje integrados mediante la plataforma de la academia / proveedores externos, gobernados por el banco de memoria y reglas estrictas de agentes (`AGENTS.md`).
- **Integraciones y APIs (Última Milla):** Endpoints unificados para consultar el estado de envíos entre múltiples transportistas (UPS, FedEx, MRW, SEUR, DHL y transportistas locales).
- **Automatización y Tickets (Experiencia del Cliente):** 
  - Motor de procesamiento de consultas para resolución automática.
  - Sistema unificado de generación de tickets de respaldo para escalado humano (*Man-in-the-Loop*).

## 3. Restricciones Técnicas y de Seguridad
- **Protección de Credenciales:** Prohibido subir claves de API, tokens o secretos al repositorio. Uso obligatorio de variables de entorno (`.env`) y exclusión estricta en `.gitignore`.
- **Aislamiento de Contexto:** Los agentes deben consultar siempre el `memory-bank/` antes de ejecutar tareas complejas para evitar alucinaciones o pérdida de directrices de negocio.
- **Commits Atómicos:** Cada hito funcional debe validarse localmente antes de registrar cambios semánticos en Git.