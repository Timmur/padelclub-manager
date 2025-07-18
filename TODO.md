# TODO - SaaS Pádel 1.0

## Planificación de Desarrollo - Estructura Playtomic Manager

### FASE 0: Configuración Inicial (Completado)

- [x] **[2025-07-18]** Crear repositorio GitHub - **Dificultad: FÁCIL**
  - Configurar repositorio padelclub-manager
  - Crear README.md profesional
  - Configurar .gitignore
  - Subir documentación inicial (PRD, PRP, TODO)
  - Archivos: README.md, .gitignore, documentación completa
  - Tiempo estimado: 2 horas
  - Dependencias: Ninguna

### FASE 1: Arquitectura Base (Semana 1-2)

- [x] **[2025-01-20]** Configurar estructura de proyecto base - **Dificultad: MEDIO**
  - Configurar Next.js 14 con TypeScript
  - Implementar sistema de autenticación
  - Configurar base de datos (Prisma + PostgreSQL)
  - [x] Configurar Docker para desarrollo local
  - Archivos: package.json, prisma/schema.prisma, lib/auth.ts, docker-compose.yml, Dockerfile
  - Tiempo estimado: 8-10 horas
  - Dependencias: Ninguna

 [x] **[2025-01-22]** Crear layout principal del dashboard - **Dificultad: MEDIO** [2025-07-18]
  - Implementar sidebar con navegación estilo Playtomic
  - Crear header con usuario y notificaciones
  - Configurar routing para todas las secciones
  - Archivos: components/layout/, app/dashboard/layout.tsx
  - Tiempo estimado: 6-8 horas
  - Dependencias: Estructura base configurada

### FASE 2: Módulo Métricas (Semana 3)

 [x] **[2025-01-27]** Implementar dashboard de métricas - **Dificultad: DIFÍCIL** [2025-07-18]
  - Crear KPIs principales (partidos, ingresos, usuarios, nuevos usuarios)
  - Implementar gráficos de barras para partidos por día
  - Configurar filtros de tiempo (últimas 2 semanas, etc.)
  - Archivos: app/dashboard/metricas/, components/charts/
  - Tiempo estimado: 12-15 horas
  - Dependencias: Layout principal

 [x] **[2025-01-29]** Integrar analytics en tiempo real - **Dificultad: EXPERTO** [2025-07-18]
  - Configurar tracking de eventos
  - Implementar cálculos de métricas automáticos
  - Crear sistema de alertas para métricas críticas
  - Archivos: lib/analytics.ts, api/metrics/
  - Tiempo estimado: 10-12 horas
  - Dependencias: Dashboard de métricas

### FASE 3: Gestión de Partidos (Semana 4-5)

- [ ] **[2025-02-03]** Crear módulo de gestión de partidos - **Dificultad: DIFÍCIL**
  - Implementar lista de partidos con filtros
  - Crear formularios para reservas online/offline
  - Configurar estados de partidos (confirmado, pendiente, cancelado)
  - Archivos: app/dashboard/partidos/, domains/bookings/
  - Tiempo estimado: 15-18 horas
  - Dependencias: Métricas implementadas

## **[2025-02-05] Implementar Sistema de Calendario de Pistas - Dificultad: MUY-ALTO**

### **Especificaciones Técnicas**

**Duración estimada:** 12-15 horas  
**Dependencias:** Gestión de partidos, Sistema de reservas  
**Prioridad:** Alta

### **1. Vista de Calendario Diaria**

#### **Layout y Estructura**
- **Eje Y (Vertical):** Listado de pistas disponibles
- **Eje X (Horizontal):** Franjas horarias en intervalos de 30 minutos
- **Duración estándar:** 1.5 horas (3 slots consecutivos)
- **Duración mínima:** 30 minutos (1 slot)
- **Duración máxima:** Configurable por club

#### **Componentes Principales**
- Componente principal del grid de calendario
- Slot individual de tiempo
- Fila de pista
- Tarjeta de reserva
- Configuración de disponibilidad
- Controles de navegación

### **2. Sistema de Estados Visuales**

