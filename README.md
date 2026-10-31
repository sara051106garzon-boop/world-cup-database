<div align="center">

# Base de datos — Copas del Mundo

[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-12-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Bash](https://img.shields.io/badge/Bash-scripts-4EAA25?logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Licencia: MIT](https://img.shields.io/badge/Licencia-MIT-yellow.svg)](LICENSE)

Modelo relacional de los partidos de las copas del mundo, con carga masiva de
datos desde un CSV y un conjunto de consultas de análisis en SQL.

</div>

---

## Descripción

Proyecto de base de datos relacional sobre la historia de los mundiales de fútbol.
Incluye el esquema, la carga de datos y las consultas que responden preguntas de
negocio: goles totales, promedios, partidos más goleadores y equipos destacados.

## Modelo de datos

```
teams                        games
├── team_id  (PK)            ├── game_id       (PK)
└── name                     ├── year
                             ├── round
                             ├── winner_id     → teams.team_id
                             ├── opponent_id   → teams.team_id
                             ├── winner_goals
                             └── opponent_goals
```

- **`teams`**: un registro por selección, sin duplicados.
- **`games`**: un registro por partido, con las dos selecciones referenciadas por
  clave foránea.

## Archivos

| Archivo | Qué hace |
| :--- | :--- |
| `worldcup.sql` | Volcado completo de la base de datos (esquema + datos) |
| `insert_data.sh` | Lee `games.csv` e inserta equipos y partidos evitando duplicados |
| `queries.sh` | Ejecuta las consultas de análisis y muestra los resultados |
| `games.csv` | Dataset de origen: año, ronda, equipos y goles |
| `expected_output.txt` | Salida esperada de `queries.sh` |

## Cómo usarlo

```bash
# 1. Restaurar el esquema (PostgreSQL)
psql --username=postgres < worldcup.sql

# 2. Cargar los datos desde el CSV
chmod +x insert_data.sh
./insert_data.sh

# 3. Ejecutar las consultas de análisis
chmod +x queries.sh
./queries.sh
```

## Consultas incluidas

- Total de goles de los equipos ganadores y de ambos equipos.
- Promedios de goles, con y sin redondeo.
- Partido con más goles de un solo equipo.
- Cantidad de partidos con más de dos goles del ganador.
- Equipos con más partidos ganados y participación por año.

## Autor

**Sara Garzón** · [github.com/sara051106garzon-boop](https://github.com/sara051106garzon-boop)

## Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).
