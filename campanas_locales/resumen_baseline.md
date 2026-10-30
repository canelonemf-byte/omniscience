# OMNISCIENCE — Línea base de evidencia (18-oct-2026)

> **Actualización 18-oct-2026 20:18 (UTC+2):** C-VIB-001 (VP-09…VP-15) pasa a **E3** mediante reimplementación reproducible (6/6 hipótesis superadas, 2 ejecuciones byte-idénticas). Conteo actual: E0 19 · E1 19 · E2 2 · E3 7 · E6[ext] 9 · — 2. Ver `log_avances.md`. Las tablas de abajo reflejan la línea base inicial.

**Fuentes revisadas:** `gh/repos/omniscience/` (README, LICENSE, 2 `.tex`, 2 `.md`; 1 commit «Importación inicial desde Google Drive»), `agsgpt/ags-core-v3.6/knowledge/omniscience/` (**copia idéntica byte a byte** del repo, sin `.git`), `agsgpt/.../projects.json` (solo metadatos: MIT, 6 archivos), `gh/plan.json`/`report.json` (inventario Drive: 4 incluidos, 9 pendientes, 2 excluidos) y `gh/content/*.json` (copias de los mismos documentos + afirmaciones fonónicas de proyectos adyacentes). Registro completo: `evidence_register.csv` (58 filas). Escala: `escala_E0_E6.md`.

## Estado del proyecto
OMNISCIENCE es hoy una **arquitectura documentada** con una sola campaña ejecutada (C-VIB-001: modelos vibratorios canónicos 1D, declarada nivel 3). En la caja **no hay código, figuras, datos, tests ni manifiestos de procedencia**: todo eso está en Drive (`grok-workspace-2.zip`, 172 MB, carpeta `figs`). Ningún cálculo sobre un material real (relajación, E_hull, Phonopy, κL) se ha hecho todavía. Universal Matter está en fase de diseño; el Phonon Engine tiene un banco de calibración con resultados de libro de texto. Los propios documentos son honestos al respecto (máx. nivel 3, sin experimento ni réplica).

## Distribución por nivel (escala 0–6 de los documentos)
| Ámbito | E0 | E1 | E2 | E3+ propio | E6 [externo] | — | Total |
|---|---|---|---|---|---|---|---|
| Universal Matter (UM) | 6 | 3 | 0 | 0 | 3 | 0 | 12 |
| Vibrational/Phonon (VP) | 5 | 7 | 8 | 0 | 6 | 0 | 26 |
| Plataforma + otros motores (PL, OT) | 4 | 9 | 0 | 0 | 0 | 2 | 15 |
| Proyectos adyacentes con fonones (ADJ) | 4 | 0 | 1 | 0 | 0 | 0 | 5 |
| **Total** | **19** | **19** | **9** | **0** | **9** | **2** | **58** |

E6 = física establecida adoptada (no verificada por el proyecto). **Ningún resultado propio está en E3 o más verificable en la caja**; C-VIB-001 (declarado E3) queda en E2 hasta recuperar y re-ejecutar los artefactos.

## Top 5 lagunas / riesgos
1. **Artefactos ausentes:** la evidencia E3 declarada no es reproducible desde la caja (sin scripts, figuras, SHA256SUMS ni pytest; «datos crudos no empaquetados» según la propia checklist).
2. **Cero cálculos sobre materiales reales:** Universal Matter y MV1 (relajación, E_hull, fonones 3D, modos imaginarios, κL) no han empezado; C-MAT-001 sigue en E1 sin pre-registro.
3. **Error de cita (alucinación bibliográfica, el riesgo nº1 que el propio doc enumera):** Nature 623:514 (2023) se atribuye a «S. M. Montgomery et al.»; Crossref da Yun Kai … Carlos M. Portela. Los 5 DOI resuelven, pero no existe audit_log.csv.
4. **Inconsistencias documentales:** escala 0–6 vs 0–7 entre documentos; licencia MIT en LICENSE vs «licencia pendiente, no redistribuir» en la Publicación.
5. **Supuestos físicos a acotar:** κL en RTA (infraestima en materiales de alta κ; puede requerir 4 fonones); Lindblad para FMO (poco fiable frente a HEOM); Tc vía Allen–Dynes (falla en MgB2). Y proyectos adyacentes con afirmaciones que **contradicen la física** (antibiótico por resonancia de flagelos; qubits superconductores a 1–2 K) o que etiquetan simulación como validación celular (GlyD-QSense), que podrían contaminar la credibilidad si se vinculan al Phonon Engine.

## Top 5 acciones recomendadas (prioridad Universal Matter + Phonon Engine)
1. **Recuperar y reproducir C-VIB-001** (descargar el zip de Drive a la caja, `sha256sum -c`, re-ejecutar con semilla 7, tests analíticos con z<3) → E2→E3 verificable. Después, reimplementación independiente → E5.
2. **Primer benchmark real MV1 (Si y NaCl):** relajación → Phonopy (desplazamientos finitos) → dispersión vs neutrones publicados → modos imaginarios con batería de convergencia → manifest PROV/RO-Crate. Sería la primera evidencia E3 sobre un material real.
3. **Pre-registrar C-MAT-001:** umbrales de E_hull por química (Sun et al. 2016: mediana 15, p90 67 meV/átomo), criterios de falsación y lista de candidatos de κL bajo conocido (PbTe, SnSe) como control.
4. **κL con phono3py (RTA vs LBTE)** en Si/diamante para documentar el dominio de validez de κL=(1/3)ΣCv²τ antes de usarla en diseño inverso.
5. **Higiene de evidencia:** corregir la cita de Nature 623, crear audit_log.csv vía Crossref, unificar la escala (0–6) y la licencia, y aislar los proyectos adyacentes con afirmaciones E0 contrarias a la física.

## Qué se puede automatizar como tarea recurrente
- **Auditoría de citas semanal:** resolver todos los DOI/URL de los `.tex` en Crossref, comparar autores/año/volumen y señalar discrepancias (como la de Nature 623).
- **Comprobación de reproducibilidad:** al llegar artefactos, re-ejecutar scripts de campaña con semilla fija, verificar hashes y marcar «inconcluso» si cambia una figura (regla del propio documento).
- **Sincronía de copias:** diff repo ↔ `agsgpt/knowledge/omniscience` ↔ Drive (hoy idénticas).
- **Re-cálculo del registro:** regenerar conteos por nivel y avisar de cualquier afirmación que suba de nivel sin artefacto asociado.
- **Radar bibliográfico** mensual (fonones topológicos, metamateriales fonónicos, κL ML, E_hull/sintetizabilidad) con enlaces verificados, para alimentar la columna «literatura».
- **Filtro de afirmaciones vibratorias** en documentos nuevos: marcar «frecuencia propia del elemento», «cuántico» sin pico Raman asignado o simulación etiquetada como validación (VP-01, VP-24).
