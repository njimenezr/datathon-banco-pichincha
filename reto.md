# Reto — BANCO PICHINCHA

## El contexto

Eres el equipo de datos de **Banco Pichincha**. Conoces el perfil financiero de tus clientes
(capacidad de pago, score, mora, cartera). Pero el mayor valor del Grupo Pichincha **no está en
tus datos solos** — aparece cuando los combinas con la actividad de comercios de **Deuna** y el
comportamiento asegurador de **Seguros** sobre esas mismas personas.

## Tu misión

> **Genera valor de negocio para el Banco combinando tus datos con los de las otras empresas del
> grupo — de forma segura.**

Qué problema resolver (cross-sell del próximo mejor producto, gestión de riesgo, capital de
trabajo a comercios, etc.) lo decides tú. **El cruce con Deuna y Seguros no viene resuelto:**
hablen entre equipos, acuerden qué compartir y descubran juntos cómo montar el Clean Room.

## Qué construir (sube tan alto como puedas)

1. **Insight** + dashboard AI/BI
2. **Modelo** (ML + MLflow)
3. **AI Functions** (ai_classify / ai_gen / ai_summarize)
4. **Genie Space** sobre los datos combinados
5. **Agente / App** *(bonus)*

## Cómo se evalúa

Ver **[`rubrica.md`](rubrica.md)**. Pesa más el **valor de negocio** y el **cruce seguro** (cómo
compartes y proteges los datos) que la sofisticación técnica.

## Lo que tienes

- Tus datos en **[`datos/`](datos/)** (Parquet) → súbelos a tu workspace (descubran cómo).
- El significado de cada campo en **[`diccionario.md`](diccionario.md)**.
- **El resto lo descubren ustedes:** qué cruzar, con quién, cómo crear el Clean Room y **cómo
  preparar los datos antes de compartirlos** (ver [`guia_participante.md`](guia_participante.md)).
  La única llave para unir personas entre empresas es **`id_cliente_hash`**.