#### **Códigos de Color**
- **🟢 Verde:** Partido completado (4 jugadores confirmados)
- **🟡 Amarillo:** Partido creado pero incompleto (1-3 jugadores)
- **🔴 Rojo:** Mantenimiento o pista no disponible
- **⚪ Blanco:** Slot libre y disponible
- **🔵 Azul:** Reserva administrativa/evento especial

#### **Información del Slot**
Cada slot debe mostrar:
- ID único del slot
- Pista asignada
- Hora de inicio y fin
- Lista de jugadores
- Estado del partido
- Tipo de reserva
- Estado de pago

### **3. Funcionalidad Drag & Drop**

#### **Casos de Uso**
- **Mover reserva:** Cambiar horario manteniendo pista
- **Cambiar pista:** Mover a otra pista en mismo horario
- **Redimensionar:** Ajustar duración en tramos de 30 min
- **Duplicar:** Crear reserva recurrente

#### **Validaciones en Tiempo Real**
- Verificar disponibilidad de pista de destino
- Validar conflictos de horarios
- Confirmar capacidad de jugadores
- Comprobar restricciones de club

### **4. Configuración de Disponibilidad**

#### **Parámetros por Pista**
- Horario de apertura y cierre
- Slots de mantenimiento programado
- Fechas bloqueadas
- Tarifas especiales por horario
- Duración mínima y máxima de reserva

### **5. Tareas Específicas de Implementación**

#### **Fase 1: Estructura Base (4-5 horas)**
- [ ] Crear componente de grid de calendario con layout responsive
- [ ] Implementar slots de tiempo con estados visuales
- [ ] Configurar sistema de colores y estilos
- [ ] Integrar con API de pistas y reservas

#### **Fase 2: Drag & Drop (5-6 horas)**
- [ ] Configurar biblioteca de drag & drop
- [ ] Implementar lógica de movimiento entre slots
- [ ] Agregar validaciones en tiempo real
- [ ] Manejar estados de carga y error

#### **Fase 3: Configuración Avanzada (3-4 horas)**
- [ ] Crear panel de configuración de disponibilidad
- [ ] Implementar restricciones por tipo de usuario
- [ ] Agregar notificaciones de cambios
- [ ] Optimizar rendimiento para múltiples pistas

### **6. Consideraciones Técnicas**

#### **Rendimiento**
- Implementar virtualización para calendarios con muchas pistas
- Usar memoización para evitar re-renders innecesarios
- Optimizar queries con paginación por días

#### **Accesibilidad**
- Navegación por teclado para drag & drop
- Compatibilidad con lectores de pantalla
- Contraste adecuado para estados visuales

#### **Responsive Design**
- Vista móvil con scroll horizontal
- Tablet con layout adaptativo
- Desktop con vista completa

### **7. Criterios de Aceptación**

- [ ] El calendario muestra todas las pistas disponibles
- [ ] Los slots reflejan estados correctos con colores apropiados
- [ ] Drag & drop funciona sin conflictos
- [ ] Validaciones previenen dobles reservas
- [ ] Configuración de disponibilidad es persistente
- [ ] Rendimiento óptimo con 20+ pistas simultáneas
- [ ] Interfaz responsive en todos los dispositivos
- [ ] Accesibilidad completa para usuarios con discapacidades

### **8. Entregables**

- [ ] Componente de calendario funcional
- [ ] Documentación de uso
- [ ] Tests unitarios y de integración
- [ ] Configuración de disponibilidad por pista
- [ ] Manual de usuario para administradores
- [ ] Validación de rendimiento con datos reales

### FASE 4: Sistema de Comunicación (Semana 6)

- [ ] **[2025-02-10]** Desarrollar módulo de chats - **Dificultad: EXPERTO**
  - Implementar chat en tiempo real con WebSockets
  - Crear sistema de notificaciones push
  - Configurar chat grupal para partidos
  - Archivos: app/dashboard/chats/, lib/websocket.ts
  - Tiempo estimado: 20-25 horas
  - Dependencias: Gestión de partidos

### FASE 5: Página Pública Estilo Playtomic (Semana 7)

- [ ] **[2025-02-17]** Desarrollar interfaz de búsqueda de partidos - **Dificultad: DIFÍCIL**
  - Implementar búsqueda y filtrado avanzado de partidos
  - Crear vista de mapa con ubicaciones de pistas
  - Desarrollar lista detallada con información completa
  - Archivos: app/public/[club]/buscar-partidos/, domains/public/
  - Tiempo estimado: 15-18 horas
  - Dependencias: Sistema de comunicación

