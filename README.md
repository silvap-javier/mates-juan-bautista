# 🐸 Saltos de Rana

Juego de restas para segundo grado. Enseña **descomposición del sustraendo con apoyo en la decena**
(*bridging through ten*): en vez de restar 25 de un tirón, la rana salta `−20`, `−1`, `−4`.

Un solo archivo (`index.html`), sin dependencias, sin build, funciona offline.
El progreso se guarda en `localStorage` del navegador del chico.

## Las 6 misiones

| # | Misión | Qué aísla |
|---|--------|-----------|
| 1 | Saco las decenas | `51 − 20` → las unidades no se tocan |
| 2 | Bajo al redondo | estando en `31`, ¿cuánto saco para llegar a `30`? |
| 3 | Salto desde el redondo | `30 − 4`, tan fácil como `10 − 4` |
| 4 | El camino completo | `51 − 25` en los tres saltos, guiado |
| 5 | Elegí el camino | con `−29` conviene compensar, no descomponer |
| 6 | Desafío | la cuenta entera, la pista a pedido |

Cada misión son 5 cuentas; al terminar cada una aparece **“¿Por qué cortamos ahí?”** con la
explicación generada para *esos* números — que es el punto: el `−1` de `51 − 25` son las unidades
del 51, y si la cuenta fuera `53 − 25` el corte sería `20 − 3 − 2`.

Abajo de todo hay un panel plegable **“Para el adulto”** con el fundamento y la pregunta útil
para practicar en casa (*“¿por qué cortaste ahí?”*, no *“¿cuánto da?”*).

## Probarlo en local

```bash
python3 -m http.server 8080
# abrir http://localhost:8080
```

## Desplegar en DigitalOcean App Platform

App Platform necesita un repo git como origen. Una sola vez:

```bash
# 1. subir a GitHub (repo nuevo, vacío, sin README)
git init && git add -A && git commit -m "Saltos de Rana"
git branch -M main
git remote add origin git@github.com:TU-USUARIO/saltos-de-rana.git
git push -u origin main

# 2. poner tu usuario/repo en .do/app.yaml (línea `repo:`)

# 3. crear la app
doctl apps create --spec .do/app.yaml
```

A partir de ahí, cada `git push` a `main` redespliega solo (`deploy_on_push: true`).

Para ver la URL: `doctl apps list`. Sitio estático → **plan Starter, gratis** (3 sitios estáticos
sin costo por cuenta).

Si preferís la consola web: **Create → Apps → GitHub → este repo → Resource Type: Static Site**,
output directory `/`. No hace falta comando de build.

### Actualizar después de un cambio

```bash
git add -A && git commit -m "ajustes" && git push
```

O forzar sin cambios: `doctl apps create-deployment <APP_ID>`.
