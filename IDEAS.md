# Inspiración maker — Teclado Redox split BT (ZMK)

**Fecha:** 2026-08-02 · Fuentes: GitHub, YouTube, Reddit/HN, Hackster/Instructables (4 agentes en paralelo)

**Sujeto:** Redox split BT, 70 teclas, nice!nano v2, ZMK + Studio, host Windows.
**Ya implementado hoy:** HRM GASC "timeless" (urob), combos clipboard ZXCV (undo/cut/copy/paste), Caps Word (Shift+Shift), Esc (Q+W), combos bootloader por mitad, capas symbol/nav/adjust.

**Dato clave del relevamiento:** no existe ningún config Redox+ZMK con tracción (todos 0⭐). La jugada correcta es la que ya venís haciendo: portar patrones de los configs top de 34-42 teclas (urob, caksoylar, Miryoku) — con la ventaja de que al Redox le sobran teclas físicas para lo que ellos resuelven con malabares.

---

## 1. El pulgar "mágico" y teclas inteligentes ⭐ lo más elogiado de la comunidad

- **Magic key de urob** ([urob/zmk-config](https://github.com/urob/zmk-config), ~1.4k⭐): UNA tecla de pulgar que hace 4 cosas según contexto — **repeat** después de letras, **sticky-shift** después de otras teclas, shift en hold, **caps-word** en doble tap. Es el feature más citado en writeups de la comunidad.
  **Cómo aplicarlo acá:** tu tecla libre del pulgar izquierdo es la candidata perfecta. Resuelve de un saque el repeat key (que te interesó) + sticky shift, sin gastar más teclas.
- **Layer-lock desde el pulgar** ([sunaku/Glove80](https://sunaku.github.io/moergo-glove80-keyboard.html), "400+ iteraciones"): convertir una capa momentánea en pegajosa a demanda, para operaciones largas en nav sin sostener el pulgar.
- **Regla de oro comunitaria** (Ask HN [split keyboards](https://news.ycombinator.com/item?id=35637041)): cada pulgar alcanza cómodo **2-3 teclas**; las exteriores del cluster son "premium/raras". No llenar el thumbcluster porque está.

## 2. Smart layers — capas que se apagan solas

- **Numword** ([urob/zmk-auto-layer](https://github.com/urob/zmk-auto-layer)): capa numérica que se activa y se **desactiva sola** al tipear algo que no es número. Nadie queda "atrapado" en la capa.
- **Smart-mouse por combo** (urob): capa mouse activada con combo `W+P`, se cierra sola al tocar una tecla no-mouse.
  **Cómo aplicarlo acá:** ES la respuesta a tu pregunta "¿cómo manejo el mouse?" — en vez de gastar el pulgar libre en `&mo mouse`, combo W+P → capa mouse (puntero+scroll+clicks como la de enero) que se apaga sola. La comunidad valora el mouse layer más de lo esperado (evita el viaje al mouse para scrollear).
- **Tri-layer nativo** ([caksoylar/zmk-config](https://github.com/caksoylar/zmk-config)): `conditional_layers` — Nav+Sym juntos activan una tercera capa (así ya funciona tu adjust, pero declarativo y sin teclas `&mo 3` sueltas).

## 3. Combos, morphs y micro-features de productividad

- **Swapper / Alt-Tab de una tecla** ([dhruvinsh/zmk-tri-state](https://github.com/dhruvinsh/zmk-tri-state)): mantiene Alt "virtualmente" hasta que tocás otra cosa — Alt-Tab con un dedo, sin retorcer la mano. En Windows es oro; elogio desproporcionado vs. costo.
- **Antecedent morph** ([englmaxi/zmk-config](https://github.com/englmaxi/zmk-config)): la tecla cambia según la anterior — arma `->`, `!=`, `<=`, `=>` automáticamente. Truco de programador poco conocido.
- **Select-word / select-line** (sunaku, base de Getreuer): macro que selecciona la palabra/línea bajo el cursor. Barato y muy usado.
- **Clipboard espejado en la mitad derecha** (sunaku + [chapmanb/zmk-34key-split](https://github.com/chapmanb/zmk-34key-split)): copy/paste también accesible con una sola mano derecha... o mejor: con la IZQUIERDA sola cuando la derecha está en el mouse. Tus combos ZXCV ya cubren ese caso ✓ — evaluá si querés el espejo para el caso inverso.
- **Leader key** ([urob/zmk-leader-key](https://github.com/urob/zmk-leader-key), patrón en [rafaelromao/keyboards](https://github.com/rafaelromao/keyboards)): secuencias tipo vim (leader → "b" → "1" = BT perfil 1). Ideal para acciones raras (Bluetooth, bootloader alternativo, unicode) sin gastar teclas ni capas.
- **Validación de lo hecho hoy:** el fix comunitario para "los combos disparan solos tipeando rápido" es `require-prior-idle-ms` **también en combos** — ya lo aplicamos a los ZXCV y a Q+W ✓.

## 4. Capa de símbolos — la revisión más barata con más retorno

[Getreuer, "Designing a symbol layer"](https://getreuer.info/posts/keyboards/symbol-layer/index.html) (autor de Caps Word en QMK):
- Símbolos frecuentes en home row; raros a las esquinas.
- **Nunca** símbolos que se doble-tapean (`==`, `++`) en el meñique.
- Bigramas de programación (`!=`, `<=`, `->`, `=>`) como **inward rolls** o morphs.
- Mod-morphs útiles de urob: coma→punto y coma con shift, punto→dos puntos.
**Cómo aplicarlo acá:** auditar tu capa symbol/nav actual contra estos criterios (hoy los símbolos están donde cayeron, no donde rinden).

## 5. Media y volumen

- **Capa Media de Miryoku** ([manna-harbour/miryoku_zmk](https://github.com/manna-harbour/miryoku_zmk)): volumen/play/pause + selección BT + salida USB/BLE en una capa propia de acceso directo (un hold de pulgar), no escondida.
  **Cómo aplicarlo acá:** hoy tu media está enterrada en adjust (nav + segunda tecla + home row). Moverla a un acceso de un solo hold — p.ej. hold de la tecla libre del pulgar (si no va la magic key ahí) o un combo — resuelve tu pregunta "¿y el volumen, play/pausa?".

## 6. Afinado de HRM (para después de unos días de uso)

- **HRM por dedo** (sunaku): umbrales distintos según fuerza del dedo (meñique ≠ índice).
- **Shift con tapping-term corto separado** ([filterpaper/zmk-config](https://github.com/filterpaper/zmk-config)): el shift de HRM con timer más corto (~170ms) para que las mayúsculas salgan rápidas, el resto sigue timeless.
- **Modos de fallo a vigilar** ([precondition guide](https://precondition.github.io/home-row-mods), [HN](https://news.ycombinator.com/item?id=38507116)): misfires en rolls rápidos, letras dobles en vez de mayúscula. El hábito que más ayuda: taps cortos y secos. Si algún dedo molesta siempre → ese mod se muda al pulgar.
- **Capa gaming sin HRM**: higiene básica si alguna vez jugás con este teclado (`&tog` a una capa QWERTY plana).

## 7. Herramientas y estructura del repo

- **[caksoylar/keymap-drawer](https://github.com/caksoylar/keymap-drawer)**: autogenera el DIBUJO del keymap (SVG) en CI en cada push — se acabó el comment ASCII desactualizado.
- **[urob/zmk-helpers](https://github.com/urob/zmk-helpers)**: posiciones nombradas (`LT0`, `RM1`) y macros `ZMK_COMBO`/`ZMK_HOLD_TAP` de una línea; `combos.dtsi` separado del keymap.
- **Gotcha ZMK Studio**: combos, hold-taps custom y módulos son build-time — Studio no los edita. Plan sano: capas base retocables en Studio, features avanzadas en el `.keymap`.
- **[KeymapDB](https://keymapdb.com/)**: base de datos filtrable de keymaps para seguir minando.
- Canal 100% del nicho: [Ben Vallack's Keyboards](https://www.youtube.com/@BenVallacksKeyboards); su [video de 9 features ZMK](https://www.youtube.com/watch?v=NAUxTR4vGys) es el mejor "menú" en video.

---

## Quick wins vs. Aspiracional

**Quick wins (un rebuild, riesgo bajo):**
1. **Magic key en el pulgar libre** — repeat + sticky-shift + caps-word en una tecla (módulos de urob).
2. **Capa mouse smart por combo W+P** — recupera el mouse sin gastar teclas, se apaga sola.
3. **Media a un hold directo** — sacar volumen/play de adjust.
4. **Swapper Alt-Tab** — módulo tri-state, una tecla en nav.
5. **Mod-morphs de coma/punto** y auditoría Getreuer de la capa symbol.

**Aspiracional (requiere iterar/acostumbrarse):**
- Leader key para BT/acciones raras · antecedent morph de bigramas (`->`, `!=`) · select-word/line · HRM por dedo · tri-layer declarativo · keymap-drawer en CI · capa gaming.

## Recomendación (por dónde arrancaría yo)

1. **Magic key en el pulgar libre izquierdo** — máximo retorno por tecla: te da el repeat que te interesó + sticky shift + caps word contextual, en la única tecla libre que tenés, con módulos probados por miles.
2. **Smart-mouse por combo W+P** (+ clicks con tap-dance si querés: tap=click izq, doble=derecho) — responde tu pregunta del mouse sin sacrificar el pulgar.
3. **Media a acceso directo** — es tu queja implícita más concreta (volumen/play hoy están a 3 teclas de distancia).

Después de una semana de uso real de los HRM, recién ahí: afinado por dedo / shift rápido (sección 6).

## Notas de confianza

- Links de GitHub, Getreuer, precondition, sunaku y HN: **verificados** por las agentes.
- Links de YouTube: URLs reales de búsqueda, pero canal/año aproximados (YouTube bloquea el fetch del contenido).
- Reddit bloquea el crawler por completo: los insights "de comunidad" vienen de los referentes cuyos posts circulan en r/ErgoMechKeyboards (urob, Getreuer, sunaku) y de HN, no de permalinks de Reddit.
- Hackster/Instructables: casi nada aplicable a keymaps (esperable, son plataformas de hardware).
