# CLAUDE.md — Mi Vida en Orden (`app_personal`)

> Archivo de contexto para Claude Code. Léelo completo antes de tocar el código.
> App de tracking personal multi-ámbito de Juan. Producción: https://juanguzman2.github.io/app_personal/

---

## 1. Qué es este proyecto

App PWA personal de un solo usuario para llevar orden en varios ámbitos de la vida.
**7 secciones** en el bottom-nav: `inicio` 🏠 · `comida` 📖 · `crono` 🗓️ · `finanzas` 💰 · `gym` 🏋️ · `ingles` 📕 · `desarrollo` 🌱 ("Crecer").
Es de uso privado (no multiusuario, no backend).

Filosofía de producto: **registro mínimo, máxima automatización**. Cada feature debe reducir fricción, no añadirla.

## 2. Stack y arquitectura

- **Un solo archivo:** todo vive en `index.html` (~3000 líneas). No hay `src/`, ni módulos.
- **React 18 vía UMD + Babel Standalone** por CDN. JSX compilado **en el navegador** dentro de
  `<script type="text/babel" data-presets="react">`. Sin build, sin bundler, sin npm.
- **Sin dependencias instalables.** Si necesitas una librería, solo por `<script src="cdnjs...">` (evítalo).
- **Persistencia:** `localStorage`, prefijo `mvo_`, vía helpers `load(key, fallback)` / `save(key, value)`.
  Al arrancar se pide `navigator.storage.persist()`.
- **PWA:** `manifest.webmanifest`, mobile-first (iPhone), viewport bloqueado.
- **Deploy:** GitHub Pages desde **`master`**. Commit → push = deploy. Sin CI.
  **Flujo acordado con el dueño: trabajar directo sobre master y hacer push sin PR ni revisión.**
- **Service worker (`service-worker.js`):** **network-first para `index.html`** (los cambios llegan solos,
  NO hace falta subir la versión del caché al editar la app) y cache-first para CDN/imagen/íconos.
  Solo sube `CACHE = "mvo-vXX"` si cambias la lista `ASSETS` (CDN, imágenes nuevas).

### Restricciones que NO debes romper
1. **Archivo único.** Nada de bundlers ni ESM. Organiza con comentarios `/* ═══ SECCIÓN ═══ */`.
2. **Claves `mvo_` + helpers `load`/`save`** siempre.
3. **Compatibilidad hacia atrás:** hay datos reales. Campos nuevos con **default** (`x.campo ?? []`).
   Nunca renombres una clave `mvo_` sin migrar.
4. **Dinero siempre `es-CO`** vía `money()` / `moneyShort()`.
5. **Estética:** paleta `C`, fuentes `SERIF`/`SANS`, componentes `Card`/`Sheet`/`Segmented`/`Bar`/`Field`/`Chip`/`Header`/`Mini`/`Toast`. Sin Tailwind ni CSS frameworks.
6. **`pedirConfirm({titulo,texto})`** antes de borrar cualquier cosa.
7. **Idioma UI: español (es-CO)** — excepto la sección Inglés, que es 100% en inglés.

## 3. Patrón de estado (componente raíz `App`)

Cada entidad se registra en **5 puntos**: (1) `useState`, (2) línea de carga en el `useEffect` de
hidratación, (3) `useEffect` de guardado con flag `ready`, (4) objeto `datos` (export), (5) objeto `setters` (import).
Si falta alguno se rompe el respaldo export/import de Ajustes (⚙ en Inicio).

### Helpers clave (reutilízalos)
`uid()` · `num()` · `money()` · `moneyShort()` · fechas: `HOY`, `fechaLocal`, `mesDe`, `MES_ACTUAL`,
`nombreMes`, `mesAdj`, `mesesHasta`, `mesesDesde`, `diasHasta` (negativo si pasó), `fechaLarga`,
`ultimos7`, `ultimosN`, `DIA_CORTO`, `lunesDe`, `semanaLunDom`, `DIAS_SEM`, `diaHoyNombre`,
`hhmmToMin`, `minNow` · gym: `e1rm` (Epley), `musculoDe`, `volumen` · noti/audio: `notiAhora`, `notiProgramar`, `beep`.

## 4. Mapa de entidades (claves `mvo_…`)

| Sección | Entidades |
|---|---|
| Comida | `recetas`, `consumo`, `quemadas`, `limites`, `lotes` (nevera), `lista` (mercado, sub-tab de Comida), `seguimiento` (corporal), `perfil` |
| Finanzas | `transacciones`, `fijos`, `inversiones` (con `portafolio`/`fondoId` opcionales), `metas`, `provisiones`, `presupuesto`, `finanzasCfg` (con `trmAuto`/`trmFecha`), `finPlan` (portafolios P1/P2, maestría, reglas, hitos; seed `SEED_FIN_PLAN`), `finAportes` (log, máx. 500), `finPatrimonio` (snapshot mensual, máx. 24), `finRitual` (checklist mensual) |
| Gym | `entrenos`, `plantillas` (plan editable) |
| Cronograma | `horario` (bloques con `gid` multi-día), `sprints` (macrotareas con `ambito` laboral/personal), `notas`, `pomoCfg`, `rutinaHecha`, `habitos`, `habitosLog`, `cuentasReg` (cuentas regresivas), `bitacora` (actividades ejecutadas), `bitacoraCfg` (meta semanal de foco), `bitacoraTimer` (timer en curso; transiente, fuera del respaldo) |
| Inglés | `inglesSR` (estado SM-2 por tarjeta), `inglesCustom` (palabras propias del usuario) |
| Crecer | `dpGratitud`, `dpAfirmaciones`, `dpVizLog`, `dpMetas` (12 pasos), `dpRueda` |
| Meta | `lastExport` (fecha del último respaldo), `guias` (legado sin UI, conservada por compatibilidad) |

