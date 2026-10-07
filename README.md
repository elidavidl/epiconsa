# EPICONSA | Página de ventas de artículos religiosos

Sitio estático hecho solo con HTML, CSS y JavaScript. No necesita instalar nada para funcionar.
El cliente arma su pedido en la página y lo envía por WhatsApp.

## Estructura

```
epiconsa/
├── index.html            Estructura y textos de la página
├── css/styles.css        Colores, tipografías y diseño
├── js/
│   ├── config.js         Número de WhatsApp y moneda  <- editar primero
│   ├── productos.js      Catálogo de productos        <- editar para agregar/quitar
│   └── main.js           Filtros, pedido y WhatsApp
├── img/                  Imágenes en formato WebP
├── tools/convertir_webp.py   Convierte tus fotos JPG/PNG a WebP
└── .nojekyll             Evita que GitHub Pages procese la carpeta
```

## Lo primero que debes cambiar

1. **Número de WhatsApp**: `js/config.js`, campo `whatsapp` (con código de país, solo dígitos: `51987654321`).
2. **Datos de contacto y horario**: al final de `index.html`, dentro de `<footer>`.
3. **Productos, precios e imágenes**: `js/productos.js`. Los precios y las imágenes actuales son de ejemplo.

## Cómo editar el código

### Opción A: en tu computadora (recomendada)

1. Instala [VS Code](https://code.visualstudio.com/) (gratis).
2. Abre la carpeta `epiconsa` con **Archivo > Abrir carpeta**.
3. Instala la extensión **Live Server** y haz clic derecho en `index.html` > **Open with Live Server**. La página se actualiza sola cada vez que guardas.
4. Cuando termines, sube los cambios a GitHub (ver más abajo).

También puedes abrir `index.html` con doble clic; todo funciona sin servidor.

### Opción B: directo en GitHub, sin instalar nada

Entra a tu repositorio y presiona la tecla **`.`** (punto). Se abre un editor VS Code en el navegador.
Edita, guarda y en el panel de Control de código fuente escribe un mensaje y presiona **Commit & Push**.

## Qué archivo tocar según lo que quieras cambiar

| Quiero cambiar... | Archivo |
|---|---|
| Colores de la marca | `css/styles.css`, bloque `:root` al inicio |
| Tipografías | `index.html` (enlace de Google Fonts) y variables `--serif` y `--sans` en `:root` |
| Titulares y textos | `index.html` |
| Agregar o quitar un producto | `js/productos.js` |
| Número de WhatsApp | `js/config.js` |
| Mensaje que llega por WhatsApp | `js/main.js`, función del botón `#enviar-pedido` |

Para agregar un producto, copia un bloque `{ ... }` de `productos.js`, cambia sus datos y guarda la imagen en `img/`.
Las categorías nuevas aparecen solas como filtros.

## Imágenes en WebP

El catálogo usa fotos en proporción **4:5** (800 x 1000 px) y la portada **4:5** (1000 x 1250 px).

**Con el script incluido:**

```bash
pip install pillow
mkdir fotos-originales        # deja aquí tus JPG o PNG
python tools/convertir_webp.py fotos-originales img
```

**Sin instalar nada:** sube tus fotos a [squoosh.app](https://squoosh.app), elige **WebP**, calidad 75 a 85, y descarga el resultado a la carpeta `img/`.

Después escribe el nombre del archivo en el campo `imagen` del producto en `productos.js`.

Consejos: usa fondos limpios y parecidos entre fotos, y apunta a menos de 80 KB por imagen.

## Publicar en GitHub Pages

Desde la web de GitHub:

1. Crea un repositorio nuevo, por ejemplo `epiconsa` (público).
2. Presiona **Add file > Upload files** y arrastra **el contenido** de la carpeta (no la carpeta misma). El archivo `index.html` debe quedar en la raíz del repositorio. Incluye `.nojekyll`; si tu sistema lo oculta, créalo desde GitHub con **Add file > Create new file**.
3. Presiona **Commit changes**.
4. Ve a **Settings > Pages**. En **Source** elige **Deploy from a branch**, rama **main**, carpeta **/ (root)** y guarda.
5. En uno o dos minutos la página estará en `https://TU-USUARIO.github.io/epiconsa/`.

Desde la terminal, si prefieres Git:

```bash
cd epiconsa
git init
git add .
git commit -m "Primera versión de EPICONSA"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/epiconsa.git
git push -u origin main
```

Para publicar cambios más adelante: `git add .`, `git commit -m "Describe el cambio"` y `git push`. GitHub Pages se actualiza solo.

## Notas

- El pedido del cliente se guarda en su propio navegador (`localStorage`); no hay base de datos ni pagos en línea. La venta se cierra por WhatsApp.
- Las rutas son relativas, así que el sitio funciona igual en `usuario.github.io/epiconsa/` que en un dominio propio.
- Las tipografías (Gloock y Hanken Grotesk) se cargan desde Google Fonts. Sin internet, la página usa fuentes del sistema.
