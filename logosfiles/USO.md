# Logo Colegio Humboldt — Guía de uso

Todos los archivos tienen **fondo transparente** y los colores oficiales detectados del original:
- Ocre: `#D69A2D` (coincide con tu `--ocre` del CSS)
- Gris cálido: `#827670`

## Archivos generados

### Logo completo (símbolo + texto)
| Archivo | Tamaño | Peso | Uso |
|---|---|---|---|
| `logo-full-1280.png` | 1280px ancho | 41 KB | Hero / portada, OG image |
| `logo-full-640.png` | 640px ancho | 18 KB | Header @2x (Retina) |
| `logo-full-320.png` | 320px ancho | 8 KB | Header @1x |

### Solo isotipo (símbolo cuadrado)
| Archivo | Tamaño | Peso | Uso |
|---|---|---|---|
| `logo-iso-512.png` | 512×512 | 39 KB | PWA, share icon |
| `logo-iso-256.png` | 256×256 | 14 KB | Cards, hero pequeño |
| `logo-iso-180.png` | 180×180 | 9 KB | Apple touch icon |
| `logo-iso-128.png` | 128×128 | 6 KB | Header móvil |
| `logo-iso-64.png` | 64×64 | 2.4 KB | Favicon grande |
| `logo-iso-32.png` | 32×32 | 1 KB | Favicon estándar |
| `logo-iso-16.png` | 16×16 | 504 B | Favicon tab |
| `favicon.ico` | 16+32+48 | 985 B | Favicon legacy |

## Cómo usarlos en el HTML

### En el `<head>` (favicons y meta)
```html
<link rel="icon" href="/logo/favicon.ico" sizes="any">
<link rel="icon" href="/logo/logo-iso-32.png" type="image/png" sizes="32x32">
<link rel="icon" href="/logo/logo-iso-16.png" type="image/png" sizes="16x16">
<link rel="apple-touch-icon" href="/logo/logo-iso-180.png">

<!-- Actualizar también el og:image para que use el logo nuevo -->
<meta property="og:image" content="https://www-colegio-humboldt-cl.vercel.app/logo/logo-full-1280.png">
<meta property="og:image:width" content="1280">
<meta property="og:image:height" content="1049">
```

### En el header (logo responsive con srcset)
```html
<a href="/" class="brand">
  <img
    src="/logo/logo-full-320.png"
    srcset="/logo/logo-full-320.png 1x, /logo/logo-full-640.png 2x"
    alt="Colegio Humboldt"
    width="160"
    height="131"
    decoding="async"
  >
</a>
```
Importante: incluir `width` y `height` evita layout shift (CLS) y mejora Core Web Vitals.

### En el hero / portada
```html
<img
  src="/logo/logo-full-640.png"
  srcset="/logo/logo-full-640.png 1x, /logo/logo-full-1280.png 2x"
  alt="Colegio Humboldt"
  width="480"
  height="393"
  decoding="async"
  fetchpriority="high"
>
```

### Solo el símbolo (para iconos pequeños, accent decorativo)
```html
<img
  src="/logo/logo-iso-64.png"
  srcset="/logo/logo-iso-64.png 1x, /logo/logo-iso-128.png 2x"
  alt=""
  width="32"
  height="32"
  aria-hidden="true"
>
```
(Usa `alt=""` + `aria-hidden="true"` si ya hay texto "Colegio Humboldt" cerca, así no lo lee dos veces el lector de pantalla.)

## Notas técnicas

- Las imágenes están **cuantizadas con paleta**: como el logo solo tiene dos colores reales, los PNG con paleta de 8-16 colores pesan mucho menos que un PNG truecolor (reducción de ~67% sobre el optimize estándar).
- **No incluí versiones WebP** porque para imágenes con paleta tan pequeña los PNG cuantizados ganan en peso a WebP.
- **No vectoricé a SVG** porque la silueta del coral/árbol con bordes irregulares requiere paths muy largos; los SVG resultantes pesaban entre 25-35 KB, más que los PNG. Si en algún momento tienes acceso al archivo original `.ai` o `.eps`, exportar a SVG desde ahí daría mejor resultado.
- **Aspect ratio del logo completo**: 1055:864 ≈ 1.22:1. Las dimensiones height en los snippets están calculadas con ese ratio.