- [ ] **[2025-02-19]** Integrar sistema de reservas públicas - **Dificultad: MEDIO**
  - Conectar interfaz pública con módulo de partidos
  - Implementar sistema de pagos para usuarios públicos
  - Crear perfiles de jugadores y sistema de reputación
  - Archivos: app/public/[club]/partido/, api/public/
  - Tiempo estimado: 12-15 horas
  - Dependencias: Interfaz de búsqueda
  - **Nota**: Permitir que los clubes apunten sus DNS a esta parte pública del SaaS para una integración de marca sin fricciones.

### FASE 6: Facturación y Configuración (Semana 8)

- [ ] **[2025-02-24]** Crear módulo de facturación - **Dificultad: MEDIO**
  - Implementar generación automática de facturas
  - Configurar reportes de ingresos
  - Integrar con sistema contable
  - Archivos: app/dashboard/facturacion/, domains/billing/
  - Tiempo estimado: 10-12 horas
  - Dependencias: Sistema de reservas públicas

- [ ] **[2025-02-26]** Finalizar módulo de ajustes - **Dificultad: FÁCIL**
  - Crear configuración general del club
  - Implementar gestión de usuarios y permisos
  - Configurar preferencias del sistema
  - Archivos: app/dashboard/ajustes/, domains/settings/
  - Tiempo estimado: 6-8 horas
  - Dependencias: Módulo de facturación

### FASE 7: Testing y Optimización (Semana 9-10)

- [ ] **[2025-03-03]** Implementar testing completo - **Dificultad: MEDIO**
  - Crear tests unitarios para todos los dominios
  - Implementar tests de integración
  - Configurar tests E2E con Playwright
  - Archivos: __tests__/, e2e/
  - Tiempo estimado: 15-20 horas
  - Dependencias: Todos los módulos MVP completados

- [ ] **[2025-03-05]** Optimización y deployment - **Dificultad: MEDIO**
  - Optimizar rendimiento y SEO
  - Configurar CI/CD pipeline
  - Preparar documentación de usuario
  - Archivos: .github/workflows/, docs/
  - Tiempo estimado: 8-10 horas
  - Dependencias: Testing completado

### FASE 8: Mejoras Futuras (Post-MVP) (Semana 11+)

- [ ] **[2025-03-10]** Desarrollar módulo de clases - **Dificultad: MEDIO**
  - Implementar CRUD de clases grupales e individuales
  - Configurar horarios recurrentes y excepciones
  - Gestionar inscripciones y listas de espera
  - Archivos: app/dashboard/mejoras/clases/, domains/classes/
  - Tiempo estimado: 12-15 horas
  - Dependencias: MVP completado

- [ ] **[2025-03-17]** Crear sistema de ligas - **Dificultad: DIFÍCIL**
  - Implementar gestión de ligas con clasificaciones
  - Configurar inscripciones y gestión de cupos
  - Crear seguimiento de resultados y estadísticas
  - Archivos: app/dashboard/mejoras/ligas/, domains/leagues/
  - Tiempo estimado: 18-22 horas
  - Dependencias: Módulo de clases

- [ ] **[2025-03-24]** Implementar gestión de torneos - **Dificultad: EXPERTO**
  - Crear brackets eliminatorios automáticos
  - Implementar gestión de inscripciones con límites
  - Configurar sistema de premios y certificados
  - Archivos: app/dashboard/mejoras/torneos/, domains/tournaments/
  - Tiempo estimado: 25-30 horas
  - Dependencias: Sistema de ligas

- [ ] **[2025-03-31]** Desarrollar Plugin WordPress para integración - **Dificultad: MEDIO**
  - Crear plugin básico para incrustar la PWA/SPA o enlazarla
  - Implementar shortcode para fácil inserción en páginas de WP
  - Archivos: plugins/wordpress-integration/
  - Tiempo estimado: 10-15 horas
  - Dependencias: Página Pública Estilo Playtomic

