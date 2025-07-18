# CLAUDE.md - Reglas del Proyecto
## PadelClub Manager - Herramienta B2B para Gestión de Clubes

**Fecha**: 17 de Julio, 2025  
**Versión**: 2.1 (Corregido - Enfoque B2B)  
**Tipo**: SaaS B2B para Administradores de Clubes de Pádel

---

## Concepto Fundamental del Proyecto

### ⚠️ CORRECCIÓN CRÍTICA DE CONCEPTO

**PadelClub Manager NO es una app para jugadores**. Es una **herramienta B2B de gestión para clubes**.

**Analogía correcta**: Somos como "Playtomic Manager" o "Shopify para clubes de pádel"

**Usuarios principales**:
- ✅ **Administradores de clubes** (dashboard completo)
- ✅ **Personal del club** (recepcionistas, gerentes)
- ✅ **Propietarios de clubes** (analytics y reportes)

**Usuarios secundarios**:
- ✅ **Jugadores** (solo página pública simple para apuntarse)

### Flujo de Uso Correcto

1. **Club se suscribe** a PadelClub Manager (€49-199/mes)
2. **Administrador configura** pistas, horarios, precios
3. **Personal del club usa dashboard** para gestionar reservas diarias
4. **Jugadores ven página pública** del club para apuntarse a partidos
5. **Club analiza datos** para optimizar su negocio

## Arquitectura de la Aplicación

### Dos Interfaces Principales

#### 1. Dashboard Administrativo (Interfaz Principal)
**URL**: `app.padelclub.com/dashboard`
**Usuarios**: Administradores y personal del club
**Funcionalidades**:
- Gestión completa de reservas
- Configuración de pistas y precios
- Gestión de miembros del club
- Analytics y reportes
- Configuración del club

#### 2. Página Pública del Club (Interfaz Secundaria)
**URL**: `{club-slug}.padelclub.com` o `padelclub.com/club/{slug}`
**Usuarios**: Jugadores del público general
**Funcionalidades**:
- Ver disponibilidad de pistas
- Apuntarse a partidos abiertos
- Ver información del club
- Contactar con el club

### Separación Clara de Responsabilidades

```
/dashboard/          # Interfaz administrativa completa
├── metricas/       # Dashboard principal con KPIs y estadísticas
├── partidos/       # Gestión de partidos y reservas
├── chats/          # Sistema de mensajería con jugadores
├── facturacion/    # Facturación y pagos
├── ajustes/        # Configuración del club y sistema
└── mejoras/        # Fase de mejoras futuras
    ├── clases/     # Gestión de clases y entrenamientos (Futuro desarrollo)
    ├── ligas/      # Organización de ligas y competiciones (Futuro desarrollo)
    └── torneos/    # Gestión de torneos (Futuro desarrollo)

/public/{club}/     # Página pública estilo Playtomic App
├── buscar-partidos/ # Búsqueda y filtrado de partidos disponibles
│   ├── filtros/    # Filtros por fecha, hora, nivel, precio
│   ├── mapa/       # Vista de mapa con ubicaciones de pistas
│   └── lista/      # Lista de partidos con detalles
├── partido/[id]/   # Detalles específicos del partido
│   ├── info/       # Información completa del partido
│   ├── jugadores/  # Lista de jugadores apuntados
│   └── unirse/     # Formulario para unirse al partido
├── mis-partidos/   # Partidos del usuario (requiere login)
├── perfil/         # Perfil público del jugador
└── club-info/      # Información del club
```

## Usabilidad y Aspecto Visual de las Páginas

### Principios Generales de Diseño
- **Responsive Design**: Todas las páginas deben ser completamente responsivas, optimizadas para dispositivos móviles, tablets y desktops, utilizando frameworks como Bootstrap o Tailwind CSS para asegurar una experiencia consistente.
- **Tema Visual**: Colores principales inspirados en el pádel (verde pista, blanco, toques de naranja para acentos). Interfaz limpia, minimalista y moderna, con tipografía sans-serif (ej. Roboto o Open Sans) para legibilidad.
- **Accesibilidad**: Cumplir con estándares WCAG 2.1, incluyendo contraste de colores, navegación por teclado y soporte para lectores de pantalla.
- **Navegación Intuitiva**: Menús claros, breadcrumbs en secciones profundas y búsqueda global para facilitar el acceso rápido a funcionalidades.

