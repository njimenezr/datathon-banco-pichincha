# Datathon Grupo Pichincha — Equipo **Banco Pichincha**

Bienvenidos al datathon del **Grupo Pichincha**. Tres empresas —**Deuna, Banco Pichincha y
Seguros del Pichincha**— tienen, cada una, datos sintéticos de sí misma. El reto es **generar
valor de negocio combinando esos datos entre empresas, de forma segura**, usando **Databricks
Clean Rooms** — sin que ninguna vea la información cruda de la otra.

Este repositorio es el de tu equipo: **Banco Pichincha**.

## Tu rol

Conoces a fondo el **perfil financiero** de tus clientes (segmentación, capacidad de pago,
score, mora, cartera). Tu oportunidad está en **cruzar** ese perfil con la actividad de comercios
de **Deuna** y el comportamiento asegurador de **Seguros** para vender mejor y prestar con menos
riesgo — todo dentro de un Clean Room.

La llave para unir a la misma persona entre empresas es **`id_cliente_hash`**.

## Qué hay aquí

| Archivo | Para qué |
|---|---|
| [`datos/`](datos/) | Tus datos en **Parquet** (los subes tú a tu workspace) |
| [`reto.md`](reto.md) | Tu reto de negocio, entregables por nivel y criterios |
| [`diccionario.md`](diccionario.md) | Tus datos (columna a columna) + glosario de negocio |
| [`rubrica.md`](rubrica.md) | Cómo evalúa el jurado |
| [`guia_participante.md`](guia_participante.md) | Cómo arranca el día y cómo entregar |
| [`pitch/plantilla_pitch.html`](pitch/plantilla_pitch.html) | Plantilla base para tu pitch final |

## Quick start

1. Entra al **workspace (trial) de Banco** con el login compartido del organizador.
2. **Sube tus datos** de [`datos/`](datos/) (Parquet) a tu workspace **como veas conveniente** —
   descubran cómo hacerlo, es parte del reto.
3. Lee [`reto.md`](reto.md) y ten a mano [`diccionario.md`](diccionario.md).
4. **Tu equipo arma el Clean Room** e invita a Deuna y Seguros para cruzar por
   `id_cliente_hash`. **No hay una guía paso a paso: descúbranlo** — es parte del reto.
5. Construye tan alto como puedas en el *value stack*: dashboard → modelo → AI Functions →
   Genie Space → agente/app.

## Material de apoyo (decks)

Presentaciones de Databricks para el datathon (Unity Catalog, Delta Sharing, Genie, etc.):

**https://github.com/njimenezr/datathon-presentaciones**

> Repo privado — pide acceso al organizador para entrar.

---

> **Datos 100% sintéticos.** Contenido educativo para el Datathon Grupo Pichincha.
