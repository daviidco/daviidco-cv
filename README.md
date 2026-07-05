# David Córdoba — CV / Portfolio

Sitio de CV/portafolio construido con [Astro](https://astro.build), publicado en GitHub Pages en:

**https://daviidco.github.io/resume-cv/**

## 🚀 Estructura del proyecto

```text
/
├── public/
│   ├── favicon.ico / favicon.svg
│   ├── images/            # imágenes usadas como fondo (hero, guitarra, etc.)
│   └── docs/               # PDF del CV descargable
├── src/
│   ├── components/         # Hero, About, Resume, Contact, Nav, Footer
│   ├── data/
│   │   └── profile.json    # todo el contenido del CV (nombre, empleo, skills, contacto...)
│   └── pages/
│       ├── index.astro     # landing con selector white/black
│       ├── white.astro     # versión clara del CV
│       └── black.astro     # versión oscura del CV
└── package.json
```

Todo el contenido (nombre, bio, empleos, skills, contacto, redes) vive en `src/data/profile.json`; los componentes solo lo consumen.

## 🧞 Comandos

Todos se corren desde la raíz del proyecto:

| Comando                   | Acción                                            |
| :------------------------ | :------------------------------------------------ |
| `npm install`              | Instala dependencias                             |
| `npm run dev`               | Levanta el servidor local en `localhost:4321`    |
| `npm run build`             | Genera el sitio de producción en `./dist/`       |
| `npm run preview`           | Sirve el build de producción para probarlo local |
| `npm run astro ...`         | Corre comandos de la CLI de Astro                |

## 🚢 Despliegue (GitHub Pages)

El sitio se publica como **project site** de GitHub Pages, es decir, vive en una subcarpeta:
`https://daviidco.github.io/resume-cv/` (no en la raíz del dominio).

Por eso `astro.config.mjs` define:

```js
site: 'https://daviidco.github.io',
base: '/resume-cv/',
```

Y todo enlace o asset interno (favicons, imágenes de fondo, el PDF del CV, los links a `/white` y `/black`) se arma con `import.meta.env.BASE_URL` en vez de una ruta absoluta hardcodeada — de lo contrario funcionan en local pero rompen (404) en producción bajo la subcarpeta. Ver la convención completa en [AGENTS.md](./AGENTS.md).

El despliegue es automático vía GitHub Actions (`.github/workflows/deploy.yml`): cada push a `main` dispara el build y la publicación. Requisitos en GitHub (una sola vez):

1. El repo debe ser público (o tener un plan que soporte Pages en repos privados).
2. `Settings → Pages → Build and deployment → Source` debe estar en **GitHub Actions**.

## 👀 Más info

Documentación de Astro: https://docs.astro.build
