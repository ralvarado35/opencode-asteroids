# Asteroids

Clon del clásico arcade **Asteroids** implementado en canvas HTML5 puro, sin dependencias ni bundler.

## Descripción

Nave espacial en un campo de asteroides con envolvimiento de bordes (el espacio es toroidal). Destruye asteroides para sumar puntos: los grandes se parten en medianos, los medianos en pequeños. Incluye power-ups especiales, como el de **Velocidad**, y la **estrella fugaz**, un asteroide rápido y efímero.

## Tecnologías

- **HTML5 Canvas** — renderizado 2D
- **JavaScript (ES6+)** — lógica del juego en un solo archivo `game.js`
- Sin frameworks, sin bundler, sin dependencias

## Cómo correr

Abre `index.html` directamente en el navegador (doble clic), o usa un servidor local:

```bash
npx serve .
```

Luego visita `http://localhost:3000`.

## Controles

| Tecla     | Acción     |
| --------- | ---------- |
| `←` `→`   | Rotar nave |
| `↑`       | Propulsar  |
| `Espacio` | Disparar   |

## Puntuación

| Asteroide      | Puntos |
| -------------- | ------ |
| Grande         | 20     |
| Mediano        | 50     |
| Pequeño        | 100    |
| Estrella fugaz | 150    |

## Características

- 3 vidas con invencibilidad temporal al reaparecer (parpadeo)
- Asteroides se parten en fragmentos más pequeños al ser destruidos
- Partículas de explosión al destruir asteroides
- Power-up **Velocidad**: cada asteroide destruido tiene un 25 % de probabilidad de soltarlo (círculo cian con relámpago); al recogerlo, la nave acelera y gira al doble durante 5 segundos. Se pierde al chocar.
- **Estrella fugaz**: aparece periódicamente (cada 8–14 s como máximo) en un punto alejado de la nave; vuela mucho más rápido que los asteroides normales, no se parte en fragmentos y se esfuma sola a los 7 segundos (parpadea durante los últimos 2 como aviso). Cazarla a tiempo vale 150 puntos; si se deja que se apague, el nivel sigue su curso igualmente.
