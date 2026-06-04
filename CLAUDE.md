# CLAUDE.md — Mi Vida en Orden (`app_personal`)

> Archivo de contexto para Claude Code. Léelo completo antes de tocar el código.
> App de tracking personal multi-ámbito de Juan. Producción: https://juanguzman2.github.io/app_personal/

---

## 1. Qué es este proyecto

App PWA personal de un solo usuario para llevar orden en varios ámbitos de la vida:
**Inicio, Comida, Cronograma, Finanzas, Gym, Lista**. Es de uso privado (no multiusuario, no backend).
El foco de trabajo actual es **rediseñar la sección Finanzas** (ver §7).

Filosofía de producto: **registro mínimo, máxima automatización**. El dueño quiere
poca interacción manual; cada feature debe reducir fricción, no añadirla.

---

## 2. Stack y arquitectura

- **Un solo archivo:** todo vive en `index.html` (~1950 líneas). No hay carpetas `src/`, ni módulos.
- **React 18 vía UMD + Babel Standalone** cargados por CDN. El JSX se compila **en el navegador**
  dentro de `<script type="text/babel" data-presets="react">`. No hay paso de build, ni bundler, ni npm.
- **Sin dependencias instalables.** No `package.json`, no `node_modules`. Si necesitas una librería,
  se agrega por `<script src="cdnjs...">` en el `<head>` (evítalo salvo que sea imprescindible).
- **Persistencia:** `localStorage`, una clave por entidad, todas con prefijo `mvo_`.
  Helpers `load(key, fallback)` / `save(key, value)` (async, envuelven `localStorage`).
- **PWA:** `manifest.webmanifest`, `icon-192.png`, `apple-touch-icon`, `theme-color #2c2415`,
  viewport bloqueado (sin zoom). Pensada **mobile-first** (iPhone, instalable en home screen).
- **Deploy:** GitHub Pages desde la rama **`master`**. Editar `index.html` → commit → push = deploy.
  No hay CI. Para probar localmente basta abrir `index.html` en el navegador (o `python -m http.server`).

### Restricciones que NO debes romper
1. **Mantén el patrón de archivo único.** No introduzcas un bundler ni dividas en módulos ESM
   (Babel standalone no resuelve `import`). Si el archivo crece mucho, organiza con comentarios de sección
   (`/* ═══ FINANZAS ═══ */`), no con archivos nuevos.
2. **No uses `localStorage`/`sessionStorage` con claves fuera del prefijo `mvo_`** ni saltes los helpers `load`/`save`.
3. **Compatibilidad hacia atrás:** ya hay datos reales guardados. Cualquier campo nuevo en una entidad
   debe tener **default** y tolerar registros viejos sin ese campo (ver §6.1 Migraciones).
4. **Formato de dinero siempre `es-CO`** vía el helper `money()` (no `toLocaleString` suelto).
5. **Estética:** respeta la paleta `C`, las fuentes `SERIF`/`SANS` y los componentes existentes
   (`Card`, `Sheet`, `Segmented`, `Bar`, `Field`, `Chip`, `Header`). No metas Tailwind ni CSS frameworks.

---

## 3. Convenciones de código

### Paleta y tipografía
```js
const C = { bg, card, espresso, gold, goldSoft, border, borderSoft, muted, text,
            green, greenSoft, red, redSoft, blue, blueSoft, purple, purpleSoft };
const SERIF = "Georgia,'Times New Roman',serif";   // títulos, montos
const SANS  = "system-ui,-apple-system,sans-serif"; // texto UI
```
Convención de color: verde = positivo/ingreso/logrado, rojo = gasto/negativo,
dorado (`gold`) = acción/acento, `muted` = secundario.

### Helpers existentes (reutilízalos, no los redefinas)
- `uid()` → id corto aleatorio.
- `num(n)` → `Number(n)||0` (los montos vienen como string desde inputs; normaliza SIEMPRE con `num`).
- `money(n)` → `"$1.234.567"` formato es-CO. `moneyShort(n)` → `"$1.2M"` / `"$45k"`.
- Fechas: `fechaLocal(d)` (YYYY-MM-DD local), `HOY`, `mesDe(f)` (YYYY-MM), `MES_ACTUAL`,
  `nombreMes(ym)`, `mesAdj(ym, ±n)`, `mesesHasta(fecha)`, `ultimos7()`, `DIA_CORTO(f)`, `lunesDe(d)`.

