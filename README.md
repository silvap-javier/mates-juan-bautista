# 💵 El Kiosco

Juego de restas para segundo grado, con **billetes de 10 y monedas de 1** — el mismo material que
usa la maestra. Un billete es una decena, una moneda es una unidad.

El chico no calcula: **paga**. Lo que le queda en la billetera *es* el resultado.

Un solo archivo (`index.html`), sin dependencias, sin build, funciona offline.
El progreso se guarda en `localStorage` del navegador del chico.

## Dónde está el concepto

Pagar 25 teniendo 51 (5 billetes y 1 moneda):

1. Da **2 billetes** → le quedan 31. *Las monedas ni se tocan.*
2. Faltan 5 monedas y sólo tiene 1. Da **esa moneda** → le quedan **30 justos, sólo billetes**.
3. Ya no tiene monedas sueltas: **rompe un billete** y se lo cambian por 10 monedas.
4. Da **4 monedas** → le quedan 2 billetes y 6 monedas = **26**.

Eso es exactamente `51 − 25 = 51 − (20 + 1 + 4)`: quitar el número entero o quitarlo por pedazos da
lo mismo, siempre que los pedazos sumen el total. Y el famoso **“1”** deja de ser misterioso:
**son las monedas sueltas que tenía**. Si la cuenta fuera `53 − 25`, tendría 3 sueltas y la partición
sería `20 + 3 + 2`. **Cambia el minuendo, cambia el corte.**

**Romper el billete es pedir prestado**, pero visible y con una razón: *no me quedan monedas*.
Cuando pase a la cuenta escrita en columna, ese “me llevo una” ya va a tener significado.

## El camino

Las paradas no son una lista: son un **camino tipo tablero** que baja serpenteando hasta el kiosco 🏪.
El chico 🧒 está parado en la parada donde va, el tramo recorrido se pinta de verde, y cada parada
terminada queda con sus estrellas. Lo que está más adelante se ve con candado.

| # | Parada | Qué aísla |
|---|--------|-----------|
| 1 | Pago con billetes | el precio es justo de billetes; las monedas no se mueven |
| 2 | Doy las sueltas | pagar con las sueltas y quedar en un número redondo |
| 3 | Rompo un billete | no hay monedas: hay que cambiar |
| 4 | La compra completa | billetes → sueltas → romper → resto |
| 5 | Me dan vuelto | con precio 38 conviene dar 40 y recibir 2 |
| 6 | Desafío final | primero predice lo que le va a quedar, después lo comprueba |

En cada compra sale un producto del kiosco al azar (🍫 un alfajor, 🪀 un yoyó, ✏️ un lápiz…) con su
precio. Son 5 compras por parada.

## “La cuenta”: el puente al papel

Arriba de la billetera hay un panel donde **cada acción escribe su operación sola**:

```
65 − 10 = 55     un billete
55 −  5 = 50     5 monedas
50  = 40 + 10    rompí un billete
50 −  3 = 47     3 monedas
─────────────────────────────
65 − 18 = 47     la cuenta entera
```

Las acciones seguidas del mismo tipo **se juntan en una sola línea**: dar 5 monedas escribe
`55 − 5 = 50`, no cinco restas de 1. Eso es lo que hace que se lea como una descomposición y no como
un conteo. Y romper un billete se escribe `50 = 40 + 10`: la misma plata, repartida distinto.

Al terminar queda la resta completa escrita, hecha por él. Vale la pena leerla en voz alta juntos.

Hay **↩️ Deshacer** para volver atrás una acción sin reiniciar la compra.

## También está el juego de la rana

`saltos.html` — la misma idea sobre una recta numérica, con saltos. Está enlazado desde el mapa.
Es más abstracto: sirve como paso siguiente, cuando el kiosco ya le sale solo.

## Probarlo en local

```bash
python3 -m http.server 8080
# abrir http://localhost:8080
```

O directamente: abrir `index.html` con doble clic (no necesita servidor).

## Desplegar en DigitalOcean App Platform

App Platform necesita un repo git como origen. Una sola vez:

```bash
# 1. subir a GitHub (repo nuevo, vacío, sin README)
git init && git add -A && git commit -m "El Kiosco"
git branch -M main
git remote add origin git@github.com:TU-USUARIO/el-kiosco.git
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
