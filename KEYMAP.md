# Guía del keymap — Redox split BT (ZMK)

> Estado: firmware compilado (Ola 1, run 30771933347) — **pendiente de flashear**.
> Generado el 2026-08-02 a partir de `config/redox.keymap`.

---

## Cheat-sheet (lo que vas a usar todo el día)

| Quiero… | Hago… |
|---|---|
| Mayúscula | Mantengo `D` (izq) o `K` (der) + la letra |
| Ctrl / Alt / GUI | Mantengo `F`/`S`/`A` (izq) o `J`/`L`/`;` (der) |
| Escape | `Q` + `W` juntas |
| Deshacer / Cortar / Copiar / Pegar | `Z+X` / `X+C` / `C+V` / `V+B` |
| ESCRIBIR EN MAYÚSCULAS | Doble tap en **MAGIC**, o los dos Shift juntos. Corta con espacio |
| Repetir la última letra | Tap en **MAGIC** justo después de tipearla |
| Una sola mayúscula sin sostener | Tap en **MAGIC** (en frío) y después la letra |
| Volumen / play-pausa | Mantengo `CAPS` → `J K L` (vol−/mute/vol+) y `U I O` (prev/play/next) |
| Alt-Tab | Mantengo **NAV** (pulgar izq) → taps en `U` |
| Mover el mouse | `W` + `P` juntas → puntero en `I J K L` |
| Números / símbolos | Mantengo **SYM** (pulgar der) |
| Flechas y navegación | Mantengo **NAV** (pulgar izq) |
| Bluetooth / F1-F12 | Mantengo **NAV** + `BSPC` (pulgar izq interno) |
| Poner en bootloader | Izq: `ESC` + `DEL`. Der: `BSPC` (fila 1) + `ENTER` |

---

## Cómo se entra a cada capa

| Capa | Acceso | Qué tiene |
|---|---|---|
| **SYM** (1) | Mantener pulgar **derecho interno** | Números, keypad, símbolos básicos |
| **NAV** (2) | Mantener pulgar **izquierdo** (4ª tecla fila inferior… ver mapa) | `!@#$%`, flechas, Home/End/PgUp/PgDn, **swapper** |
| **ADJ** (3) | Mantener **NAV** + `BSPC` o + `MAGIC` | Bluetooth, F1-F12, bootloader, reset, media viejo |
| **MEDIA** (4) | Mantener `CAPS` (mano izq) | Volumen, play/pausa, prev/next |
| **MOUSE** (5) | Combo `W` + `P` | Puntero, scroll, clicks. **Se apaga sola** al tipear |

---

## Capa BASE

```
  ESC     1     2     3     4     5                              6     7     8     9     0  BSPC
  TAB     Q     W     E     R     T     ‑                  =     Y     U     I     O     P     \
 CAPS     A     S     D     F     G     [                  ]     H     J     K     L     ;     '
 SHFT     Z     X     C     V     B  PGDN  PGUP      HOME  END    N     M     ,     .     /  ⇧/⏎
 CTRL   GUI   ALT MAGIC   NAV       BSPC   DEL        ENT   SPC      SYM  LEFT  DOWN    UP RIGHT
```

**Home-row mods (GASC)** — se activan manteniendo la tecla:

```
        A     S     D     F                          J     K     L     ;
       GUI   ALT  SHIFT CTRL                        CTRL SHIFT   ALT   GUI
```

Configuración "timeless" de urob: `flavor=balanced`, `tapping-term 280 ms`, `require-prior-idle 150 ms` y *positional hold-tap* — o sea, un mod solo dispara si la tecla que lo acompaña está en **la otra mitad**. Por eso tipear rápido no genera mods fantasma.

**Teclas con dos funciones en la base:**

| Tecla | Tap | Hold |
|---|---|---|
| `CAPS` | CapsLock | Capa MEDIA |
| `MAGIC` | ver abajo | Shift |
| Esquina inferior derecha | Enter | Shift |

---

## MAGIC — la tecla de cuatro caras

Está en la 4ª posición de la fila inferior izquierda (la que antes estaba muerta). Es el patrón *magic thumb* de urob y se comporta según el contexto:

| Gesto | Qué hace | Para qué sirve |
|---|---|---|
| **Tap justo después de una letra** (< 1,2 s) | Repite esa letra | Evita el doble golpe con el mismo dedo: `ll`, `rr`, `ee`, `nn` |
| **Tap "en frío"** (pausa antes) | Sticky Shift | La próxima tecla sale en mayúscula, sin sostener nada |
| **Doble tap** | Caps Word | Escribe en MAYÚSCULAS hasta que tocás espacio |
| **Hold** | Shift normal | Mayúscula sosteniendo, como siempre |

