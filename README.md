# 🎒 Las mates de Juan Bautista

Tres juegos de resta para segundo grado. Un archivo cada uno, sin dependencias ni build,
funcionan offline. **`index.html` es la portada**: saluda, muestra las estrellas de cada juego y
lleva a los tres.

| Archivo | Juego | Qué practica |
|---------|-------|--------------|
| `index.html` | 🎒 portada | por dónde empezar |
| `hoja.html` | ✏️ Como en clase | el método del cuaderno (empezá acá) |
| `kiosco.html` | 💵 El Kiosco | restar pagando |
| `numeros.html` | 🏦 El Banquito | descomponer números |
| `saltos.html` | 🐸 la rana | *sin enlazar* — versión vieja con recta numérica |

## ✏️ Como en clase — `hoja.html`

**Copia la hoja de la escuela.** Papel rayado, margen rojo, y la misma notación: las flechitas
arriba del segundo número lo parten en tres pedacitos, y abajo van las tres líneas.

```
        20    5    2
         ↖    ↑    ↗
      65 − 27 = 38
      65 − 20 = 45
      45 −  5 = 40
      40 −  2 = 38
```

Todas las cuentas son **menores a 50** y el número que se resta tiene **2 o 3 decenas**, como en el
cuaderno. En las paradas de tres pedacitos, arriba se ve el objetivo armándose solo:
`? + ? + ? = 26` → `20 + 4 + 2 = 26`, así queda claro que los pedazos tienen que sumar el número.

**Cada línea se resuelve mirando plata.** Debajo de la cuenta activa aparece el número en billetes
y monedas, con **tachado en rojo lo que hay que sacar**: para `44 − 30` se ven 4 billetes y 4 monedas
con 3 billetes tachados, y sólo hay que contar lo que queda. Cuando toca restar de un redondo
(`30 − 4`), el número aparece ya con **un billete roto en 10 monedas** — el mismo canje del kiosco.
En la última parada esa ayuda no está.

**La descomposición se ve, no se lee.** Debajo de cada flechita está el pedacito dibujado en plata:
el `30` son tres billetes verdes, el `2` son dos monedas. Los que todavía no eligió aparecen en gris,
así puede contarlos antes de decidir. Y **las unidades del número de arriba van resaltadas en amarillo**
(el `2` de `72`), que es de donde sale el pedacito del medio — el que lo deja parado en un redondo.
**El casillero del medio está pintado del mismo amarillo**, con su flecha, para que se lea que son la
misma cosa; y mientras toca elegirlo, el dígito late.
En la última parada la ayuda gris desaparece.

Casi sin texto: las únicas consignas son **“Primero las decenas”**, **“Bajá al redondo”**,
**“Lo que sobra”** y **“¿Cuánto da?”**. Los cortes se eligen tocando un número grande; los
resultados se escriben con el teclado. Si se equivoca: `🙈 Esa no…`, y a la segunda una pista de
cuatro palabras (*“Mirá el final del 51”*).

**Nunca se pide el resultado de golpe**: siempre hay flechitas y líneas. Las dos primeras paradas
usan restas que no cruzan la decena y se parten en **dos** pedacitos; de la tercera en adelante, en tres.

| # | Parada | Pedacitos | Qué pide |
|---|--------|-----------|----------|
| 1 | Dos pedacitos | 2 | los cortes ya vienen marcados; escribe las dos cuentas |
| 2 | Cortá vos | 2 | elige los cortes y escribe las cuentas |
| 3 | Tres pedacitos | 3 | sólo elegir los tres cortes; las líneas salen solas |
| 4 | Las tres líneas | 3 | los cortes ya vienen marcados; escribe los resultados |
| 5 | Todo junto | 3 | corte y resultado, uno tras otro |
| 6 | Vos solo | 3 | igual, sin la ayuda gris y con números más grandes |

**El corte no es fijo.** El primer pedacito son las decenas del número que resta; el segundo son
**las unidades del número de arriba** (el 1 del 51), para caer justo en un redondo; el tercero es lo
que sobra. Con `53 − 25` el corte sería `20 · 3 · 2`. Cambia el número de arriba, cambia el corte.


## 💵 El Kiosco — `kiosco.html`

Restar pagando, con **billetes de 10 y monedas de 1** — el mismo material que
usa la maestra. Un billete es una decena, una moneda es una unidad.

El chico no calcula: **paga**. Lo que le queda en la billetera *es* el resultado.

Un solo archivo (`kiosco.html`), sin dependencias, sin build, funciona offline.
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

## “Para poder pagar…”: la descomposición que hace falta

Arriba de la billetera hay una tabla de **decenas y unidades** que muestra, en vivo, la
descomposición que el número necesita para poder restarse:

```
                    💵 billetes    🪙 monedas
                       de 10          de 1
   tenés  42             4̶ 3          2̶ 12
   pagás  27              2             7
   ─────────────────────────────────────────
   te quedan              ?             ?

   ✅ Rompiste un billete: el 42 dejó de ser 40 + 2 y ahora es 30 + 12.
      Con 12 monedas ya podés pagar 7.
```

Antes de romper, la celda de las monedas **late en rojo**: *“⚠️ Con 2 monedas no podés pagar 7”*.
Al romper, el 4 queda tachado con un 3 al lado y el 2 pasa a 12 — que es exactamente lo que la
maestra escribe arriba de la cuenta en columna. Al terminar, la nota cierra el círculo:

```
3 − 2 = 1 billetes  y  12 − 7 = 5 monedas  →  42 − 27 = 15
```

La tabla no aparece en la parada 5 (la del vuelto), porque ahí la estrategia no es descomponer sino
compensar.

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

## 🏦 El Banquito — descomposición de números

`numeros.html` — el mismo camino y el mismo material, pero sobre **descomponer números**, que es lo
que la maestra trabaja día a día. Enlazado desde el mapa del kiosco.

La idea que sostiene todo: `47 = 40 + 7` **no es la única forma**. También es `30 + 17`, y esa
descomposición “rara” es exactamente lo que pasa cuando en el kiosco **rompe un billete**. Un chico
que sólo sabe que 47 es 40 + 7 se traba cuando tiene que pagar 8 monedas; uno que sabe que 47
*también* es 30 + 17 no se traba. Por eso las dos últimas paradas insisten con esa forma.

| # | Parada | Qué hace |
|---|--------|----------|
| 1 | Armá el número | pone billetes y monedas hasta llegar justo al número |
| 2 | ¿Cuánto hay? | lee una pila normal (4 billetes y 7 monedas → 47) |
| 3 | Muchas monedas | lee una pila con más de 10 monedas (6 billetes y 15 → 75) |
| 4 | De otra forma | el mismo número con **un billete menos**: 54 con 4 billetes → `40 + 14` |
| 5 | Completá | `40 + __ = 47`, `__ + 7 = 47` y también `30 + __ = 47` |
| 6 | Desafío final | las tres cosas mezcladas, siempre en la forma rara |

La cuenta se escribe sola mientras toca la plata:

```
💵 3 billetes = 30      de a 10
🪙 6 monedas  =  6      de a 1
────────────────────────────────
   30 + 6 = 36
```

Al armar, poner un billete que se pasaría del número está bloqueado, con el motivo. Al completar hay
un **💡 Verlo con la plata** que muestra en billetes y monedas **el pedazo que ya se conoce** (no la
respuesta).

Puntúa: armando, 3 estrellas si usa la menor cantidad de piezas posible (o si respeta el límite de
billetes cuando se lo pedimos). Leyendo o completando, 3 estrellas si acierta a la primera, 2 a la
segunda, 1 después.

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
