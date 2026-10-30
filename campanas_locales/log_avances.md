# Log de avances — OMNISCIENCE

## 2026-10-18 20:18 (UTC+2) — C-VIB-001 reproducida (reimplementación) y pre-registro C-MAT-001
- **Recuperación desde Drive: FALLIDA.** La carpeta `figs` (id 17tWKDUDiaFEBc_IAumtLVJQrq4LKky8n) se listó (11 imágenes: 01–09, 11, 12) pero `DownloadFile` respondió «No connected service can serve files this turn». `grok-workspace-2.zip` (172 MB) tampoco se pudo descargar. Los scripts originales (simular_vibraciones.py, animar_modos.py) y SHA256SUMS.txt no existen como archivos sueltos en Drive. No se verificó ningún hash original.
- **Alternativa:** reimplementación mínima `cvib001_repro.py` (sha256 e796ae2e…f4) de H1–H6 con tolerancias declaradas; entorno: Python 3.13.5, numpy 2.4.4, scipy 1.18.1, matplotlib 3.11.2; semilla 7.
- **v1.0:** H4 y H5 fallaron por diseño del arnés (H4: comparar ω tras sqrt cerca de ω=0; H5: exigir ≥3 gaps cuando la geometría de igual tiempo de tránsito cierra los gaps pares). Corregido en v1.1 (comparar ω²; ≥2 gaps; ARPACK con v0 fijo). Cambio post-hoc **declarado**; resultados de v1.0 guardados en C-VIB-001/results_v1.0_criterios_originales.json. Los criterios de falsación del documento original ya se cumplían en v1.0.
- **v1.1: 6/6 PASS**, 2 ejecuciones **byte-idénticas** (PNG + results.json).
  - H1 err amplitud 7.6e-12, fase 1.5e-11 rad, Q 9.975/10 · H2 picos 180.00/320.00 Hz, inicio burst 2.208 s, contraste 24 dB · H3 err f_n 9.2e-5, nodo 1e-13 · H4 gap 0.4608 (0.9535→1.4142), 0 modos en el gap · H5 2 gaps, |T|² en centros 1.4e-14, conservación 2.5e-14 · H6 err E_n 2.1e-5, nodos 0–9.
- **Registro:** VP-09…VP-15 pasan de E2 a **E3** (reimplementación reproducible; no réplica independiente, no medida). VP-17 (MP4) sigue en E2. Conteo total: E0 19 · E1 19 · E2 2 · E3 7 · E6[ext] 9 · — 2.
- **C-MAT-001:** borrador de pre-registro `prereg_C-MAT-001.md` (paso E1→E2 con Phonopy + potencial ML sobre 9 materiales de referencia, con 2 controles negativos). Propuesto, NO ejecutado.
- **Pendiente:** reconectar Google Drive con soporte de descarga para recuperar el zip, verificar SHA256SUMS y comparar las figuras originales con las nuevas (paso hacia E5).

## 2026-10-18 21:30 (UTC+2) — C-MAT-001 ejecutada (pre-registrada)
- **Referencias verificadas antes de ejecutar** (enmiendas §8 del prereg):
  - Si 520 → 520.2 cm⁻¹
  - GaAs TO 268 → 269 cm⁻¹
  - MgO TO 401 → 396 cm⁻¹
  - PbTe TO 18.0 cm⁻¹ (nuevo)
  - C 1332 cm⁻¹ (sin cambio)
  - NaCl: no verificada; cuenta como no superada
- **Prereg congelado** a las 21:16 (sha256 efb5f872…ea90) y sin cambios posteriores.
- **Modelo:** MACE-MP-0 medium (ckpt sha256 01bfe221…5845), float64, CPU; sin CHGNet. Pila: ASE 3.29.0, Phonopy 4.8.3, mace-torch 0.3.16.
- **Resultados:**
  - H-MAT-1 **PASA**: 9/9; controles negativos SrTiO3 −2.36 THz y BaTiO3 −6.41 THz.
  - H-MAT-2 **FALSADA**: 0/6.
    - Si −28.3 %, C −12.0 %, GaAs −21.0 %, MgO −16.0 %, PbTe +194 %.
    - NaCl −9.9 % frente a una referencia secundaria; no cuenta.
  - H-MAT-3 **PASA**: 0 materiales inconclusos.