La distinción entre repeat y sticky-shift la hace el módulo `zmk-adaptive-key`: si la tecla anterior fue una letra y pasó menos de 1,2 s, es repeat; si no, es Shift.

---

## Capa SYM — números y símbolos

*(mantener pulgar derecho interno)*

```
    ·     ·     ·     ·     ·     ·                              ·     ·     ·     ·     ·     ·
  ESC     1     2     3     4     5     ·                  ·     6     7     8     9     0   DEL
    ·     ‑     =     [     ]     \     ·                  ·     *     4     5     6     +     ‑
    ·   ESC   GUI  ⌘+C   ⌘+V     `     ·     ·         ·   ·     /     1     2     3    ⏎     ⏎
    ·     ·     ·     ·     ·         ·     ·           ·     0      ADJ     ·     ·     ·     ·
```

`·` = transparente (pasa a la capa base).

---

## Capa NAV — navegación y símbolos shifted

*(mantener pulgar izquierdo)*

```
    ·     ·     ·     ·     ·     ·                              ·     ·     ·     ·     ·     ·
  ESC     !     @     #     $     %     ·                  ·     ·  SWAP     ·     ·     ·   DEL
    ·     _     +     {     }     |     ·                  ·  HOME  PGUP  PRSC    ↑     `     ~
    ·   ESC   GUI     (     )     ~     ·     ·         ·   ·   END  PGDN     ←     ↓     →    ⏎
    ·     ·     ·   ADJ     ·         ADJ     ·           ·     ·      ·     ·     ·     ·     ·
```

**SWAP** (en la posición de `U`) es el swapper Alt-Tab — ver abajo.
Las flechas quedan en `L` (arriba) y `, . /` (izquierda, abajo, derecha).

---

## SWAPPER — Alt-Tab con una tecla

Con **NAV** mantenido, cada tap en `U`:

1. El primer tap abre el switcher de Windows y **mantiene Alt virtualmente**.
2. Cada tap siguiente avanza una ventana.
3. Las **flechas** y los **Shift** navegan la grilla **sin cerrarlo** (Shift va hacia atrás).
4. Cualquier otra tecla lo cierra y suelta Alt.

O sea: Alt-Tab completo sin retorcer la mano para sostener Alt.

---

## Capa MEDIA — volumen y reproducción

*(mantener `CAPS` con la izquierda; tap de `CAPS` sigue siendo CapsLock)*

```
    ·     ·     ·     ·     ·     ·                              ·     ·     ·     ·     ·     ·
    ·     ·     ·     ·     ·     ·     ·                  ·     ·  PREV  PLAY  NEXT     ·     ·
    ·     ·     ·     ·     ·     ·     ·                  ·     ·  VOL−  MUTE  VOL+     ·     ·
    ·     ·     ·     ·     ·     ·     ·     ·         ·   ·     ·     ·     ·     ·     ·     ·
    ·     ·     ·     ·     ·         ·     ·           ·     ·      ·     ·     ·     ·     ·
```

Todo bajo la mano derecha en reposo: `U I O` para pistas, `J K L` para volumen.

---

## Capa MOUSE — puntero y scroll

*(combo `W` + `P` para entrar)*

```
    ·     ·     ·     ·     ·     ·                              ·     ·     ·     ·     ·     ·
    ·     ·     ·     ·     ·     ·     ·                  ·     ·   ⇑SC    ↑M   ⇓SC     ·     ·
    ·     ·     ·     ·     ·     ·     ·                  ·   ⇐SC    ←M    ↓M    →M   ⇒SC     ·
    ·     ·     ·     ·     ·     ·     ·     ·         ·   ·     ·     ·     ·     ·     ·     ·
    ·     ·     ·     ·     ·        CLIC-M   ·        CLIC-D CLIC-I    ·     ·     ·     ·     ·
```

- **Puntero:** `I` arriba, `J` izquierda, `K` abajo, `L` derecha.
- **Scroll:** `U` arriba, `O` abajo, `H` izquierda, `;` derecha.
- **Clicks:** `SPACE` (pulgar der) = izquierdo · `ENTER` (pulgar der) = derecho · `BSPC` (pulgar izq) = medio.
- **Salida automática:** apenas tocás cualquier tecla fuera de ese grupo, la capa se apaga sola y esa tecla se escribe normal. No te podés quedar "atrapado" en la capa.