### Dashboard Administrativo
- **Usabilidad**: Interfaz intuitiva con navegación lateral persistente, dashboards personalizables con widgets arrastrables y filtros rápidos para datos. Soporte para atajos de teclado en tareas comunes como crear reservas.
- **Aspecto Visual**: Diseño profesional con tarjetas (cards) para métricas, gráficos interactivos (usando Chart.js) y tablas responsivas. Modo oscuro opcional para uso prolongado.

### Página Pública del Club
- **Usabilidad**: Flujo simple para búsqueda y reserva: filtro → lista → detalle → unirse. Integración con login social para registro rápido. Notificaciones en tiempo real para actualizaciones de partidos.
- **Aspecto Visual**: Diseño atractivo y dinámico con imágenes de pistas, mapas interactivos (Google Maps API) y botones prominentes para acciones clave. Animaciones suaves para transiciones y carga de datos.

### Otras Consideraciones
- **Performance**: Carga inicial < 2 segundos, optimización de imágenes y lazy loading.
- **Feedback del Usuario**: Tooltips, mensajes de éxito/error y barras de progreso para operaciones asíncronas.
- **Consistencia**: Elementos UI reutilizables a través de un design system para mantener uniformidad en todas las páginas.

## Funcionalidades Core por Prioridad (Estructura Playtomic Manager)

### Prioridad 1: Métricas y Dashboard Principal (Semanas 1-3)

#### Dashboard de Métricas
- **KPIs principales** (179 partidos, 2.5k ingresos, 2.4k transacciones online, 315 usuarios, 162 nuevos usuarios)
- **Gráficos de barras** para visualización de partidos por día
- **Filtros temporales** (últimas 2 semanas, selecciones personalizadas)
- **Métricas en tiempo real** con actualización automática
- **Comparativas** de rendimiento por períodos

### Prioridad 2: Gestión de Partidos (Semanas 4-5)

#### Sistema de Reservas Avanzado
- **Lista completa de partidos** con filtros múltiples
- **Reservas online y offline** (Bookings Online, Playtomic Matches, Bookings Offline)
- **Calendario visual** con disponibilidad en tiempo real
- **Gestión de estados** (confirmado, pendiente, cancelado)
- **Prevención de dobles reservas** con locking optimista
- **Listas de espera** automáticas

### Prioridad 3: Sistema de Comunicación (Semana 6)

#### Módulo de Chats
- **Chat en tiempo real** con jugadores
- **Notificaciones push** para mensajes importantes
- **Chat grupal** para partidos y eventos
- **Historial de conversaciones** organizado
- **Integración** con reservas y eventos

### Prioridad 4: Página Pública Estilo Playtomic (Semana 7)

#### Interfaz de Búsqueda de Partidos
- **Búsqueda y filtrado** de partidos disponibles por fecha, hora, nivel
- **Vista de mapa** integrada con ubicaciones de pistas
- **Lista detallada** de partidos con información completa
- **Sistema de reservas** público conectado con dashboard
- **Perfiles de jugadores** y sistema de reputación
- **Responsive design** optimizado para móvil (PWA)
- **Configuración de DNS**: Permitir que los clubes apunten sus DNS a esta parte pública del SaaS para una integración de marca sin fricciones.

#### Integración con Módulo de Partidos
- **Sincronización en tiempo real** con dashboard administrativo
- **API compartida** entre interfaz pública y administrativa
- **Notificaciones** automáticas de nuevos partidos
- **Sistema de pagos** integrado para reservas públicas

### Prioridad 5: Facturación y Configuración (Semana 8)

#### Sistema de Facturación
- **Generación automática** de facturas
- **Reportes de ingresos** detallados
- **Integración contable** para exportación
- **Gestión de pagos** pendientes y recordatorios