- **Observación:** SnSe relajó a Fm-3m, así que su veredicto no corresponde a la fase Pnma. En el análisis de sensibilidad queda 8/9 y H-MAT-1 sigue pasando.
- **Lectura:** el ablandamiento sistemático de MACE-MP-0 coincide con lo descrito en doi:10.1038/s41524-024-01500-6. Este análisis es exploratorio.
- **Registro:**
  - UM-08 E1→**E2**.
  - UM-07 E0→E1 (flujo parcial).
  - VP-04: justificación actualizada.
  - Conteo: E0 18 · E1 19 · E2 3 · E3 7 · E6[ext] 9 · — 2.
- **Archivos:** C-MAT-001/ (results.json, provenance_C-MAT-001.json, requirements.lock, informe_resultados.md, figs/, out/, code/).

## 2026-10-18 22:00 (UTC+2) — Escaneo de innovación (cartera_innovacion)
- **Cartera:** 16 candidatas en materiales, química, biología y tecnología, más el re-chequeo de ADJ-01/02/03. Originalidad comprobada con ~15 búsquedas web (2023–2026). **Ninguna idea es «nueva»**: 7 son parciales y 9 conocidas.
- **Top 5:**
  1. INN-01 σᴬ-compuerta (18)
  2. INN-03 doble pozo frente a Tc (12)
  3. INN-05 solapamiento de DOS y TBC (12)
  4. INN-11 Akhiezer en HBAR (12)
  5. INN-02 escalado anti-ablandamiento (9)
- **Exploratorios ejecutados** (CPU, MACE-MP-0 medium; marcados como no confirmatorios):
  - X1 σᴬ: PbTe 0.46 > NaCl 0.39 > Si 0.26; Si sesgado frente a DFT 0.15.
  - X2 pozos: ρ 0.97 frente a Tc (n = 5).
  - X3 solapamientos de DOS.
  - X4 flagelo: Q ≈ 3×10⁻⁴, ADJ-02 refutado.
  - X5 escalado LOO: −14…+12 %, insuficiente.
- **Pre-registros** (borradores, sin congelar): prereg_INN-01, prereg_INN-03, prereg_INN-05. Todos exigen materiales nuevos, porque se redactaron después de ver los exploratorios.
- **Registro:**
  - Filas nuevas INN-01/03/05/02 en E2 (exploratorio) e INN-11 en E1.
  - Notas de re-chequeo añadidas a ADJ-01/02/03.
- **Derechos:** texto, código y figuras propios; las fuentes solo se citan (nota originalidad_y_derechos).
- **Archivos:** innovacion/

## 2026-10-18 23:45 (UTC+2) — INN-03 confirmatorio (doble pozo frente a Tc)
- **Prereg:** congelado con enmiendas B1–B4 (sha256 839eeaec…728a). El `.sha256` existe desde 23:15:23 y el cálculo empezó a las 23:34:51. Referencias revalidadas: 9 DOI en Crossref; Tc de BiFeO3 y CsGeX3 comprobadas en los resúmenes. Sin enmiendas nuevas.
- **Conjunto** (n = 10, disjunto de X2): BiFeO3, CsGeCl3, CsGeBr3, CsGeI3, PbZrO3, PbHfO3, CaTiO3, BaZrO3, SrZrO3, BaSnO3.
- **Resultados con los criterios originales:**
  - H-F1: ρ = 0.376, FALSADA.
  - H-F2: 6/10, FALSADA.
  - Controles negativos: CaTiO3 falla, BaZrO3 pasa.
  - Sensibilidad 3×3×3: estable.
  - **Veredicto: FALSADA.**
- **Réplica:** ΔE_rel idéntico. Sin desviaciones.
- **Registro:** INN-03 sigue en E2, ahora confirmatorio negativo.
- **Archivos:** innovacion/INN-03/.

## 2026-10-19 00:45 (UTC+2) — INN-05 confirmatorio (solapamiento de DOS frente a TBC)
- **Prereg:** congelado con enmiendas C1–C6 (sha256 4d8f3ba1…e4d2). El `.sha256` existe desde ≤ 23:15:23; la ejecución fue de 23:34:51 a 23:36:34. Congelación anterior al cálculo. DOI de Koh 2020 y Costescu 2003 comprobados en Crossref.
- **Conjunto:** Al, Co, Ru y TiN sobre Al2O3 (n = 4); controles Al|Al y C|Pb.
- **Resultados con los criterios originales:**
  - H-T1: NO EVALUABLE (n = 4 < 8).
  - H-T2: NO EVALUABLE.
  - H-T3: NO EVALUABLE (sin DOS DFT).
  - Las tres cuentan como no superadas. Controles OK.
  - **Veredicto: NO SUPERADA (no evaluable), no falsada.**
