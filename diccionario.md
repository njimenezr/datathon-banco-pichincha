# Diccionario de datos y glosario — Datathon Grupo Pichincha · **Banco Pichincha**

Qué datos tienes, qué significa cada columna y cada término de negocio. Pensado para tu equipo.

> **Todo es sintético.** Cédulas, montos y clientes son ficticios (cero PII). Las estructuras
> imitan las reales de Banco Pichincha.
>
> **Llave de cruce:** `id_cliente_hash` (un SHA-256 de la cédula). Es el **único** campo con el
> que unirás a la misma persona con Deuna y Seguros dentro del Clean Room.

---

## 1. Glosario cross-company (aplica a todos)

- **`id_cliente_hash`** — huella SHA-256 de la cédula. Igual en las 3 empresas para la misma
  persona → permite cruzar sin exponer la cédula real.
- **Clean Room** — sala limpia de datos: cada empresa comparte tablas para analizarlas en
  conjunto **sin ver la fila cruda de la otra**. Ahí se hace el join gobernado.
- **Overlap / cruce** — personas que aparecen en más de una empresa (misma `id_cliente_hash`).
- **Gap de cross-sell** — clientes tuyos que **no** están en otra empresa (p. ej. clientes del
  banco **sin póliza** de seguros). Es la oportunidad comercial.
- **Cross-sell** — venderle a un cliente actual un producto de otra línea/empresa del grupo.
- **Churn / retención** — abandono del cliente (churn) vs. acciones para conservarlo (retención).
- **Next-Best-Action (NBA)** — la siguiente mejor oferta o acción recomendada por cliente.
- **PII** — datos personales identificables. Aquí no hay: todo es sintético y hasheado.

> El **esquema de Deuna y Seguros no está en este documento**: lo descubrirás **dentro del
> Clean Room** cuando esas empresas compartan sus tablas. Diseña tu estrategia sabiendo que
> cruzarás por `id_cliente_hash`.

---

## 2. Tus datos — `banco.clean_room.clientes_banco` (~80 000 filas · 43 columnas)

Una fila por cliente persona. Convención: **tipo** · **dominio/rango** · descripción.

| Columna | Tipo | Dominio / rango | Descripción |
|---|---|---|---|
| `id_cliente_hash` | string | SHA-256 | **Llave de cruce** (hash de la cédula). |
| `edad` | int | 18–77 | Edad. |
| `rango_edad` | string | 18-25 … 66+ | Grupo etario. |
| `genero` | string | F / M | Género. |
| `ciudad` | string | — | Ciudad. |
| `region` | string | REGION NORTE · REGION COSTA | Región comercial. |
| `antiguedad_meses` | int | ≥ 0 | Meses como cliente del banco. |
| `cliente_nuevo` | int | 0/1 | Antigüedad < 12 meses. |
| `sub_segmento` | string | MASIVO_BASICO · MASIVO_PROMEDIO · MASIVO_TOP · PRE_AFLUENTE · AFLUENTE | Segmento por valor/afluencia. |
| `banca_cliente` | string | PERSONAS · PERSONAS + PES · PREMIUM | Banca de atención. |
| `saldo_cuentas` | double | ≥ 0 (USD) | Saldo en cuentas. |
| `saldo_inversiones` | double | ≥ 0 (USD) | Saldo en inversiones (0 salvo (pre)afluentes). |
| `prom_pasivos_6m` | double | ≥ 0 (USD) | Promedio de pasivos (depósitos) últimos 6 meses. |
| `maximo_cupo_tc` | double | ≥ 0 (USD) | Cupo máximo de TC en BP. |
| `maximo_cupo_tc_no_bp` | double | ≥ 0 (USD) | Cupo máximo de TC en otras entidades. |
| `maximo_desembolso_consumo` | double | ≥ 0 (USD) | Desembolso máximo de crédito de consumo. |
| `maximo_desembolso_consumo_bp` | double | ≥ 0 (USD) | Desembolso de consumo en BP. |
| `maximo_desembolso_consumo_no_bp` | double | ≥ 0 (USD) | Desembolso de consumo en otras entidades. |
| `monto_giros` | double | ≥ 0 (USD) | Monto transaccional de giros. |
| `ticket_promedio_giros` | double | ≥ 0 (USD) | Ticket promedio de giros. |
| `total_desembolsado_habitar_bp` | double | ≥ 0 (USD) | Crédito vivienda BP (sparse; 0 en la mayoría). |
| `max_monto_desembolsado_vivienda` | double | ≥ 0 (USD) | Máx. desembolso vivienda (sparse). |
| `saldo_cartera` | double | ≥ 0 (USD) | Saldo de crédito (cartera). `= _tc + _otros`. |
| `saldo_cartera_tc` | double | ≥ 0 (USD) | Cartera en tarjeta de crédito. |
| `saldo_cartera_otros` | double | ≥ 0 (USD) | Cartera en otros productos. |
| `saldo_cartera_sf` | double | ≥ 0 (USD) | Cartera en el sistema financiero externo. |
| `indicador_cartera` | int | 0/1 | Tiene cartera > 0. |
| `score_buro` | int | 300–850 | Score crediticio de buró. Baja con el riesgo. |
| `calificacion` | int | 1–4 | Calificación crediticia (1 mejor, 4 peor), derivada del score. |
| `dias_mora_max_12m` | int | ≥ 0 | Días de mora máximos en 12 meses. |
| `saldo_vencido` | double | ≥ 0 (USD) | Saldo vencido (0 si no hay mora ≥ 30d). `= _tc + _otros`. |
| `saldo_vencido_tc` | double | ≥ 0 (USD) | Vencido en TC; 0 si no hay mora. |
| `saldo_vencido_otros` | double | ≥ 0 (USD) | Vencido en otros productos; 0 si no hay mora. |
| `saldo_vencido_sf` | double | ≥ 0 (USD) | Vencido en el sistema financiero externo. |
| `indicador_vencida` | int | 0/1 | Tiene cartera vencida (≥ 30 días). |
| `indicador_vencida_sf` | int | 0/1 | Vencida en SF externo. |
| `indicador_castigada_sf` | int | 0/1 | Cartera castigada en SF externo (solo muy riesgosos). |
| `flag_mora_30d` | int | 0/1 | Marca de mora ≥ 30 días (~9% de la cartera). |
| `es_accionista` | int | 0/1 | Atributo societario. |
| `es_representante_ge` | int | 0/1 | Representante de grupo económico. |
| `es_rechazado` | int | 0/1 | Solicitud de crédito rechazada. |
| `tiene_tarjetas_adicionales` | int | 0/1 | Tiene TCs adicionales. |
| `sow` | double | [0, 1] | **Share of wallet** estimado (cuánto del bolsillo del cliente capta el banco). |