#### Ajustes del Sistema
- **Configuración del club** (horarios, precios, políticas)
- **Gestión de usuarios** y permisos por rol
- **Configuración de pistas** (indoor/outdoor, mantenimiento)
- **Preferencias del sistema** y notificaciones

### Métricas del Proyecto

#### MVP (Fases 1-7)
- **Tiempo estimado total**: 147-173 horas
- **Duración**: 10 semanas (20 de enero - 7 de marzo 2025)
- **Módulos incluidos**: Métricas, Partidos, Chats, Página Pública Playtomic, Facturación, Configuración

#### Mejoras Futuras (Fase 8)
- **Tiempo estimado**: 147-207 horas
- **Módulos**: Clases, Ligas, Torneos, Plugin WP, Iframe, APP Nativa (planificación/diseño)

#### Total del Proyecto
- **Tiempo total estimado**: 294-380 horas
- **Duración completa**: 13+ semanas (semanas adicionales para las nuevas mejoras)

#### Desglose por Módulo MVP
1. **Arquitectura Base**: 14-18 horas
2. **Métricas y Dashboard**: 22-27 horas
3. **Gestión de Partidos**: 23-28 horas
4. **Sistema de Comunicación**: 20-25 horas
5. **Página Pública Playtomic**: 27-33 horas
6. **Facturación**: 10-12 horas
7. **Configuración**: 6-8 horas
8. **Testing y Deployment**: 23-30 horas

### Fase de Mejoras Futuras (Post-MVP)

#### Clases y Entrenamientos
- **CRUD completo** de clases grupales e individuales
- **Horarios recurrentes** y excepciones
- **Inscripciones** con límites de participantes
- **Gestión de instructores** y asignaciones
- **Sistema de pagos** integrado para clases

#### Ligas y Competiciones
- **Gestión de ligas** con clasificaciones automáticas
- **Inscripciones** con gestión de cupos
- **Seguimiento de resultados** y estadísticas
- **Sistema de premios** y rankings

#### Torneos
- **Creación de torneos** con brackets eliminatorios
- **Gestión de inscripciones** con límites
- **Seguimiento automático** de resultados
- **Sistema de premios** y certificados

#### Integración con Plataformas Externas
- **Plugin WordPress**: Desarrollo de un plugin para incrustar la PWA/SPA o enlazarla fácilmente en sitios de WordPress.
- **Integración vía Iframe**: Documentación y guía para incrustar la PWA/SPA mediante iframe en cualquier sitio web.

#### APP Móvil Nativa
- **Planificación y Diseño**: Definición de alcance, funcionalidades clave, arquitectura inicial y experiencia de usuario para una futura APP móvil nativa (iOS/Android).

## Reglas de Desarrollo Específicas

### REGLA OBLIGATORIA: Gestión de TODO.md

**ANTES DE EMPEZAR CUALQUIER TAREA**:
```markdown
## TODO.md - OBLIGATORIO

SIEMPRE debes guardar la tarea en TODO.md antes de comenzar:

### Formato obligatorio:
- [ ] **[FECHA]** Nombre de la tarea - **Dificultad: [FÁCIL/MEDIO/DIFÍCIL/EXPERTO]**
  - Descripción detallada de la tarea
  - Archivos que se van a modificar/crear
  - Tiempo estimado
  - Dependencias si las hay

### Ejemplo:
- [ ] **[2025-07-17]** Crear dashboard administrativo principal - **Dificultad: MEDIO**
  - Implementar layout con sidebar y header
  - Crear componentes de navegación
  - Integrar con sistema de autenticación
  - Archivos: app/dashboard/, components/layout/
  - Tiempo estimado: 4-6 horas
  - Dependencias: Autenticación configurada
```

**AL FINALIZAR LA TAREA**:
```markdown
OBLIGATORIO marcar como completada:
- [x] **[2025-07-17]** Crear dashboard administrativo principal - **Dificultad: MEDIO** ✅ COMPLETADO
```

