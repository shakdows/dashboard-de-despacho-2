# Dashboard de Almacén — Control de Guías Emitidas

Dashboard analítico interactivo del **Almacén Principal Faraday**, construido a partir del
control de guías emitidas. Un solo archivo `index.html`, 100 % del lado del cliente
(HTML + CSS + JavaScript vanilla + Chart.js por CDN). Sin build, sin backend.

> Creado por **Alexis Ramírez** · alias **Shakdows** · [veronix.ai](https://veronix.ai)
> © 2026 Alexis Ramírez (Shakdows) · VERONIX

---

## ¿Qué muestra?

- **6 KPIs**: guías emitidas, valor despachado (US$), ítems, tiempo mediano de picking,
  cumplimiento SUNAT y tasa de anulación.
- **6 gráficos interactivos**:
  1. Volumen diario de guías (línea + promedio).
  2. Motivo de traslado (dona).
  3. Carga de trabajo por hora (barras, resalta la hora punta).
  4. Distribución del tiempo de picking (histograma verde→ámbar→rojo).
  5. Top 10 clientes por número de guías.
  6. Estado de las guías (dona).
- **Filtros dinámicos**: tipo de documento, día y motivo de traslado. Todo recalcula al instante.
- Cada gráfico clave lleva una nota en lenguaje simple para que cualquier empleado lo entienda.

Los datos están **embebidos** dentro de `index.html` (no requiere archivos externos).

---

## Estructura del repo

```
index.html            → dashboard completo (estructura + CSS + datos + logo embebidos)
vercel.json           → configuración de sitio estático
logo-shakdows.png     → logo Grima (referencia; ya va embebido en el HTML)
.gitignore
README.md
```

---

## Despliegue: GitHub → Vercel

1. Crea un repositorio nuevo en GitHub y sube estos archivos (arrastra y suelta en la web
   o `git push`).
2. Entra a [vercel.com](https://vercel.com) → **Add New → Project** → importa el repositorio.
3. Framework Preset: **Other**. No hay build command ni output directory que configurar
   (es un sitio estático de un solo archivo).
4. **Deploy**. Vercel sirve `index.html` automáticamente en la raíz.

Cada vez que hagas `push` a la rama principal, Vercel redepliega solo.

---

## 🔐 Acceso por token mensual

El dashboard se abre con una **pantalla de acceso**. Cada mes requiere un token distinto:
entrégalo al cliente **solo tras confirmar el pago del mes**. Al ingresar un token válido
se guarda en el navegador y no se vuelve a pedir hasta que expire.

**Tokens 2026** (definidos en `index.html`, arriba del todo, en `VALID_TOKENS`):

| Mes        | Token                 | Vence      |
|------------|-----------------------|------------|
| Enero      | 84H5-QMWX-3UBJ-4GEY   | 31/01/2026 |
| Febrero    | RJ3D-KZAJ-DMZJ-G3AT   | 28/02/2026 |
| Marzo      | QSW5-7B4V-DW25-7MKU   | 31/03/2026 |
| Abril      | K2VD-VKKF-NNY5-7WBD   | 30/04/2026 |
| Mayo       | UAYN-BGTP-JXSG-2SPQ   | 31/05/2026 |
| Junio      | BTXW-7CV2-EX6V-Y658   | 30/06/2026 |
| Julio      | 2QMP-38NH-GZE7-WQBW   | 31/07/2026 |
| Agosto     | 26SA-C2FE-PJVG-SEBW   | 31/08/2026 |
| Septiembre | 7ES9-U623-3PSN-6G53   | 30/09/2026 |
| Octubre    | 7TMB-7CAH-N2HX-524D   | 31/10/2026 |
| Noviembre  | UUWV-PG33-QAR9-5W3X   | 30/11/2026 |
| Diciembre  | ASD6-88UW-CY6R-QGC8   | 31/12/2026 |

**Cómo gestionarlo:**

- Para cambiar los códigos, edita la lista `VALID_TOKENS` en `index.html`.
- La clave de almacenamiento en el navegador es `almacen_faraday_dashboard_token`
  (independiente de otros tableros).
- **Importante**: al ser 100 % client-side, este token es una **palanca comercial**, no
  seguridad criptográfica: un usuario técnico podría ver el código fuente. Frena el uso casual
  y el impago. Para un candado real (que puedas desactivar tú a distancia), migra la validación
  a Supabase con una columna `activa`.

---

## Actualizar los datos

El dataset va embebido en `index.html` como la constante `DATA` (un `<script>` cerca del final).
Para actualizarlo, reemplaza ese arreglo con el nuevo export procesado del Excel de control de
guías y vuelve a hacer `push`.