### Componentes UI reutilizables
- `<Header titulo="…"/>` — encabezado de sección.
- `<Segmented value onChange options=[{id,label}]/>` — tabs (las usa cada sección).
- `<Card pad={n}>…</Card>` — tarjeta blanca con borde.
- `<Sheet open onClose title>…</Sheet>` — bottom sheet modal para formularios.
- `<Bar pct color h/>` — barra de progreso.
- `<Field label>…</Field>` — wrapper de campo de formulario.
- `<Chip bg col>…</Chip>` — etiqueta pequeña.
- `await pedirConfirm({titulo, texto})` — diálogo de confirmación (úsalo antes de borrar).
- Estilos compartidos: `inputStyle`, `labelStyle`, `navMesBtn`, `btnP(ok)` (botón primario), `btnDel(fn)` (borrar).

### Patrón de estado (componente raíz)
Todo el estado vive en el componente raíz y se hidrata en un `useEffect` inicial. Para cada entidad hay:
- un `useState`,
- una línea de carga en el `useEffect` de hidratación (`setX(await load("x", default))`),
- un `useEffect` de guardado (`useEffect(()=>{if(ready)save("x",x)},[x,ready])`),
- entrada en los objetos `datos` (export) y `setters`.

**El flag `ready`** evita que el primer render (estado vacío) sobrescriba lo guardado.
Cualquier entidad nueva debe registrarse en los 4 puntos anteriores **y** en `datos`/`setters`
para que entre al respaldo export/import.

### Backup
`exportar()` descarga `mi-vida-en-orden-{HOY}.json` con todo `datos`. `importar(ev)` lo restaura.
Si agregas entidades, quedan incluidas automáticamente si están en `datos`/`setters`.

---

## 4. Mapa de secciones (bottom nav)
`inicio` 🏠 · `comida` 📖 · `crono` 🗓️ · `finanzas` 💰 · `gym` 🏋️ · `lista` 🛒
Cada una es un componente que recibe props (estado + setters) desde la raíz.

---

## 5. Categorías (constantes globales)
```js
CAT_GASTO   = ["🍽️ Alimentación","🛒 Mercado","🏠 Vivienda","🚗 Transporte","🎓 Educación",
               "🎉 Ocio","💊 Salud","💡 Servicios","💳 Deudas","🛍️ Compras","📦 Otros"];
CAT_INGRESO = ["💼 Salario","💵 Freelance","🎁 Extra","📈 Rendimientos","📦 Otros"];
```

---

## 6. Modelo de datos — Finanzas (estado actual)

| Entidad (clave `mvo_…`) | Forma |
|---|---|
| `transacciones` | `{ id, tipo:"ingreso"\|"gasto", categoria, concepto, monto, fecha, _fijo? }` |
| `fijos` | `{ id, nombre, monto, categoria, pagos:{ [ym]: boolean } }` |
| `inversiones` | `{ id, nombre, invertido, actual }` |
| `metas` | `{ id, nombre, objetivo, actual, fecha, inversionId? }` |

Componente `Finanzas` → tabs `Segmented`: **Mes** (`mov`) · **Fijos** (`fijos`) · **Inversión** (`inv`) · **Metas** (`metas`).

Comportamiento actual relevante:
- **Mes:** lista transacciones del mes, balance ingreso/gasto, desglose por categoría. Navegación por mes.
- **Fijos:** lista de gastos recurrentes. Marcar "pagado" en un mes **crea automáticamente** una transacción
  de gasto (`id = "fijo-"+f.id+"-"+ym`, con `_fijo`). Desmarcar la borra. (Buen patrón: reúsalo.)
- **Inversión:** portafolio con `invertido` vs `actual`, % de rendimiento. "Aportar" suma a ambos campos.
- **Metas:** objetivo/actual/fecha, barra de progreso, calcula "ahorra al mes" = faltante / meses restantes.
  Puede vincularse a una inversión (`inversionId`); entonces su avance = `actual` de esa inversión.

### 6.1 Migraciones (IMPORTANTE)
No hay sistema de versiones de esquema. Al añadir campos:
- Da **defaults** al leer (`const provs = m.provisiones ?? []`).
- Para datos nuevos, calcula al vuelo o haz una migración idempotente en la hidratación
  (un helper `migrar(datos)` que rellene campos faltantes una sola vez y vuelva a `save`).
