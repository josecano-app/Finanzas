# CG Finanzas: contexto para Claude Code

App de finanzas personales en un solo archivo, `index.html`, sin build ni dependencias (solo Google Fonts: Bricolage Grotesque y Figtree). Interfaz en español de Chile, montos en CLP (`Intl.NumberFormat("es-CL")`), pensada primero para iPhone.

## Estructura de `index.html`
- Estado global `S`: `cfg` (configuración y plan), `movs` (gastos por mes `"YYYY-MM" -> [{id, fecha, cat, nota, monto}]`), `tab`, `mes`.
- Guardado: `localStorage` con la clave `plata-de-la-casa-v1` (`saveLocal`, `saveCfg`, `saveMonth`). Si existe `window.claude` (artifact de claude.ai) usa además su `db`; fuera de claude.ai ese bloque no hace nada.
- Cálculo: `simulate(cfg, useAbonos)` proyecta mes a mes los créditos en cuotas (interés = saldo × tasa mensual; en el mes `fin` se paga el saldo completo); `monthPlan` arma lo que entra y sale en un mes; `cashPath` acumula el saldo de la cuenta.
- Vistas: `inicioView`, `anotarView`, `deudasView`, `planView`; los eventos se conectan en `bind()`.

## Modelo de `cfg`
- `ingresos[]`, `fijos[]`: `{id, n, m, dia?, desde?, hasta?}` (meses `"YYYY-MM"`).
- `presupuestos[]`: categorías de gasto diario `{id, n, m}`.
- `deudas[]`: `tipo` = `"cuotas"` (entra en la simulación: `saldo, tasa, cuota, dia, fin`), `"linea"` o `"tarjeta"` (pagos fijados por mes en `pagosMes`).
- `abonos`: `{"YYYY-MM": {idDeuda: monto}}`. `pagos`: checks del mes `{"YYYY-MM": {idItem: true}}`.
- `planDesde`, `saldoCuenta {mes, monto}`, `colchon`.

## Reglas
- No subir `plan-inicial.js` ni respaldos JSON: contienen datos financieros reales.
- Mantener todo en un archivo y que funcione abriéndolo con un servidor estático.
- Si cambias archivos cacheados, sube la versión de `CACHE` en `sw.js`.