**NUNCA OLVIDES**: TODO.md es tu registro de trabajo. Claude Code DEBE mantenerlo actualizado SIEMPRE.

### Workflow de Desarrollo

### Proceso Obligatorio: Explorar → Planificar → Codificar → Confirmar

**1. Explorar**: 
- **PRIMERO**: Guardar tarea en TODO.md con fecha y dificultad
- Lee archivos relevantes ANTES de escribir código
- Entiende el contexto completo del problema
- Identifica dependencias y impactos

**2. Planificar**:
- Usa "think" para activar pensamiento extendido
- Crea plan detallado antes de implementar
- Considera edge cases y validaciones

**3. Codificar**:
- Implementa siguiendo patrones establecidos
- Verifica razonabilidad durante implementación
- Incluye tests unitarios/integración

**4. Confirmar**:
- Ejecuta tests antes de commit
- Actualiza documentación si es necesario
- **OBLIGATORIO**: Marcar tarea como completada en TODO.md
- Crea PR con descripción clara

### Comandos de Validación

Antes de considerar completada cualquier tarea:

```bash
# Validación rápida
npm run lint
npm run type-check
npm run test:unit

# Validación completa
npm run test:integration
npm run test:e2e:critical
npm run build
```

## Patrones de Código Específicos

### Estructura de Dominios (Playtomic Manager)

```typescript
// Organización por dominio de negocio - Estructura Playtomic
domains/
├── metrics/            # Dashboard de métricas y KPIs
│   ├── services/       # Cálculos de métricas en tiempo real
│   ├── repositories/   # Acceso a datos de analytics
│   ├── types/          # Tipos para métricas y reportes
│   └── validators/     # Validaciones de filtros y períodos
├── matches/            # Gestión de partidos (bookings)
│   ├── services/       # Lógica de reservas y disponibilidad
│   ├── repositories/   # Acceso a datos de partidos
│   ├── types/          # Tipos de reservas y estados
│   └── validators/     # Validaciones de reservas
├── chats/              # Sistema de mensajería
│   ├── services/       # WebSocket y notificaciones
│   ├── repositories/   # Historial de mensajes
│   ├── types/          # Tipos de mensajes y chats
│   └── validators/     # Validaciones de contenido
├── classes/            # Gestión de clases y entrenamientos
│   ├── services/       # Programación e inscripciones
│   ├── repositories/   # Datos de clases e instructores
│   ├── types/          # Tipos de clases y horarios
│   └── validators/     # Validaciones de clases
├── leagues/            # Organización de ligas
│   ├── services/       # Clasificaciones y enfrentamientos
│   ├── repositories/   # Datos de ligas y resultados
│   ├── types/          # Tipos de competiciones
│   └── validators/     # Validaciones de torneos
├── tournaments/        # Gestión de torneos
│   ├── services/       # Brackets y eliminatorias
│   ├── repositories/   # Datos de torneos
│   ├── types/          # Tipos de torneos
│   └── validators/     # Validaciones de inscripciones
├── billing/            # Facturación y pagos
│   ├── services/       # Generación de facturas
│   ├── repositories/   # Datos financieros
│   ├── types/          # Tipos de facturación
│   └── validators/     # Validaciones de pagos
├── settings/           # Configuración del sistema
│   ├── services/       # Gestión de configuraciones
│   ├── repositories/   # Preferencias del club
│   ├── types/          # Tipos de configuración
│   └── validators/     # Validaciones de ajustes
└── public/             # Interfaz pública estilo Playtomic
    ├── services/       # Búsqueda y filtrado de partidos
    ├── repositories/   # Acceso a datos públicos
    ├── types/          # Tipos para interfaz pública
    └── validators/     # Validaciones de reservas públicas
```

### Componentes React para Dashboard

