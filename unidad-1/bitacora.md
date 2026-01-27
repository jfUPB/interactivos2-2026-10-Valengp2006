# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 01  22/01/2026

<img width="1352" height="787" alt="Captura de pantalla 2026-01-22 a la(s) 9 19 29 a m" src="https://github.com/user-attachments/assets/2ad9c2a9-0601-47c3-a452-923da527e2a7" />
<img width="583" height="385" alt="Captura de pantalla 2026-01-22 a la(s) 9 19 46 a m" src="https://github.com/user-attachments/assets/ead762d5-3219-4b0e-8668-a22449bf5218" />
<img width="579" height="382" alt="Captura de pantalla 2026-01-22 a la(s) 9 35 18 a m" src="https://github.com/user-attachments/assets/bb4bb7c9-e579-4c94-bb4c-433a310c20a0" />
<img width="1350" height="777" alt="Captura de pantalla 2026-01-22 a la(s) 9 43 48 a m" src="https://github.com/user-attachments/assets/3e600dd3-8bb2-429b-925b-441ad9b18937" />
<img width="1352" height="788" alt="Captura de pantalla 2026-01-22 a la(s) 9 44 49 a m" src="https://github.com/user-attachments/assets/13e279e0-2b02-4315-bb80-118443611ade" />
<img width="1352" height="789" alt="Captura de pantalla 2026-01-22 a la(s) 9 45 08 a m" src="https://github.com/user-attachments/assets/060fb382-bada-4f52-9aa4-486536c77560" />

### Actividad 02

Explicación del caso de estudio:

- Explica detalladamente cómo funciona el sistema físico interactivo del caso de estudio.
- Describe la variación que has propuesto y cómo la has implementado.
- Muestra el código y explica paso a paso cómo reproducir tu variación del caso de estudio.


### Actividad 03

Experimentación son Strudel:

- Documenta cada experimento que realices con Strudel.
- Explica detalladamente cómo funciona cada una de las partes del código que has escrito.

<img width="538" height="352" alt="Captura de pantalla 2026-01-27 a la(s) 8 11 02 a m" src="https://github.com/user-attachments/assets/e7474ea5-88cb-4904-8d0f-c312bff9b01e" />


## Bitácora de aplicación 

### Actividad 03 27/01/2026

```javascript
setcps(0.7);

p1: n("0 2 4 6 7 6 4 2")
  .scale("<c3:major>")
  .distort(0.9)
  .superimpose((x) => x.detune("<0.5>"))
  .lpenv(perlin.slow(3).range(1, 4))
  .lpf(perlin.slow(2).range(100, 2000))
  .gain(0.3);

p2: "<a1>/8".clip(0.8).struct("x*8").note();

p3: n("0@3 2 4 <[6,8] [7,9]>")
.scale("C:minor").sound("piano")

p4: sound("[bd*4,~ rim ~ cp]*<1 [2 4]>")
```

<img width="520" height="409" alt="Captura de pantalla 2026-01-27 a la(s) 9 25 59 a m" src="https://github.com/user-attachments/assets/bc844247-53f2-48d2-8939-276ccdcfb84c" />

## Bitácora de reflexión





