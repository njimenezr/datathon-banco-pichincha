# Reto BANCO PICHINCHA — Cross-sell inteligente y riesgo conjunto

## Contexto de negocio

Eres el equipo de datos de **Banco Pichincha**. Conoces a fondo el perfil financiero de tus
clientes, pero te faltan dos cosas: **qué tan activos son como comerciantes** (eso lo sabe
**Deuna**) y **su comportamiento como asegurados** (prima, cancelaciones — eso lo sabe
**Seguros**). Combinando esas señales — de forma segura, vía **Clean Room** — puedes vender
mejor y prestar con menos riesgo.

## Pregunta central

> **¿A qué clientes ofrecerles el próximo mejor producto (crédito, inversión o seguro), y
> cómo ajustar el riesgo usando señales de Deuna y Seguros que hoy no vemos?**

## Tus datos — `banco.clean_room.clientes_banco`

| Columna | Descripción |
|---|---|
| `id_cliente_hash` | Llave de cruce |
| `edad`, `genero`, `ciudad`, `region`, `antiguedad_meses` | Demográficos |
| `sub_segmento` (MASIVO_BASICO…AFLUENTE), `banca_cliente` | Segmentación por valor |
| `maximo_cupo_tc` (+ `_no_bp`), `maximo_desembolso_consumo` (+ `_bp`/`_no_bp`), `prom_pasivos_6m`, `saldo_cuentas`, `saldo_inversiones`, `sow` | Capacidad y relación (con desglose BP vs. no-BP) |
| `monto_giros`, `ticket_promedio_giros`, `total_desembolsado_habitar_bp`, `max_monto_desembolsado_vivienda` | Transaccionalidad y crédito de vivienda |
| `saldo_cartera` (+ `_tc`/`_otros`/`_sf`), `indicador_cartera` | Cartera desglosada por producto y por sistema financiero |
| `score_buro`, `calificacion`, `dias_mora_max_12m`, `saldo_vencido` (+ `_tc`/`_otros`/`_sf`), `indicador_vencida`, `indicador_vencida_sf`, `indicador_castigada_sf`, `flag_mora_30d` | Riesgo crediticio (con vencido/castigado por SF) |
| `rango_edad`, `cliente_nuevo`, `es_accionista`, `es_representante_ge`, `es_rechazado`, `tiene_tarjetas_adicionales` | Atributos y banderas |

> **43 columnas** en total: el desglose de cupo/desembolso (BP vs. no-BP), cartera y vencido por
> producto y por **sistema financiero externo** (`_sf`, `indicador_castigada_sf`), giros y crédito
> de vivienda dan mucho más para modelar riesgo y next-best-action.

## Datos que obtienes vía Clean Room

- **Deuna** (`comercios_deuna`): `num_transacciones`, `monto`, `prob_desercion`, `segmento`… → ¿tu cliente es además un comercio activo? ¿está creciendo o desertando?
- **Seguros** (`clientes_seguros`): `prima_total_anual`, `num_cancelaciones_12m`, `num_terminaciones`, `segmento_riesgo`, `estado_cliente`… → ¿ya está asegurado? ¿está cancelando pólizas (señal de fuga)?

**Llave de cruce:** `id_cliente_hash`.

## Pistas (señal real en los datos)

- El **`score_buro` bajo / mora** correlaciona con **más cancelaciones/terminaciones** en Seguros y **más churn** en Deuna → señal de riesgo cross-company aprovechable.
- La **afluencia** (saldos altos) se asocia a **mayor prima total** en Seguros → segmenta inversión y seguros premium.
- Hay **~40k clientes del banco sin seguro** → gap directo de cross-sell (bancaseguros).

## Entregables por nivel (sube tan alto como puedas)

1. **Insight** *(obligatorio)*: cruce en Clean Room + dashboard AI/BI de oportunidades de cross-sell y del riesgo conjunto por segmento.
2. **Predicción** *(obligatorio)*: modelo de propensión (a seguro/inversión/crédito) **o** un score de riesgo mejorado con señales de Deuna/Seguros. MLflow.
3. **Enriquecimiento**: `ai_classify` para priorizar clientes, `ai_gen` para el mensaje de oferta, `ai_summarize` para un perfil 360.
4. **Conversacional**: Genie Space que responda "¿qué clientes AFLUENTE sin seguro tienen bajo riesgo?".
5. **Agente / App** *(bonus)*: agente Next-Best-Action por cliente, o app de "cockpit" para el asesor.

## Ideas de insight

- Clientes afluentes sin seguro y con bajo riesgo de cancelación → cross-sell premium.
- Clientes con buen score que además son comercios Deuna crecientes → oferta de crédito de capital de trabajo.
- Ajuste de score interno incorporando las cancelaciones/terminaciones de Seguros como feature externa.

## Criterios de éxito

- Cruce **dentro del Clean Room**, sin exponer PII.
- Resultado **accionable** con **impacto cuantificado** ($ potencial, # clientes, reducción de riesgo).
- Pitch con demo en vivo del insight (Genie/agente).