---

## Capa ADJ — Bluetooth, F-keys, mantenimiento

*(mantener NAV + `BSPC` o + `MAGIC`)*

```
   F1    F2    F3    F4    F5    F6                             F7    F8    F9   F10   F11   F12
    ·     ·     ·     ·     ·     ·  BOOT                 BTclr  BT0   BT1   BT2   BT3   BT4  OUT
    ·  MUTE  VOL−  VOL+  PLAY     ·  RESET                    ·   F1    F2    F3    F4    F5   F6
    ·  PRSC  PRSC  CAPS     ·     ·     ·     ·         ·   ·    F7    F8    F9   F10   F11   F12
    ·     ·     ·     ·     ·         ·     ·           ·     ·      ·     ·     ·     ·     ·
```

- `BT0`–`BT4` seleccionan perfil Bluetooth; `BTclr` borra el emparejamiento del perfil activo.
- `OUT` alterna salida USB ↔ Bluetooth.
- El media de esta capa quedó como duplicado histórico — el acceso bueno ahora es la capa MEDIA.

---

## Combos (dos teclas juntas)

| Combo | Resultado | Nota |
|---|---|---|
| `Z` + `X` | Deshacer (Ctrl+Z) | |
| `X` + `C` | Cortar (Ctrl+X) | |
| `C` + `V` | Copiar (Ctrl+C) | |
| `V` + `B` | Pegar (Ctrl+V) | |
| `Q` + `W` | Escape | |
| `Shift` izq + `Shift/Enter` der | Caps Word | |
| `W` + `P` | Capa MOUSE | Cruzado entre manos |
| `ESC` + `DEL` (pulgar izq) | **Bootloader mitad izquierda** | Siempre disponible |
| `BSPC` (fila 1) + `ENTER` (pulgar der) | **Bootloader mitad derecha** | Siempre disponible |

Los combos de clipboard y Escape tienen `require-prior-idle-ms = 150`: si venís tipeando rápido no se disparan solos, solo cuando hacés una micro-pausa. Los combos de bootloader **no** tienen esa restricción, para que siempre respondan.

---

## Flasheo

1. Combo de bootloader de la mitad correspondiente (o doble-tap al reset físico).
2. La mitad monta como unidad USB.
3. Copiar el `.uf2`:
   - Izquierda → `redox_left_studio-nice_nano_v2-zmk.uf2`
   - Derecha → `redox_right-nice_nano_v2-zmk.uf2`
4. Se reinicia sola al terminar la copia.

**Reglas importantes:**

- El keymap vive en la **mitad izquierda** (es la central). Cambios de keymap/conf ⇒ alcanza con flashear la izquierda.
- Cambios en `west.yml` (módulos) ⇒ flashear **ambas** mitades del mismo build.
- `git push` pelado va a Forgejo y **no compila**. Para generar firmware: `git push origin` (GitHub) → GitHub Action → bajar artifacts.

## Si algo sale raro

| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| Mods que se disparan solos al tipear | `tapping-term` u `prior-idle` muy corto para tu velocidad | Subir `tapping-term-ms` en `hml`/`hmr` |
| Mayúsculas que salen tarde o no salen | Shift de HRM demasiado lento | Bajar el término solo para Shift (patrón filterpaper) |
| Teclas viejas "fantasma" tras flashear | Ediciones guardadas desde ZMK Studio | En Studio: *Restore Stock Settings* |
| Las mitades no se hablan | Firmwares de builds distintos | Flashear ambas del mismo run |
| Alt queda pegado tras usar el swapper | Falta una posición en `ignored-key-positions` | Agregarla al behavior `swapper` |

---

## Módulos externos usados

Declarados en `config/west.yml`, revisión `v0.3` heredada del manifest (matchea el release de ZMK):

- **`urob/zmk-adaptive-key`** — permite que MAGIC distinga "vengo de una letra" (repeat) de "vengo en frío" (sticky shift).
- **`urob/zmk-tri-state`** — behavior de tres estados que sostiene el swapper (Alt-Tab) y la smart-mouse.

Caps Word y Key Repeat son **nativos** de ZMK, no necesitan módulo.

---

## Referencias

- [urob/zmk-config](https://github.com/urob/zmk-config) — HRM timeless, magic thumb, smart-mouse
- [Guía de home-row mods](https://precondition.github.io/home-row-mods)
- [Getreuer — Designing a symbol layer](https://getreuer.info/posts/keyboards/symbol-layer/index.html)