```typescript
// Patrón estándar para componentes administrativos
// components/dashboard/[module]/[Component].tsx

interface ComponentProps {
  // Props específicas
  clubId: string;
  onAction?: (data: ActionData) => void;
  // Props comunes
  className?: string;
  loading?: boolean;
}

export const Component: React.FC<ComponentProps> = ({
  clubId,
  onAction,
  className = '',
  loading = false
}) => {
  // Lógica del componente
  return (
    <div className={`dashboard-component ${className}`}>
      {/* Contenido */}
    </div>
  );
};
```

### APIs para Gestión de Clubes

```typescript
// Patrón estándar para APIs administrativas
// app/api/admin/[resource]/route.ts

export async function GET(request: NextRequest) {
  try {
    // 1. Verificar autenticación de administrador
    const session = await getAdminSession();
    if (!session) return unauthorized();

    // 2. Validar permisos del club
    const clubId = request.nextUrl.searchParams.get('clubId');
    await validateClubAccess(session.user.id, clubId);

    // 3. Ejecutar lógica de negocio
    const service = new ResourceService();
    const result = await service.getResources(clubId);

    // 4. Respuesta estructurada
    return NextResponse.json({
      success: true,
      data: result,
      meta: { timestamp: new Date().toISOString() }
    });

  } catch (error) {
    return handleApiError(error);
  }
}
```

## Consideraciones Específicas del Negocio

### Modelo Multi-Tenant

**Cada club es un tenant independiente**:
- Datos completamente aislados entre clubes
- Configuración personalizada por club
- Facturación independiente por club
- Subdominios opcionales por club

### Roles y Permisos

```typescript
enum UserRole {
  SUPER_ADMIN = 'super_admin',    // Administrador de la plataforma
  CLUB_OWNER = 'club_owner',      // Propietario del club
  CLUB_ADMIN = 'club_admin',      // Administrador del club
  CLUB_STAFF = 'club_staff',      // Personal del club
  CLUB_MEMBER = 'club_member'     // Socio del club (solo página pública)
}

// Permisos por rol
const PERMISSIONS = {
  [UserRole.SUPER_ADMIN]: ['*'], // Todos los permisos
  [UserRole.CLUB_OWNER]: [
    'club:read', 'club:write', 'club:delete',
    'analytics:read', 'billing:read', 'staff:manage'
  ],
  [UserRole.CLUB_ADMIN]: [
    'club:read', 'club:write',
    'bookings:manage', 'members:manage', 'analytics:read'
  ],
  [UserRole.CLUB_STAFF]: [
    'bookings:create', 'bookings:read', 'members:read'
  ],
  [UserRole.CLUB_MEMBER]: [
    'public:read', 'booking:create' // Solo página pública
  ]
};
```

### Flujos de Negocio Críticos

#### 1. Onboarding de Nuevo Club

```typescript
// Flujo completo de alta de club
async function onboardNewClub(clubData: CreateClubData) {
  // 1. Crear club en base de datos
  const club = await createClub(clubData);
  
  // 2. Configurar pistas por defecto
  await createDefaultCourts(club.id);
  
  // 3. Configurar horarios estándar
  await setupDefaultSchedule(club.id);
  
  // 4. Crear usuario administrador
  await createClubAdmin(club.id, clubData.adminEmail);
  
  // 5. Configurar página pública
  await setupPublicPage(club.id);
  
  // 6. Enviar email de bienvenida
  await sendWelcomeEmail(clubData.adminEmail);
  
  return club;
}
```

#### 2. Gestión de Reservas Diarias

```typescript
// Flujo típico del personal del club
async function createBookingFromPhone(bookingData: PhoneBookingData) {
  // 1. Verificar disponibilidad en tiempo real
  const availability = await checkAvailability(
    bookingData.courtId, 
    bookingData.startTime
  );
  
  // 2. Crear reserva temporal (5 min TTL)
  const tempBooking = await createTemporaryBooking(bookingData);
  
  // 3. Procesar pago si es necesario
  if (bookingData.paymentRequired) {
    await processPayment(tempBooking.id, bookingData.paymentData);
  }
  
  // 4. Confirmar reserva definitiva
  const booking = await confirmBooking(tempBooking.id);
  
  // 5. Notificar al cliente
  await sendBookingConfirmation(booking);
  
  return booking;
}
```

