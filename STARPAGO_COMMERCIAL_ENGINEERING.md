# ⚙️ Starpago — Ingeniería Comercial Práctica (3 Piezas Faltantes)

> **Protocolo:** Zero Bullshit | Zero Parálisis por Análisis  
> **Fuente de datos:** casino.org (scraping vivo Agosto 2026) + AffPapa (Scraping Agosto 2026) + latinoscasinos.com + framework de PSPs de alto riesgo  
> **Estado:** Ejecutable desde el Día 1

---

## 🗺️ MAPA DE DINERO — Datos Verificados de casino.org (Scraping Agosto 2026)

### 🇲🇽 México — Top Casinos + Rieles de Pago Activos

| # | Casino | Pago del | Retiro | Métodos de Depósito (Verificados) |
|---|--------|-----------|--------|-----------------------------------|
| 1 | **Brazino777** | 98.26% | 1-5 días | Payz, Pay4Fun, Visa, Mastercard, Amex, DinersClub |
| 2 | **BC.Game** | 98.35% | 0-5 días | Crypto, Tarjetas internacionales |
| 3 | **Winner** | — | — | OXXO Pay, SPEI, Tarjetas locales |
| 4 | **Winpot.MX** | — | — | SPEI, Tarjetas locales |
| 5 | **PlayUZU.mx** | — | — | SPEI, Tarjetas |

**💡 Hallazgo MX:** El menú de Métodos de Pago en casino.org México lista explícitamente: **OXXO Pay, Todito Cash, SPEI, PayPal**. SPEI es el riel institucional dominante. Casinos sin SPEI dinámico tienen pain de conciliación.

### 🇵🇪 Perú — Top Casinos + Rieles de Pago Activos

| # | Casino | Pago del | Retiro | Métodos de Depósito (Verificados) |
|---|--------|-----------|--------|-----------------------------------|
| 1 | **Caliente.pe** | 97.81% | 1-3 días | PagoEfectivo, AstroPay, Visa, Mastercard, Transferencia |
| 2 | **Betsson** | 96% | 1-5 días | PagoEfectivo, Visa, Mastercard |
| 3 | **PlayUZU PE** | — | — | — |
| 4 | **bet365** | — | — | — |
| 5 | **Inkabet** | — | — | — |

**💡 Hallazgo PE:** casino.org Perú lista **Yape y Plin** como APMs estrella. Caliente.pe anuncia "Retiros inmediatos con Yape/Plin" como ventaja competitiva principal. AstroPay activo en Caliente.pe = competidor directo a desbancar.

**💡 latinoscasinos.com confirma APMs LATAM:** OXXO + Mercado Pago (MX), PagoEfectivo + Yape + Plin (PE), PSE + Efecty (CO), PIX (BR).

---

## 🔴 PIEZA 1: Pre-Onboarding Risk Qualification Checklist

> **Objetivo:** No atorar la tubería adquirente del entrevistador con merchants de riesgo.  
> **Cuándo usarlo:** Antes de presentar CUALQUIER prospecto al área de Riesgo/Compliance.