- Nunca renombres una clave `mvo_` existente sin migrar primero (perderías datos del usuario).

---

## 7. REDISEÑO DE FINANZAS — objetivo y especificación

### 7.1 El problema con el diseño actual
Hoy Finanzas es un **libro contable reactivo**: registras lo que ya gastaste. Las buenas finanzas
personales son **proactivas**: planeas (presupuesto), apartas para gastos irregulares (provisiones),
te pagas primero (ahorro automático antes del gasto), y mides progreso hacia metas y patrimonio.

### 7.2 Modelo central: la "cascada del dinero"
Toda la sección debe girar en torno a este orden de asignación del ingreso del mes:

```
INGRESO DEL MES
  ├─ 1. Fijos            (arriendo, servicios, suscripciones)        ← ya existe
  ├─ 2. Provisiones      (1/12 de gastos anuales: SOAT, seguro,      ← NUEVO (mayor impacto)
  │                       mantenimiento carro, declaración de renta)
  ├─ 3. Ahorro / Metas   (PÁGATE PRIMERO: F. emergencia → máster →   ← mejorar
  │                       finca). Objetivo: tasa de ahorro ≥ 40%.
  └─ 4. Variable         (lo que queda = "disponible para gastar")    ← mejorar con presupuesto
```
La UI debe hacer visible y, donde se pueda, **automática** esta cascada.

### 7.3 KPIs a exponer (principios de finanzas personales aplicados)
- **Tasa de ahorro del mes** = (ingreso − gasto) / ingreso. KPI #1 para alguien con ingresos altos.
- **Patrimonio neto** = activos (cuentas + inversiones + carro) − pasivos (deudas; hoy 0).
- **Fondo de emergencia:** cuántos **meses de gastos** cubre (meta: 10M ≈ 5–6 meses).
- **Disponible para gastar este mes** (runway) = ingreso − fijos − provisión mensual − aporte a metas.
- **Progreso ponderado de metas** y si cada una va **"en ruta"**.

---

## 8. Especificación por fases (implementables en orden)

> Cada fase es un PR independiente. Respeta §2 (restricciones) y §6.1 (migraciones).

### FASE 1 — Provisiones / Fondos para gastos anuales  ⭐ (máxima prioridad)
**Por qué:** hay gastos irregulares grandes (SOAT, seguro todo riesgo del Mazda 2, mantenimiento,
impuesto vehicular, **declaración de renta**) que hoy "explotan" el mes en que caen.
La solución experta es apartar **1/12 cada mes**.

Nueva entidad `provisiones` (clave `mvo_provisiones`):
```js
{ id, nombre, categoria, montoAnual, mesVencimiento /* 1-12 o null */,
  saldo /* acumulado */, _historial?: [{fecha, tipo:"aporte"|"uso", monto}] }
```
Lógica:
- `provisionMensual = montoAnual / 12` (o `/ mesesHasta(vencimiento)` si está cerca).
- Botón "Apartar este mes" (o auto-aporte mensual) suma `provisionMensual` al `saldo`.
- Al ocurrir el gasto: "Usar fondo" descuenta del `saldo` y **crea una transacción** de gasto
  (reusa el patrón de `fijos` → `transacciones`).
- Vista: total a provisionar/mes, saldo por fondo, alerta si un vencimiento se acerca y el saldo no alcanza.

Defaults sugeridos para sembrar (editables; **montos a confirmar con el usuario**):
SOAT, Seguro todo riesgo (carro), Mantenimiento Mazda 2, Impuesto vehicular,
Declaración de renta, Regalos/Navidad.

### FASE 2 — Presupuesto por categoría + Tasa de ahorro
- Nueva entidad `presupuesto` (clave `mvo_presupuesto`): `{ [categoria]: montoPlaneado }`
  (o por mes: `{ [ym]: { [categoria]: monto } }` con fallback al plan base).
- En la tab **Mes**: por cada categoría mostrar **planeado vs real** con `<Bar>` y color
  (verde < 80%, dorado 80–100%, rojo > 100%).
- Mostrar **tasa de ahorro del mes** arriba, con meta configurable (default 40%).
- Método a documentar en la UI: presupuesto base-cero adaptado a ingresos variables
  (cada peso tiene un trabajo asignado).

