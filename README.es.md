<p align="center"><img src="legend/ZONA_GDC_legend_ES.png" width="720" alt="Leyenda ZONA GDC"></p>

# ZONA GDC — LUTs de monitorización para guía de exposición

**Idiomas:** [English](README.md) · [Română](README.ro.md) · Español · Web: <https://gordas.dev/zona-gdc/> · Proyecto compañero: [ETTR GDC](https://github.com/gordasgdc/ettr-gdc) (LUTs de compensación log → log)

[![Licencia: CC BY 4.0](https://img.shields.io/badge/licence-CC%20BY%204.0-blue-blue)](LICENSE)

ZONA GDC es un conjunto de LUTs `.cube` 33×33×33 **solo para monitorización**. Se carga en un monitor, visor o previsualización de grabador externo que reciba la señal log de la cámara; el LUT muestra una imagen Rec.709 de *diagnóstico*: luminancia monocroma con bandas de color en niveles de exposición definidos. Es una ayuda de exposición, **no un look ni una corrección de color**.

## Contrato
- **Entrada:** el perfil log del nombre del archivo (p. ej. `VLog-VG` = V-Log / V-Gamut), rango completo, sin otra transformación aplicada.
- **Salida:** imagen Rec.709 de diagnóstico, codificada con la OETF BT.709, rango completo. **No** es log → log (eso lo hace ETTR GDC).
- Aplícalo **una sola vez**. Si el monitor o la cámara ya aplican un LUT/transformación, desactívala o tendrás una doble transformación.
- Solo monitorización: no lo uses para etalonar ni lo grabes a propósito en la grabación principal. Un `.cube` no puede imponer «solo monitor»; según el enrutado del dispositivo, un LUT de monitorización puede aparecer también en las salidas externas grabadas — comprueba tu dispositivo.

## Qué significan los colores
Los pasos se miden **después** de la compensación de monitorización respecto al gris 18 % (`Y = luminancia de la señal scene-linear ÷ 2^comp`).

| Color | Significado | Intervalo |
|---|---|---|
| Rojo | tope del rango de código de la señal log **original** | cualquier canal con código ≥ 31/32 |
| Amarillo | blanco de pantalla alcanzado | por encima de +2,47 pasos (100 % señal BT.709); nada se comprime |
| Rosa | referencia **tonal** de piel | +0,79 … +1,45 pasos = 55–70 % señal BT.709 (convención de trabajo, no estándar; no detecta piel) |
| Verde | nivel de carta gris | −0,4 … +0,4 pasos = 35–48 % señal BT.709 |
| Azul | sombras profundas | por debajo de −5 pasos (≈ 2,5 % señal BT.709) |
| gris | el resto | luminancia monocroma BT.709 (contexto) |

El rosa es solo un rango tonal: cualquier pared brillante o cielo en ese rango también se vuelve rosa. «Amarillo» significa que la **imagen de monitorización** recortaría; no es una afirmación sobre el recorte del sensor (no se usan datos de cámara). El rojo se evalúa sobre los códigos originales de entrada, así que el aviso sobre el límite real de la señal no desaparece al compensar.

## Compensación (nombre de archivo `…_MONITOR-<paso>EV.cube`)
`0EV` analiza la imagen tal cual. `m1EV` la analiza tras oscurecerla −1 paso: el gris capturado a +1 paso cae sobre la referencia de gris. Igual `m0_5EV` (−0,5) y `m1_5EV` (−1,5). Sin +0,5 EV en esta versión.

## Precisión medida (33³, interpolado — ver `INDEX.md`, `audit.json`)
La auditoría evalúa el cubo **interpolado** (trilineal y tetraédrico, rampas de 0,01 pasos) frente al modelo analítico.
- Posición del borde de banda en rampas neutras (grises): peor 0,18 pasos, típico 0,06 pasos (tetraédrico).
- Las bandas son estrechas respecto a la rejilla: dentro de la banda de gris de 0,8 pasos el color alcanza 55–85 % de cobertura según el perfil (el resto es mezcla con la imagen monocroma). 4 perfiles con la cobertura más baja o colores saturados no representables son **experimentales**: `LogC4_AWG4`, `Film-Gen5_BMD-WG-Gen5`, `DaVinci-Intermediate_DWG`, `ACEScct_AP1`.
- Colores muy saturados: los bordes de banda pueden desplazarse varios pasos (peor color de prueba ≈ 7 pasos); la causa no se investigó más. No confíes en los bordes de banda para objetos muy saturados.
- El error puntual en 8 bits es grande (hasta ~100 códigos) justo en los bordes de banda, porque las bandas tienen bordes marcados y la rejilla es 33³; lejos de los bordes es pequeño. Los bordes se mueven con suavidad con la exposición (no se encontró parpadeo: 0,7 % de los píxeles cambian de banda entre fotogramas en un clip en movimiento a −1 EV).
- No probado en monitores, visores ni grabadores externos físicos. Los umbrales exactos **no están garantizados** en hardware no probado (el dispositivo puede remuestrear, recortar o usar su propia interpolación).

## Contenido
28 perfiles por marca (Sony, Canon, Panasonic, ARRI, RED, Blackmagic, Nikon, Fujifilm, Apple, FilmLight, DaVinci, ACES), 4 LUTs cada uno; `Sony/_Viewfinder_6char/` contiene copias con nombre corto para visores con nombres de 6 caracteres. `INDEX.csv/md`, `STATS.json`, `catalog.json`, `audit.json`, `MANIFEST_SHA256.txt`, imágenes de leyenda RO/EN/ES. No incluido: GoPro Protune (sin fuente verificada de gama).

## Licencia y atribución

Las LUTs pregeneradas y la documentación de esta distribución se licencian bajo **Creative Commons Atribución 4.0 Internacional (CC BY 4.0)** — https://creativecommons.org/licenses/by/4.0/deed.es (`LICENSE`). Puedes usarlas, copiarlas, modificarlas y redistribuirlas, también con fines comerciales, **siempre que cites a «Dumitru Cristinel Gordas — ZONA GDC», enlaces la licencia e indiques si hiciste cambios.** Componentes de terceros y procedencia: `docs/PROVENANCE.md`. Proyecto independiente, sin afiliación ni respaldo de ningún fabricante de cámaras o software; los nombres de marca solo identifican los formatos que publican.