```
BLOQUE 1 — COMPLIANCE MÍNIMO (Si cualquiera es NO → STOP, no avanzar)

[ ] ¿Tiene licencia activa de juego en su país?
    MX: Permiso SEGOB/DGJS vigente
    PE: Autorización MINCETUR/DGJCMT (Ley 31557)
    CO: Licencia Coljuegos activa
    BR: Registro activo SPA/MF bajo dominio .bet.br

[ ] ¿Chargeback Ratio histórico < 1%? (Solicitar estado de cuenta 3 meses)
    1-2%: Escalar a Riesgo para decisión
    > 2%: DESCALIFICAR inmediatamente

[ ] ¿Tienen UBO (Ultimate Beneficial Owner) identificable?
    Solicitar: Acta constitutiva + identificación del UBO
    Estructuras opacas en paraísos fiscales sin justificación = RED FLAG


BLOQUE 2 — VIABILIDAD ECONÓMICA (2+ en NO → Baja prioridad)

[ ] ¿Procesan al menos $100,000 USD/mes de volumen?
    < $50K/mes: No es cuenta Key, derivar a self-serve

[ ] ¿60%+ de sus jugadores están en países con adquirencia Starpago? (MX/BR/CO/PE/CL)
    Operadores europeos queriendo "solo cobrar en LATAM" = deal complejo, no quick-win

[ ] ¿Modelo B2C directo (casino/sportsbook) o B2B (agregador)?
    Agregadores: Requieren diligencia adicional por sub-merchants ocultos


BLOQUE 3 — FIT TÉCNICO (Todo NO → Ciclo largo, no quick-win)

[ ] ¿Ya integran PSP vía API? (Si sí: tienen equipo técnico, integración en 2-4 semanas)
[ ] ¿Tienen Head of Payments o CTO como contacto técnico?
    Sin este contacto: la venta se cae en implementación. No cerrar sin él.
[ ] ¿Cuál es su PSP actual y cuál es el pain específico?
    Documentar: rechazos / lentitud de payouts / FX caro / caídas de plataforma


RESULTADO:
BLOQUE 1 completo + BLOQUE 2 (2+) + BLOQUE 3 (1+) = TIER 1 — Alta prioridad
BLOQUE 1 completo + BLOQUE 2 parcial = TIER 2 — Seguimiento 30 días
BLOQUE 1 incompleto = DESCALIFICADO
```

**🎯 Frase para la entrevista:**
> *"Antes de mandar un merchant al equipo de Riesgo, lo paso por un checklist de 3 bloques: compliance (licencia + chargeback < 1% + UBO identificable), viabilidad económica ($100K+/mes) y fit técnico. Solo los que pasan los 3 entran al embudo. Así protejo la tubería adquirente de Starpago desde el día 1."*

---

## 💸 PIEZA 2: Flujo de Liquidación y FX — Cómo se Mueve el Dinero

> **Objetivo:** Saber explicar el ciclo completo del dinero al CEO del casino en 2 minutos.

### 🇲🇽 México — Flujo SPEI

```
[JUGADOR en MX]
    ↓ Deposita
[PAY-IN vía SPEI / OXXO Pay / Tarjeta Local]
    ↓
[RECONCILIACIÓN automática]
    SPEI: T+0 (instantáneo)
    OXXO: T+1 hábil

OPCIÓN A — Liquidación en MXN (sin FX):
    → Transferencia a cuenta del casino en MX (CLABE del merchant)
    → Frecuencia pactada: Diaria o Semanal
    → Comisión FX: $0

OPCIÓN B — Settlement en USD / Transfronterizo:
    → Conversión MXN→USD (FX Spread negociable, típico mercado: 1.5–3.5%)
    → Envío vía SWIFT a holding del casino (Curaçao / Malta / UK)
    → T+2 a T+5 hábiles

PAIN POINT A ATACAR:
PayRetailers cobra FX Spread de 3–5%.
Si Starpago ofrece 1.5–2% con SPEI dinámico → ahorro de 1–3% por ciclo.
Ese diferencial se puede demostrar con números en la primera reunión.
```

### 🇧🇷 Brasil — Flujo PIX (Mercado Aislado)

```
[JUGADOR en BR]
    ↓ Deposita
[PAY-IN vía PIX (A2A instantáneo) / Boleto / Tarjeta]
    ↓
RECONCILIACIÓN:
    PIX: instantáneo (segundos)
    Boleto: T+1

OPCIÓN A — Liquidación en BRL (lo más común):
    → A cuenta bancaria BR del operador (requiere CNPJ activo)
    → Marco regulatorio: Ley 14.790 + normativa BCB (Banco Central de Brasil)
    → ⚠️ SIN entidad legal brasileña (CNPJ), no hay liquidación posible

OPCIÓN B — Remesa internacional BRL→USD:
    → Requiere autorización BCB + declaración IOF
    → IOF: varía según operación (0% a 6.38%)
    → Más lento y complejo, mayoría de operadores prefieren Opción A

PAIN POINT A ATACAR (verificado con datos reales):
Pay4Fun y Zimpler son líderes de PIX en casinos (Brazino777 usa Pay4Fun),
pero su cashout al jugador tarda 24–72h.
PIX directo de Starpago puede liquidar en segundos → killer feature.
```