- **Descriptivo:** ρ(O, TBC) = 0.77 = ρ(AMM, TBC), Δρ = 0. Con la misma TBC, O varía unas 9 veces.
- **Desviación D1 (procedimiento):** una ejecución previa a la restauración no se puede situar respecto a la congelación. La confirmatoria la reproduce con diferencias ≤ 10⁻⁹ y el veredicto no depende de los valores.
- **Registro:** INN-05 sigue en E2 (exploratorio). Conteo: E0 18 · E1 20 · E2 7 · E3 7 · E6 9 · — 2.
- **Archivos:** innovacion/INN-05/.

## 2026-10-19 01:00 (UTC+2) — INN-01 confirmatorio (σᴬ MACE como compuerta armónica)
- **Prereg:** congelado con enmiendas A1–A8 (sha256 180ae31a…9663). El `.sha256` existe desde ≤ 23:15:23. Hashes del código guardados a las 23:43:39 y verificados. Cálculo armónico de 23:43:39 a 23:48:37; MD de 23:49 a ~00:53. Congelación anterior al cálculo. Valores de Knoop 2020 revisados de nuevo en la fuente.
- **Conjunto:** CuCl, CuBr, CuI, AgI y AgBr (ZB); AgCl, AgBr, AgI y NaBr (RS); control Si. AgI-RS excluido por A4, así que n = 8.
- **Resultados con los criterios originales:**
  - H-A1: NO EVALUABLE (n < 10, y también n < 9 con la enmienda).
  - H-A2: NO EVALUABLE.
  - H-A3: NO EVALUABLE (A5).
  - **Veredicto: NO SUPERADA (no evaluable).**
- **Descriptivo:**
  - ρ = 0.50, IC95 [−0.42, 0.92]; |sesgo| 0.122. Habría fallado.
  - Si: 0.227 frente a 0.15.
  - MD completa: CuI 0.571 y AgCl 1.085.
  - No pre-registrado: ρ frente a aiMD = −0.04 (n = 7).
- **Desviaciones:** ninguna. La MD terminó; no hubo que cortarla.
- **Registro:** INN-01 sigue en E2 (exploratorio).
- **Archivos:** innovacion/INN-01/.

## 2026-10-19 09:20 (UTC+2) — C-MAT-002 (termodinámica armónica frente a JANAF; tres calculadores en Si)
- **Prereg:** congelado a las 09:10:31 (sha256 af9fd6d7…aa70), antes de cualquier cálculo. Referencias: NIST-JANAF Si-001, Mg-008, Cl-053 (Cp y S a 100, 200 y 298.15 K), descargadas hoy.
- **Calculadores:** MACE-MP-0 medium (mismo checkpoint que C-MAT-001), Stillinger–Weber 1985 y Kumagai 2007 (matscipy 1.3.1). Phonopy 4.8.3, 0.01 Å, 2×2×2 y 3×3×3, malla 20³.
- **Resultados (criterios originales):**
  - S298 MACE: Si +28 %, MgO +22 %, NaCl +5 % → H-TH-1 **FALSADA**.
  - H-TH-2 **PASA** (sobreestima en los 3), H-TH-3 **PASA** (error de Cv a 100 K +41/+45/+6 % frente a +9/+7/−5 % a 298 K), H-TH-4 **PASA** (ΔS_obs/ΔS_pred = 0.64 y 0.68).
  - Si: S298 MACE 24.1 · JANAF 18.8 · SW 16.5 · Kumagai 15.0 → H-X-1 **PASA**, H-X-3 **PASA** (horquillado), H-X-2 **FALSADA** (TO SW +14 %, Kumagai +18 %).
  - SW da TO-Γ 594.8 cm⁻¹; la literatura publica 594.76 cm⁻¹ → comprobación externa del flujo con otro calculador.
  - H-X-4 **FALSADA** en v1.0 (S298 MACE Si 24.147 frente a 24.120 entre ejecuciones).
