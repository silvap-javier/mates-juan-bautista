# 🐸 Saltos de Rana

Juego de restas para segundo grado. Enseña **descomposición del sustraendo con apoyo en la decena**
(*bridging through ten*): en vez de restar 25 de un tirón, la rana salta `−20`, `−1`, `−4`.

Un solo archivo (`index.html`), sin dependencias, sin build, funciona offline.
El progreso se guarda en `localStorage` del navegador del chico.

## Cómo se juega

El chico **no escribe el resultado: lo alcanza saltando**. Arma el tamaño del salto con los
botones `−10 −1 +1 +10`, ve con la **rana fantasma dónde va a caer antes de saltar**, y repite
hasta llegar a la meta 🏁. El resultado aparece porque cayó ahí.

Dos atajos que enseñan solos:

- **Tocar una piedra redonda** calcula el salto necesario y lo dice en voz alta:
  *“Para llegar a la piedra 40 el salto tiene que ser de 6”*. Ahí se ve que el pedacito
  son las unidades del número donde está parado.
- **El búho 🦉 habla en cada paso** — es el adulto acompañando: avisa antes de cruzar
  una decena, festeja cuando cae en un redondo, y al final muestra la partición que el
  chico mismo armó.

### Las 6 misiones

| # | Misión | Qué aísla | Meta |
|---|--------|-----------|------|
| 1 | Saltos de a diez | `56 − 20` → las unidades no se tocan | 1 salto |
| 2 | Pisá la piedra redonda | de `34` caer justo en `30` | 1 salto |
| 3 | Salgo del redondo | `30 − 4`, igual que `10 − 4` | 1 salto |
| 4 | El camino completo | `51 − 25`: decenas → piedra → resto | 3 saltos |
| 5 | El atajo del redondo | con `−29` conviene pasarse y devolver | 2 saltos |
| 6 | Desafío | primero predice el resultado, después lo comprueba | 3 saltos |

### Cómo puntúa (es lo que empuja a partir bien)

Las **3 estrellas** se ganan por llegar **sin cruzar ninguna decena de un salto**, dentro de la
meta. Si cruza —por ejemplo `58 − 9 = 49` de una— llega igual, pero se lleva 1 estrella y el búho
le señala el salto culpable y qué hacer en su lugar. No se premia la cuenta rápida: se premia
**la partición que no obliga a cruzar**, que es exactamente la dificultad que se está atacando.

Al terminar cada cuenta aparece **“¿Por qué cortaste ahí?”** con el camino real que hizo:
*“Partiste el 16 en 10 + 3 + 3… y ese 3 son las unidades del 43. Con otro número de arriba,
el corte sería otro.”*

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