- [ ] **[2025-04-07]** Documentar integración vía Iframe - **Dificultad: FÁCIL**
  - Crear guía detallada para incrustar la PWA/SPA mediante iframe
  - Incluir consideraciones de seguridad y UX para iframes
  - Archivos: docs/integracion/iframe.md
  - Tiempo estimado: 2-5 horas
  - Dependencias: Página Pública Estilo Playtomic

- [ ] **[2025-04-14]** Planificación y Diseño de APP Móvil Nativa - **Dificultad: EXPERTO**
  - Definir alcance y funcionalidades clave para una APP móvil nativa (iOS/Android)
  - Diseñar arquitectura inicial y experiencia de usuario para la APP
  - Archivos: docs/app-nativa/planificacion.md
  - Tiempo estimado: 80-120 horas (solo planificación y diseño inicial, desarrollo posterior)
  - Dependencias: Página Pública Estilo Playtomic, API Pública

## Notas de Arquitectura

### Tecnologías Principales
- **Frontend**: Next.js 14, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes, Prisma ORM
- **Base de Datos**: PostgreSQL
- **Autenticación**: NextAuth.js
- **Pagos**: Stripe
- **Real-time**: WebSockets (Socket.io)
- **Charts**: Recharts o Chart.js
- **Testing**: Jest, React Testing Library, Playwright

### Patrones de Desarrollo
- Domain-Driven Design (DDD)
- Repository Pattern para acceso a datos
- Service Layer para lógica de negocio
- Component-based architecture
- API-first approach

### Métricas de Éxito
- Tiempo de carga < 2 segundos
- 99.9% uptime
- Cobertura de tests > 80%
- Responsive design 100%
- Accesibilidad WCAG 2.1 AA

### Usabilidad y Aspecto Visual

**Principios Generales de Diseño**
- **Diseño Responsive**: Adaptación perfecta a móviles, tablets y desktop
- **Tema Visual Unificado**: Paleta de colores profesional y consistente
- **Accesibilidad**: Cumplimiento WCAG 2.1 AA para todos los usuarios
- **Navegación Intuitiva**: Flujos optimizados para completar tareas rápidamente
- **Rendimiento**: Carga rápida (<2s) incluso en conexiones lentas
- **Consistencia**: Patrones de diseño uniformes en toda la plataforma

**Dashboard Administrativo**
- **Interfaz Limpia**: Espacio negativo para reducir carga cognitiva
- **Jerarquía Visual**: Elementos importantes destacados con tamaño/color
- **Componentes Reutilizables**: Patrones consistentes para formularios, tablas
- **Feedback Inmediato**: Notificaciones claras para acciones del usuario
- **Modo Oscuro**: Opción para reducir fatiga visual en largas sesiones

**Página Pública del Club**
- **Branding Flexible**: Adaptación a identidad visual de cada club
- **Call-to-Actions Claros**: Botones prominentes para reservas/contacto
- **Imágenes de Alta Calidad**: Muestran ambiente real del club
- **Tipografía Legible**: Fuentes optimizadas para lectura rápida
- **Microinteracciones**: Animaciones sutiles para mejorar experiencia

## Métricas del Proyecto

### MVP (Fases 1-7)
- **Tiempo estimado total**: 147-173 horas
- **Duración**: 10 semanas (20 de enero - 7 de marzo 2025)
- **Módulos incluidos**: Métricas, Partidos, Chats, Página Pública Playtomic, Facturación, Configuración

### Mejoras Futuras (Fase 8)
- **Tiempo estimado**: 147-207 horas
- **Módulos**: Clases, Ligas, Torneos, Plugin WP, Iframe, APP Nativa (planificación/diseño)

### Total del Proyecto
- **Tiempo total estimado**: 294-380 horas
- **Duración completa**: 13+ semanas (semanas adicionales para las nuevas mejoras)

### Desglose por Módulo MVP
1. **Arquitectura Base**: 14-18 horas
2. **Métricas y Dashboard**: 22-27 horas
3. **Gestión de Partidos**: 23-28 horas
4. **Sistema de Comunicación**: 20-25 horas
5. **Página Pública Playtomic**: 27-33 horas
6. **Facturación**: 10-12 horas
7. **Configuración**: 6-8 horas
8. **Testing y Deployment**: 23-30 horas

---

**Última actualización**: 2025-01-20