- **Desviaciones:** D1 (post hoc): los modos acústicos en Γ (~1e-7 THz) entraban en las sumas térmicas; con exclude_gamma_acoustic=True (v1.1) hay 2 ejecuciones idénticas byte a byte, efecto ≤0.11 %. D2: la normalización por Cv(3000 K)/3R infla ≤0.36 %. Ningún veredicto cambia.
- **Originalidad:** cualitativamente **ya conocido** (Loew et al. 2025 doi:10.1038/s41524-025-01650-1; Deng et al. 2025 doi:10.1038/s41524-024-01500-6; escalado 1.18 en PMC12080109). **Parcial:** el factor de transferencia del ablandamiento TO a la entropía (~0.65) frente a datos experimentales no apareció en una búsqueda rápida.
- **Registro:** UM-10 E0→**E2**; nueva fila UM-13 (C-MAT-002) en **E2**; UM-07 sigue en E1 con justificación ampliada. Conteo: E0 17 · E1 20 · E2 9 · E3 7 · E6 9 · — 2 (64 filas).
- **Archivos:** C-MAT-002/ (prereg, código, out/, results.json, results_sensibilidad_v1_1.json, provenance_C-MAT-002.json, figs/fig_S_vs_JANAF.png, informe_resultados.md).
- **Próximo paso:** prereg C-MAT-003 con n≥8 sólidos JANAF, un uMLIP más reciente (MatterSim/SevenNet) y corrección cuasiarmónica.

## 2026-10-19 10:05 (UTC+2) — C-MAT-003 (QHA y tres potenciales universales frente a JANAF, 11 sólidos)
- **Prereg:** congelado a las 09:31:06 (sha256 2d9a1256…fc96), antes de cualquier cálculo con los materiales del estudio. La prueba de humo solo usó Ge y Cu. Hashes de código y checkpoints fijados a las 09:35:21.
- **Materiales:** Si, MgO y NaCl (anclas), más LiF, NaF, KCl, KBr, CaO, CaF2, Al2O3 y BeO. Tablas JANAF verificadas con CODATA, Robie y Hemingway 1995 (doi:10.3133/b2131) y OSTI 4314983 para LiF. Desviación máxima de S298: 0.56 %.
- **Potenciales:** MatterSim v1.0.0-5M (principal), SevenNet-0 y MACE-MP-0 (línea base). Phonopy 4.8.3, QHA con 10 volúmenes (0.96–1.14) y EOS Vinet. Todo en CPU.
- **Resultados con los criterios originales:**
  - H-Q1 **FALSADA**: con MatterSim y QHA, 2 de 11 quedan dentro de ±10 %.
  - H-Q2 **FALSADA**: MARE de S298 = 11.8 %.
  - H-Q3 **FALSADA por poco**: MARE armónica 7.4 % con MatterSim frente a 14.0 % con MACE; el error baja un 47 % y se pedía un 50 %.
  - H-Q4 y H-Q5 **FALSADAS**: la QHA empeora S y Cp a 600 K.
  - H-Q6 **FALSADA**: SevenNet-0 da prácticamente lo mismo que MACE.
  - H-Q7 **PASA**: MACE sobreestima S298 en los 11 materiales.
  - H-REP **FALSADA**: ninguna réplica es idéntica byte a byte. La diferencia en S armónica es ≤ 1.3e-4 y los 8 veredictos salen iguales en run2.
  - Controles: C1 pasa (regresión ≤ 0.23 %), C3 pasa, C2 falla en 1 caso y C6 deja sin horquilla de volumen 3 casos.
- **Desviaciones:**
  - D1: corrección de un fallo en el script de evaluación.
  - D2: reglas R1–R3, que en este caso no cambiaron nada.
  - D3: float32 en MatterSim y SevenNet, con QHA patológicas.
  - D4: Cp_QHA numérico ruidoso.
- **Exploratorio (no pre-registrado):** en la celda experimental aproximada, la MARE armónica de S298 baja de 7.4 a 3.0 % con MatterSim y de 14.1 a 9.7 % con MACE. Indica que buena parte del error viene del volumen de equilibrio.
- **Originalidad:** ya conocido. Fromsejer et al. 2025 (doi:10.1016/j.commatsci.2025.113770) y Loew et al. 2025 (doi:10.1038/s41524-025-01650-1). Lo propio es solo la calibración pre-registrada y con fallos declarados.
- **Registro:** nueva fila UM-14 (C-MAT-003) en **E2**. UM-10 sigue en E2, UM-07 en E1 y UM-13 en E2, con las justificaciones ampliadas. Conteo: E0 17 · E1 20 · E2 10 · E3 7 · E6 9 · — 2 (65 filas).
- **Archivos:** C-MAT-003/ (prereg y .FROZEN.md, code/, out/run1 y run2, refs/, results.json, results_replica_run2.json, results_exploratorio_vexp.json, provenance_C-MAT-003.json, figs/fig_S_err_JANAF.png, informe_resultados.md).
- **Próximo paso:** prereg de C-MAT-004 con la corrección de volumen fijada a priori, float64 y Cp por ajuste suave.