---

## 3. Glosario de negocio — Banco

- **Sub-segmento (masivo → afluente)** — nivel de valor del cliente: `MASIVO_BASICO` <
  `MASIVO_PROMEDIO` < `MASIVO_TOP` < `PRE_AFLUENTE` < `AFLUENTE`.
- **Banca cliente** — modelo de atención (PERSONAS, PERSONAS + PES, PREMIUM).
- **Score de buró** — puntaje crediticio (300–850); más alto = menos riesgo.
- **Calificación** — nota crediticia 1 (mejor) a 4 (peor), derivada del score.
- **Mora / días de mora / `flag_mora_30d`** — atraso en pagos; la bandera marca ≥ 30 días.
- **Cartera / cartera vencida** — saldo de crédito; vencida = con mora.
- **Pasivos** — dinero que el cliente deposita en el banco (cuentas, plazos).
- **Cupo TC** — límite de la tarjeta de crédito. **Desembolso consumo** — monto de crédito de consumo.
- **BP vs. no-BP** — sufijos `_bp` / `_no_bp`: producto/saldo **en Banco Pichincha** vs. **en otras
  entidades** (visión del cliente dentro y fuera del banco).
- **Giros (`monto_giros`, `ticket_promedio_giros`)** — volumen y ticket de transacciones de giros.
- **Cartera `_tc` / `_otros` / `_sf`** — desglose del crédito: tarjeta, otros productos, y
  **sistema financiero externo** (`_sf` = deuda del cliente en otros bancos, vía buró).
- **Cartera castigada (`indicador_castigada_sf`)** — crédito dado por incobrable (write-off); máximo riesgo.
- **Cliente nuevo (`cliente_nuevo`)** — antigüedad < 12 meses.
- **Accionista / representante (`es_accionista`, `es_representante_ge`)** — vínculo societario del
  cliente con empresas; útil para banca de negocios.
- **SOW (Share of Wallet)** — porción del bolsillo financiero del cliente que capta el banco (0–1).

---

## 4. ¿Qué puedes responder con tus datos?

- ¿Qué clientes tienen mayor capacidad de pago / afluencia?
- ¿Quiénes están en mora, con score bajo o cartera castigada?
- ¿Dónde hay margen de **share of wallet** (cupo/desembolso fuera de BP que podrías capturar)?

**Y al cruzar en el Clean Room** (por `id_cliente_hash`): ¿tus clientes de alto valor **sin
póliza** cuánto valen como cross-sell? ¿los que cancelan seguro o desertan como comercio tienen
peor perfil de riesgo en el banco? Ahí está el valor del datathon: **combinar** tus indicadores
con los de las otras dos empresas. Descubrirás sus tablas dentro del Clean Room.