### 🇨🇴 Colombia — Flujo PSE / Efecty

```
[JUGADOR en CO]
    ↓ Deposita
[PAY-IN vía PSE / Efecty / Tarjeta]
    ↓
RECONCILIACIÓN:
    PSE: T+1 hábil (ACH Colombia)
    Efecty: T+0 a T+1

LIQUIDACIÓN en COP:
    → A cuenta del operador (licenciado Coljuegos)
    → Settlement: 24–48h hábiles

FX opcional:
    → COP → USD vía mercado cambiario regulado (Resolución BanRep 1/2018)

PAIN POINT A ATACAR:
PSE tiene fricción alta (autenticación bancaria en 3+ pasos).
Efecty (efectivo) tiene volumen masivo en estratos 1-3 sin cuenta bancaria.
Quien domine el canal efectivo (Efecty/Baloto) tiene ventaja real en CO.
```

### 🇵🇪 Perú — Flujo PagoEfectivo / Yape

```
[JUGADOR en PE]
    ↓ Deposita
[PAY-IN vía PagoEfectivo / Yape / Plin / Visa]
    ↓
RECONCILIACIÓN:
    Yape/Plin: Instantáneo (A2A móvil)
    PagoEfectivo: T+0 a T+1 (según agente: BCP, BBVA, Interbank, Scotiabank)

LIQUIDACIÓN en PEN:
    → A cuenta del operador (autorizado MINCETUR/Ley 31557)

PAIN POINT A ATACAR (verificado con datos reales):
Caliente.pe (#1 en PE) anuncia "retiros inmediatos con Yape/Plin" como feature estrella.
Betsson PE tiene pago del 96% — hay rechazos mejorables con adquirencia local.
Casinos sin Yape nativo están perdiendo conversiones de jugadores móviles.
```

---

## 🎯 PIEZA 3: Máquina de Prospección Inversa — Checkout Audit

> **Objetivo:** Identificar el pain real de un casino antes de la primera llamada.  
> **Tiempo:** 30 minutos por prospecto. Ejecutable desde el Día 1, Hora 1.

### 🔧 Flujo de Trabajo Diario

```
PASO 1 — IDENTIFICACIÓN DE TARGET (5 min)
    Fuentes con datos reales:
    ✦ casino.org/es-mx → Top 10 → Casinos con retiro > 3 días = PAIN confirmado
    ✦ casino.org/pe → Top 10 → Casinos sin Yape = PAIN confirmado
    ✦ AffPapa.com > "Payment Providers" > Filtrar por LATAM
    ✦ latinoscasinos.com → Ver qué casinos NO tienen APMs locales listados

    Señales de alerta (indican mal PSP):
    ✦ Retiros > 3 días en casino.org
    ✦ Pago del < 96% (rechazos altos = adquirente deficiente)
    ✦ Menú de pagos sin APMs locales (solo Visa/MC internacional)


PASO 2 — CHECKOUT AUDIT (15 min, modo incógnito)
    → Ir al casino como usuario → clic en "Depositar" / "Caja" / "Cashier"
    → Documentar:
    
    a) ¿SPEI presente? ¿Es estático (CLABE fija) o dinámico (CLABE única por tx)?
       SPEI estático = errores de conciliación = PAIN REAL del operador
    
    b) ¿SPEI dinámico expira en < 5 minutos? = ALTA FRICCIÓN para el jugador
    
    c) ¿El retiro (cashout) requiere más de 3 pasos? = FRICCIÓN = ABANDONO
    
    d) ¿Publican el tipo de cambio FX en el cajero? ¿A qué %?
       Ejemplo: "1 USD = 19.8 MXN" cuando el mercado está en 17.5 MXN = 13% spread
    
    e) ¿Cuántos campos pide el KYC? Más de 4 campos = abandono alto


PASO 3 — CONTACTO (5 min)
    LinkedIn: "[Casino] Head of Payments" o "CFO" o "Country Manager LATAM"
    Operadores europeos (Betsson, bet365): buscar "Head of Payments LATAM"


PASO 4 — MENSAJE DE OUTREACH (5 min)
    ─────────────────────────────────────────────────────────────
    LINKEDIN (nota de conexión, máx. 300 caracteres):
    
    "Hola [Nombre], revisé el cajero de [Casino] y el SPEI es estático.
    Cada tx comparte CLABE — eso genera errores de conciliación frecuentes.
    Tengo una solución. ¿15 minutos esta semana?"
    ─────────────────────────────────────────────────────────────
    EMAIL:
    
    Asunto: [Casino] — SPEI dinámico y payouts en < 24h
    
    [Nombre],
    
    Revisé el cajero de [Casino] y noté dos fricciones concretas:
    1. SPEI estático → errores de conciliación en picos de tráfico.
    2. Pago del [X]% → hay rechazos que están costando revenue.
    
    Procesamos SPEI dinámico (CLABE única por transacción) con conciliación
    automática y payouts en < 24h para México.
    
    ¿15 minutos para mostrarle el diferencial en números?
    
    [Nombre] | Business Development | Starpago
    ─────────────────────────────────────────────────────────────
```

