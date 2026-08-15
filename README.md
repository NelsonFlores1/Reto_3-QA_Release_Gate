# Reto_3-QA_Release_Gate
Solución del reto 3 para la certificación 3.

## Descripcion
Sos QA en el equipo del QA Release Gate del curso. Ya tenés métricas de:

- Suite API/UI (pass rate)
- Performance K6 (p95)
- Seguridad ZAP (FAIL-NEW vs WARN-NEW)
- Mutation testing (mutation score)
- Accesibilidad Axe (violaciones *critical*)

Te piden un módulo Python que, con los umbrales del curso, decida si el release pasa o se bloquea.

El esqueleto ya existe. Tu trabajo es implementar 6 funciones marcadas con TODO en src/release_gate.py. Una suite de pytest valida cada una: cuando todo está bien, los 14 tests pasan.

UMBRALES

| Chequeo |	Umbral	| Sesión |
| :--- | :---: | ---: |
| Pass rate	| falla si < 0.95 |	S4/S5
| p95 (ms) |	falla si > 500 |	S6
| ZAP FAIL-NEW	| falla si > 0 (WARN no bloquea) |	S7
| Mutation score |	falla si < 0.90 |	S8
| Axe critical |	falla si > 0	| S7

## Funciones a implementar

1. pass_rate(passed, total)
2. p95_ok(p95_ms, threshold_ms=None)
3. zap_gate(fail_new, warn_new=0, fail_limit=None)
4. mutation_score(killed, total_mutants)
5. a11y_critical_ok(critical_violations)
6. release_gate(metrics) → {"checks": {...}, "passed": bool}

Cada función tiene docstring con casos borde. Leelos antes de programar.

## Cómo correrlo
**Requisito:** uv instalado (mismo del curso).

### Desde esta carpeta (reto-practico/)
```bash
uv sync
uv run pytest -v # al inicio falla: es esperado
```

### Implementa función por función hasta ver:

**14 passed**

Cuando el gate esté listo, también podés verlo decidir:

```bash
uv run python -m src.release_gate
```

### Salida esperada (release de ejemplo con mutation score roto: 40/50 = 0.80 < 0.90):
```bash
{

"checks": {

"pass_rate": true,

"p95": true,

"zap": true,

"mutation": false,

"a11y": true

},

"passed": false

}
```

**Evidencia de que funcionó:** uv run pytest -v → **14** passed (el score es automático).

**Código en GitHub:** https://github.com/dsolisp/curso/tree/main/retos/reto-practico

## Tareas:
### 1. Entregable
- uv run pytest -v → 14 passed
- uv run python -m src.release_gate → JSON con "passed": false y solo mutation en false
- Explicá en una frase por qué ese release se bloquea

### Reglas
- No modifiques tests/test_release_gate.py ni THRESHOLDS.
- Sin librerías externas: solo biblioteca estándar.
- Si un test no te pasa, leé el nombre del test y su assert.

#### Notas del instructor (práctico)
- Solución de referencia: retos/respuestas/release_gate_solucion.py
- Criterio: uv run pytest -v → 14 passed
- El release de ejemplo debe bloquear solo por mutation (score 0.80 < 0.90)
- URL del código: https://github.com/dsolisp/curso/tree/main/retos/reto-practico
