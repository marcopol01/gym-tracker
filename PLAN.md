# Gym Tracker — plan

## Idea
Web muy sencilla, abrible desde un enlace y "instalable" en el móvil (icono en la pantalla de inicio),
para apuntar en el gimnasio: **ejercicio → series → peso × reps**, y ver cómo progresas.

## Decisión técnica: PWA de un solo archivo
- **HTML + CSS + JS puro**, sin frameworks ni build. Abres `index.html` y funciona.
- **PWA** (`manifest.webmanifest` + `sw.js`): se añade a la pantalla de inicio y funciona **sin conexión** (en el gimnasio muchas veces no hay cobertura).
- **Datos en el propio móvil** (`localStorage`). Sin cuentas, sin servidor, gratis.
- **Exportar / importar JSON** como copia de seguridad o para pasar los datos a otro móvil.

## Enlace directo (hosting gratis)
Cualquiera de estas da una URL tipo `https://tuusuario.github.io/gym-tracker`:
1. **GitHub Pages** – subir la carpeta a un repo y activar Pages.
2. **Netlify Drop** – arrastrar la carpeta a app.netlify.com/drop (30 segundos).
3. **Vercel / Cloudflare Pages** – igual de gratis.

Luego en el móvil: abrir el enlace → "Añadir a pantalla de inicio".

## Pantallas
| Pestaña | Qué hace |
|---|---|
| **Entrenar** | Eliges ejercicio, apuntas peso y reps con botones +/−, "Añadir serie". Te enseña lo que hiciste la última vez para superarlo. |
| **Historial** | Entrenos por día, con todas las series. Se pueden borrar series. |
| **Progreso** | Por ejercicio: mejor peso, 1RM estimado (Epley) y una gráfica de evolución. |

## Modelo de datos
```json
{
  "exercises": ["Press banca", "Sentadilla", ...],
  "sets": [
    { "id": "…", "date": "2026-11-11", "exercise": "Press banca", "weight": 60, "reps": 8, "ts": 1731320000000 }
  ]
}
```

## Fase 2 (si se queda corto)
- **Sincronizar entre dispositivos**: Supabase (gratis) con login por email mágico.
- Rutinas predefinidas (Push / Pull / Pierna), temporizador de descanso, notas por serie.
- Convertir a app nativa con Capacitor si se quiere publicar en tiendas.
