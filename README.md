# sdd-kit

Spec-driven development ligero para Claude Code. Documentación mínima y control del desarrollador en cada fase.

- **Poca letra:** una spec corta (happy path y sad paths) y una lista de fases. Nada más.
- **TDD por fase:** cada fase empieza con un test que falla y termina con el test en verde.
- **Pair programming:** al terminar cada fase, Claude se detiene. Tú revisas el código y la prueba manual, das feedback ("baja el botón", "usa tal interfaz") y Claude lo aplica hasta que digas que quedó bien.

## Flujo

| Comando | Cuándo | Resultado |
|---|---|---|
| `/sdd:scan` | Una vez, al instalar en el repo (o cuando cambie el proyecto) | `.sdd/project.md`: stack, arquitectura, convenciones y comando de tests, cada dato con su archivo de origen |
| `/sdd:specify <descripción>` | Por cada cambio | `.sdd/specs/NNN-nombre/spec.md` (simple ~15 líneas, complejo ~50) |
| `/sdd:create-tasks` | Después de la spec | `tasks.md` con fases verticales |
| `/sdd:implement` | Una vez por fase | Construye **una** fase y espera tu aprobación |

Cada fase en `tasks.md`:

```markdown
## Phase 1 — Limpiar tras una búsqueda (covers HP-1)
- [ ] 1.1 Failing test — result: ________
- [ ] 1.2 Implementation — files: ________
- [ ] 1.3 Passing test — result: ________
- [ ] 1.4 Developer approval
```

Claude marca 1.1-1.3. La casilla 1.4 solo se marca con tu aprobación explícita. Las casillas son el estado: si cierras el editor, `/sdd:implement` retoma donde quedó.

## Instalación

Como plugin, en el proyecto donde lo quieras usar:

```
/plugin marketplace add wavila88/sdd-kit
/plugin install sdd@sdd-kit
```

Después ejecuta `/sdd:scan` y revisa `.sdd/project.md`.

## Estructura en tu proyecto

```
.sdd/
├── project.md
└── specs/
    └── 001-clear-search/
        ├── spec.md
        └── tasks.md
```