### Métricas Específicas del Dashboard

```typescript
// Métricas clave para administradores de clubes
interface ClubMetrics {
  // Ocupación
  occupancyRate: {
    today: number;
    thisWeek: number;
    thisMonth: number;
  };
  
  // Ingresos
  revenue: {
    today: number;
    thisWeek: number;
    thisMonth: number;
    comparison: {
      previousWeek: number;
      previousMonth: number;
    };
  };
  
  // Miembros
  members: {
    total: number;
    active: number;
    newThisMonth: number;
    renewalsDue: number;
  };
  
  // Pistas
  courts: {
    total: number;
    active: number;
    maintenance: number;
    mostPopular: string;
  };
}
```

## Integraciones Críticas

### Sistema de Pagos (Stripe)

**Para clubes que cobran online**:
- Integración completa con Stripe Connect
- Pagos directos al club (no a la plataforma)
- Comisión de la plataforma como application fee
- Gestión de reembolsos automática

### Comunicaciones (SendGrid + WhatsApp)

**Para notificaciones automáticas**:
- Confirmaciones de reserva por email
- Recordatorios por WhatsApp
- Comunicaciones masivas a socios
- Alertas al personal del club

### Análisis (Google Analytics + Custom)

**Para insights del negocio**:
- Tracking de uso del dashboard
- Análisis de la página pública
- Métricas personalizadas del club
- Reportes automáticos mensuales

## Consideraciones de Escalabilidad

### Arquitectura Multi-Tenant

**Aislamiento de datos por club**:
```sql
-- Todas las tablas incluyen club_id
CREATE TABLE bookings (
  id UUID PRIMARY KEY,
  club_id UUID NOT NULL REFERENCES clubs(id),
  court_id UUID NOT NULL,
  -- otros campos
  
  -- Índices optimizados por club
  INDEX idx_bookings_club_date (club_id, booking_date),
  INDEX idx_bookings_club_court (club_id, court_id)
);
```

### Cache Estratégico

**Redis para datos frecuentes**:
- Disponibilidad de pistas por club
- Configuración de precios
- Sesiones de usuario
- Métricas del dashboard

### Monitoreo Específico

**Alertas críticas para el negocio**:
- Dobles reservas (debe ser 0%)
- Tiempo de respuesta del dashboard
- Errores en procesamiento de pagos
- Caídas de disponibilidad por club

## Roadmap de Funcionalidades

### MVP (8 semanas)
1. **Dashboard administrativo básico**
2. **Gestión de clubes y pistas**
3. **Sistema de reservas interno**
4. **Página pública simple**

### V1.0 (16 semanas)
5. **Gestión completa de miembros**
6. **Analytics y reportes**
7. **Integraciones de pago**
8. **Sistema de notificaciones**

### V2.0 (24 semanas)
9. **App móvil para administradores**
10. **Sistema de torneos**
11. **Precios dinámicos automáticos**
12. **Marketplace de profesores**

## Recordatorios Críticos

### Para Claude Code

1. **Enfoque B2B**: Siempre pensar desde la perspectiva del administrador del club
2. **Dashboard primero**: La interfaz administrativa es la funcionalidad principal
3. **Página pública secundaria**: Simple y efectiva, no competir con Playtomic
4. **Gestión de negocio**: Herramientas para optimizar operaciones del club
5. **TODO.md obligatorio**: Nunca empezar sin registrar, nunca terminar sin marcar

### Preguntas de Validación

Antes de implementar cualquier funcionalidad, pregúntate:
- ¿Esto ayuda al administrador del club a gestionar mejor su negocio?
- ¿Es intuitivo para personal no técnico?
- ¿Genera valor medible para el club?
- ¿Está alineado con el modelo B2B?

---

**Recordatorio Final**: PadelClub Manager es una herramienta de gestión para clubes, no una app para jugadores. El éxito se mide por la eficiencia operativa y rentabilidad de los clubes que usan la plataforma.