### 📊 Targets Verificados para Checkout Audit Inmediato

Estos casinos tienen pain points **identificados con datos reales de casino.org**:

| Casino | País | Pain Verificado | Ángulo de Ataque |
|--------|------|----------------|-----------------|
| **Betano** | LATAM (BR/MX/CO/PE/AR) | Marca #1 dominante regional | Modelo de localización perfecta con APMs locales e infraestructura de payouts instantáneos. |
| **Brazino777** | MX/BR | Retiro 1-5 días | Payouts más rápidos + PIX directo |
| **BC.Game** | MX | Solo cripto visible, sin APMs locales | Integrar SPEI para usuarios no-cripto |
| **Caliente.pe** | PE | AstroPay activo = intermediario costoso | Ofrecer APMs directos sin billetera |
| **Betsson PE** | PE | Pago del 96% — rechazos mejorables | Adquirencia local con mayor approval rate |
| **Inkabet PE** | PE | Casino local sin info clara de APMs | Prospecto de alto potencial sin PSP robusto |

> 📌 **Inteligencia de Mercado (Ranking Blask / TopPay Julio 2026):**
> *"In emerging markets, payments aren't just part of the product. Payments ARE the product."*
> **Betano** es la única marca que domina de forma simultánea en los 5 mercados clave (BR, MX, CO, PE, AR) gracias a su estrategia de infraestructura de pagos locales (PIX, SPEI, PSE, Yape) y Payouts instantáneos.

---

## 🤝 PIEZA 4: Infraestructura de Payouts para Afiliados y Modelos de Comisión

> **Objetivo:** Ofrecer a los operadores la solución tecnológica para pagar comisiones a sus redes de afiliados (CPA/RevShare) de forma masiva, instantánea y con bajo FX.  
> **Por qué es un Killer Feature para el CEO/CFO del Casino:** El pago tardío o costoso a afiliados destruye la reputación del operador y frena la adquisición de jugadores.

### 💰 Desglose de Modelos de Comisión en iGaming (AffPapa Standards)

1. **CPA (Cost Per Acquisition / Action):**
   * Payout único por jugador nuevo que deposita (FTD - First Time Deposit).
   * Rango de mercado: **$50 – $250 USD** por jugador calificado.
   * *Pain del Operador:* Necesita pagar masivamente a cientos de afiliados cada semana en monedas locales (MXN, BRL, COP, PEN) sin arruinarse en comisiones bancarias SWIFT.
   * *Solución Starpago:* Payouts masivos vía API directa usando SPEI/PIX/PSE local.

2. **RevShare (Revenue Share):**
   * Porcentaje recurrente sobre el NGR (Net Gaming Revenue) generado por los jugadores referidos.
   * Rango de mercado: **15% – 40%** en Apuestas Deportivas | **hasta 60%** en Casino Online.
   * *Pain del Operador:* Reconciliación mensual compleja y retrasos en transferencias internacionales.
   * *Solución Starpago:* Reconciliación automatizada T+0 / T+1 con settlement directo a cuentas bancarias de afiliados en LATAM.

