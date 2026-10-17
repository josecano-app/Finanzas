# CG Finanzas

App web (PWA) de finanzas familiares: presupuesto del mes, registro de gastos, pagos del mes y plan para salir de deudas con abonos extra.

## Archivos

- `index.html`: toda la app (HTML, CSS y JavaScript en un solo archivo).
- `manifest.webmanifest`, `icons/`: nombre e ícono al instalarla en el celular.
- `sw.js`: permite abrirla sin conexión.
- `plan-inicial.js`: datos iniciales (ingresos, cuentas, deudas, abonos). **Es personal y está en `.gitignore`.**
- `plan-inicial.ejemplo.js`: plantilla del formato.

## Probar en el computador

```bash
python3 -m http.server 8080
# abrir http://localhost:8080
```

## Publicar (GitHub Pages)

1. Sube el repositorio a GitHub (de preferencia **privado**).
2. Settings → Pages → Branch `main`, carpeta `/ (root)`.
3. Abre la URL en Safari del iPhone → Compartir → **Agregar a pantalla de inicio**.

Como `plan-inicial.js` no se sube, la primera vez la app muestra "Crear plan vacío" o "Restaurar desde un respaldo". Para pasar tus datos: en el computador, Ajustes → **Descargar respaldo**, y en el iPhone, **Restaurar respaldo**.

## Dónde se guardan los datos

En `localStorage` del navegador, en cada equipo por separado. Usa Ajustes → Respaldo para copiarlos entre equipos.