### FASE 3 — Dashboard "Resumen" + Patrimonio neto
- Nueva tab inicial **Resumen** (primer `Segmented`), dashboard de una mirada:
  patrimonio neto y su variación, tasa de ahorro, estado del fondo de emergencia (meses cubiertos),
  disponible para gastar, y metas en miniatura.
- Nueva entidad `activos` (clave `mvo_activos`): `{ id, nombre, tipo:"cuenta"|"activo"|"deuda", valor }`
  para capturar saldos bancarios y el carro. **Patrimonio neto** = Σactivos + Σ`inversiones.actual` − Σdeudas.
- **Snapshots mensuales** de patrimonio (`mvo_patrimonioHist: [{ym, valor}]`) para graficar evolución
  (reusa el patrón de gráfico de barras de la sección Gym).

### FASE 4 — Metas mejoradas + ingresos extraordinarios
- **Orden de prioridad** entre metas (campo `prioridad` o reordenar): financiar en secuencia
  Fondo de emergencia → Máster → Finca.
- **Indicador "en ruta":** comparar aporte mensual requerido vs aportes reales recientes;
  mostrar **fecha proyectada** de cumplimiento y semáforo (en ruta / atrasada).
- **Meta multimoneda** (máster en USD): permitir nota de moneda/objetivo en USD y, opcional,
  campo TRM de referencia para estimar el costo en COP.
- **Ingresos extraordinarios** (primas, bonos): al registrar un ingreso grande, ofrecer un
  **reparto sugerido** (ej. % a meta prioritaria / % a finca / % libre) y aplicarlo con un toque.
  Esto operacionaliza la disciplina con dinero "lumpy".

---

## 9. Contexto financiero del dueño (úsalo como defaults/validaciones)

> Parámetros reales para diseñar features y sembrar valores por defecto. **Confirmar con el usuario**;
> los montos de provisiones son estimados.

**Ingresos (COP):** estructura de ~18 salarios/año. Salario base ~5.6M/mes; primas (jun y dic),
prima de vacaciones y bonos; total bruto anual ≈ 109M. Ingreso **irregular**: el grueso del ahorro
sale de primas y bonos → la Fase 4 (ingresos extraordinarios) es importante.

**Gastos:** fijos ~1M/mes + irregulares (carro Mazda 2 2022: SOAT, seguro, mantenimiento, impuesto;
declaración de renta). Sin deudas.

**Metas (en este orden de prioridad):**
1. **Fondo de emergencia: 10M COP** (líquido, ~5–6 meses de gastos). Llenar primero.
2. **Maestría (UT Austin, virtual): ~10.000 USD**, inicio ~mediados de **2027**. Pasivo en dólares →
   considerar meta en USD.
3. **Finca: 300–400M COP**, horizonte ~5 años (~2031). Meta grande y exigente.

**Objetivo de comportamiento:** tasa de ahorro alta (≥40%), automatización máxima, mínima interacción.
La app debe reforzar: págate primero, provisiona lo irregular, no dejes saldos ociosos, mide patrimonio.

> Nota: no asumir productos de inversión ni beneficios tributarios (AFC / crédito de vivienda) por defecto;
> una finca de recreo normalmente NO califica como vivienda de habitación. Dejar esos supuestos al usuario.

---

## 10. Acuerdos de trabajo para Claude Code

- **Antes de codear una fase:** confirma el alcance y el modelo de datos con el usuario si hay ambigüedad.
- **Una fase = un cambio coherente.** No mezcles fases en el mismo PR.
- **Migraciones primero:** si tocas el esquema de una entidad existente, asegura defaults y prueba con
  un backup `.json` real importado.
- **Prueba siempre** abriendo `index.html` en el navegador (móvil idealmente). No hay tests automáticos;
  verifica manualmente: crear, editar, borrar, navegar meses, exportar/importar.
- **Mantén el estilo:** paleta `C`, `SERIF`/`SANS`, componentes `Card`/`Sheet`/`Segmented`/`Bar`/`Field`,
  `money()` para todo monto, `pedirConfirm` antes de borrar.
- **No agregues dependencias** salvo acuerdo explícito (y solo por CDN).
- **Comenta cada bloque nuevo** con un separador de sección y deja la entidad registrada en
  estado + hidratación + guardado + `datos` + `setters`.
- **Idioma de la UI: español** (es-CO).