3. **Hybrid (CPA + RevShare):**
   * Combinación (ej. $50 CPA + 20% RevShare). Es el estándar moderno en la industria.

4. **Fixed Fee / Listing Fee:**
   * Tarifa fija mensual/anual solicitada por sitios de reseñas autorizados (ej. casino.org, AffPapa) para listado prioritario.

---

## 📅 CALENDARIO VERIFICADO 2026 — Eventos C-Level iGaming LATAM

> **Fuente verificada:** AffPapa iGaming Events Calendar 2026 (Auditoría completa 8 páginas)

| Fecha | Evento | Ubicación | Enfoque Estratégico Starpago |
|---|---|---|---|
| **12-13 Ago 2026** | **Token Americas (Flagship)** | CDMX (Centro Asturiano) | Dólares digitales, Stablecoins (USDT/USDC), tokenización y pagos transfronterizos. |
| **13 Ago 2026** | **G&M Events Brazil** | São Paulo, Brasil | Negociación con operadores de apuestas (.bet.br) y prueba de PIX instantáneo. |
| **24-25 Ago 2026** | **CGS Recife** | Recife, Brasil | Red de afiliados y proveedores B2B locales en el mercado brasileño. |
| **1-3 Sep 2026** | **SiGMA North America** | CDMX, México | Evento insignia en México: pitch presencial a casinos Tier 1 (Winner, Brazino777). |
| **9-10 Sep 2026** | **G&M Events Argentina** | Rosario, Argentina | Encuentro con operadores de salas y plataformas online de Argentina/Mercosur. |
| **15 Oct 2026** | **GAT Expo Bogotá** | Bogotá, Colombia | Showroom ejecutivo de un día para negociaciones directas con permisionarios Coljuegos. |
| **4-5 Nov 2026** | **G&M Events Mexico** | CDMX (Oficinas Google/Oracle) | Encuentro C-Level con líderes de tecnología y apuestas en México. |
| **23-25 Nov 2026** | **AffPapa Conference Cancún** | Cancún, México | Cierre de acuerdos de payouts masivos con redes globales de afiliados y casinos. |
| **25 Nov 2026** | **AffPapa iGaming Awards LATAM** | Cancún, México | Gala C-Level: consolidación institucional y networking de alto nivel. |
| **9-12 Dic 2026** | **Tulum Innovation Fest** | Tulum, Q. Roo (Ikal Arena) | Cierre de año local en territorio propio (Tulum/Cancún) con founders de Crypto, Web3 y New Economy. |

---

## 💬 Las 4 Frases de Cierre para la Entrevista

**Pieza 1 — Pre-Calificación:**
> *"Mi primer filtro es compliance: si no tiene licencia activa y chargeback < 1%, no entra al embudo. Protejo la tubería adquirente de Starpago desde el día 1 — no le mando merchants basura al área de Riesgo."*

**Pieza 2 — FX/Settlement:**
> *"Un casino que liquida en México con PayRetailers está pagando 3–5% de FX Spread. Starpago con SPEI dinámico puede llegar a 1.5–2%. Eso es 1–3 puntos de margen que le devuelvo al operador en cada ciclo. El pitch se cierra con una calculadora, no con una presentación."*

**Pieza 3 — Prospección Inversa:**
> *"No hago llamadas en frío. Hago auditorías de cajero. Entro al casino, veo que su SPEI tarda 72h en liquidar y que su FX está a 4.2%, y le escribo al Head of Payments diciéndole exactamente eso con datos. La tasa de respuesta se triplica porque no le estoy vendiendo nada — le estoy mostrando su propio problema."*

**Pieza 4 — Settlement de Afiliados:**
> *"Los casinos gastan millones en comisiones CPA y RevShare. Si sus pagos a afiliados en LATAM se retrasan por lidiar con bancos locales, los afiliados mueven el tráfico a la competencia. Con la API de Payouts masivos de Starpago en SPEI y PIX, el operador liquida comisiones en minutos y se convierte en el destino favorito de los mejores afiliados de la región."*