Patrones que se repiten (reúsalos):
- **Marcar algo crea/borra una transacción**: fijos → `transacciones` (`id="fijo-"+f.id+"-"+ym`, `_fijo`); fondos → `_fondo`.
- **Hábito vinculado a bloque del horario**: marcar el bloque en `rutinaHecha` cumple el hábito (`habitoCumplido`).
- **Formularios en `<Sheet>`** con objeto `_nuevo` y `guardar`/`eliminar`.

## 5. Secciones (resumen de comportamiento)

- **Inicio:** héroe (Asta/Black Clover, `FRASES`), efectivo + mes, meta financiera más próxima, rutina de hoy
  (bloques marcables), hábitos de hoy, repaso de inglés pendiente, cuentas regresivas, nevera (lotes),
  aviso de respaldo si >30 días. Ajustes (⚙) = export/import JSON.
- **Comida:** Recetas (pasos + modo cocina + lotes) · Diario (kcal/macros, balanza semanal) ·
  Seguimiento (peso, pliegues Jackson-Pollock 3 `grasaJP3`, proyección) · Mercado (lista de compras).
- **Cronograma:** Estudio (calendario semanal de bloques multi-día + pomodoro + avisos) ·
  Trabajo (sprints/macrotareas con ámbito 💼/🚀 + filtros, notas; los sprints **planifican**) ·
  Hábitos (CRUD, rachas, heatmap 30 días, "refuerza estos", cuentas regresivas) ·
  Bitácora (**registra lo ejecutado**: registro rápido con ámbito/duración/foco/distracciones,
  resumen semanal lun–dom con foco profundo vs meta editable, barras por ámbito, racha, alerta de
  descarga <70% × 2 semanas, modo enfoque con timer persistente, ▶ en tareas de sprint → entrada
  vinculada con `tareaRef` + marcar tarea completada).
- **Finanzas:** Resumen (balance, tasa de ahorro, patrimonio 12m, chip del ritual, cascada
  fijos→metas→provisión→disponible, fijos, presupuesto, gráfica 6 meses, movimientos) ·
  Inversión (TRM automática con semáforo verde/neutro/stop, inversiones agrupadas por portafolio
  P1/P2/Otras con real% vs target% y chips de drift, sugerencia del próximo aporte, fondos/provisiones) ·
  Plan (💸 Día de pago que reparte salario por targets DCA y prima/bono con waterfall
  maestría→P1 + resto→P2 en tramos, ritual mensual con racha, portafolios del plan con
  vinculación fondo↔inversión, hitos countdown, reglas de oro) · Metas (prioridad, en ruta, USD).
  El día de pago crea la transacción de ingreso con id determinístico `salario-YYYY-MM` (no duplica).
- **Gym:** Entrenos (plantillas Upper/Lower 5 días, "última vez" con todas las series, toast de PR,
  series/músculo vs MEV-MAV) · Plan (editable, restaurable) · Progreso (1RM est./peso/volumen por ejercicio).
- **Inglés (todo en inglés):** mazos IELTS Vocabulary (548+) y Grammar (46) con SM-2; 15 nuevas/día
  (+15 opcionales), filtro por tema (select o tap en "Progress by topic"), "Tomorrow: N due",
  **My words**: el usuario agrega sus propias palabras (`inglesCustom`) → 2 tarjetas c/u.
- **Crecer (Desarrollo Personal, Brian Tracy/Seminario Fénix):** Teoría (acordeón estático `TEORIA_BT`) ·
  Práctica (gratitud + afirmaciones + visualización guiada con log) · Metas (12 pasos, 7 `AREAS_VIDA`,
  Propósito Mayor, Rueda de la Vida) · Mi Año (estático `MI_ANO`).

## 6. Acuerdos de trabajo para Claude Code

- **Trabaja directo en master y haz push** al terminar (acordado con el dueño; no crear PRs).
  Antes de commitear: `git stash push -- .claude/settings.local.json`, commit, `git stash pop`.
- **Confirma alcance** con el usuario si hay ambigüedad en una feature nueva.
- **Migraciones primero** si tocas esquema (defaults + tolerancia a registros viejos).
- **Prueba siempre** en el preview (crear, editar, borrar, navegar, exportar/importar) y limpia los
  datos de prueba del localStorage antes de terminar.
- **No subas la versión del SW por cambios en `index.html`** (network-first se encarga); solo si cambias `ASSETS`.
- **Comenta cada bloque nuevo** con separador y registra entidades nuevas en los 5 puntos.
