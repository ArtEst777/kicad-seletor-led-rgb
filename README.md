# Seletor de LED RGB — KiCad (`kicad-seletor-led-rgb`)

Projeto de placa de circuito impresso (PCB) desenvolvido no **KiCad 10.0** para acionamento e seleção manual das cores de um **LED RGB SMD de Ânodo Comum** (`APFA3010LSEEZGKQBKC`), utilizando uma chave deslizante de 3 posições e proteção contra inversão de polaridade na alimentação DC.

---

## Visão Geral do Circuito

O circuito recebe alimentação contínua através de um conector **Barrel Jack DC (`J1`)**. A linha positiva passa por um diodo Schottky **`SS12` (`D1`)** para proteção contra inversão de polaridade e alimenta o pino de ânodo comum do LED RGB **`APFA3010` (`D3`)**.

A seleção de cor é feita no lado do cátodo (*low-side switching*) por meio de uma chave deslizante SMD de 3 posições (**`SW2`**), que conecta o barramento de `GND` a um dos três resistores limitadores de corrente (**`R1`**, **`R2`** ou **`R3`**), acionando individualmente o canal **Vermelho (R)**, **Verde (G)** ou **Azul (B)**.

---

## Lista de Materiais (BOM)

| Referência | Componente / Valor | Footprint (KiCad) | Descrição |
| :--- | :--- | :--- | :--- |
| **J1** | `Barrel_Jack` | `Connector_BarrelJack:BarrelJack_Horizontal` | Conector de alimentação DC Barrel Jack Horizontal |
| **D1** | `SS12` | `Diode_SMD:D_SMA` | Diodo Schottky 20V 1A (DO-214AC / SMA) — Proteção de polaridade |
| **D3** | `APFA3010` | `LED_SMD:LED_Kingbright_APFA3010_3x1.5mm_Horizontal` | LED RGB SMD Right-Angle (3.0 x 1.5 x 1.0 mm), Ânodo Comum |
| **R1** | `330 Ω` | `Resistor_SMD:R_0805_2012Metric` | Resistor SMD 0805 — Limitador de corrente do canal **Vermelho (R)** |
| **R2** | `220 Ω` | `Resistor_SMD:R_0805_2012Metric` | Resistor SMD 0805 — Limitador de corrente do canal **Verde (G)** |
| **R3** | `220 Ω` | `Resistor_SMD:R_0805_2012Metric` | Resistor SMD 0805 — Limitador de corrente do canal **Azul (B)** |
| **SW2** | `SW_SP3T_PCM13` | `Button_Switch_SMD:SW_SP3T_PCM13` | Chave deslizante SMD de 3 posições (Ultraminiature Slide Switch) |

---

## Dimensionamento Elétrico

Com base no [datasheet do LED Kingbright APFA3010LSEEZGKQBKC](Datasheets/APFA3010LSEEZGKQBKC.pdf):

| Canal (Cor) | Comprimento de Onda ($\lambda_{\text{peak}}$) | Tensão Direta Típica ($V_F @ 2\text{ mA}$) | Corrente Contínua Máx. ($I_F$) | Resistor Utilizado | Corrente Estimada ($V_{\text{in}} = 5\text{ V}$) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Hyper Red (Pino 1)** | $630\text{ nm}$ | $1.80\text{ V}$ (máx. $2.1\text{ V}$) | $30\text{ mA}$ | `330 Ω` (`R1`) | $\approx 8.3\text{ mA}$ |
| **Green (Pino 3)** | $515\text{ nm}$ | $2.65\text{ V}$ (máx. $3.1\text{ V}$) | $25\text{ mA}$ | `220 Ω` (`R2`) | $\approx 8.4\text{ mA}$ |
| **Blue (Pino 4)** | $460\text{ nm}$ | $2.65\text{ V}$ (máx. $3.1\text{ V}$) | $30\text{ mA}$ | `220 Ω` (`R3`) | $\approx 8.4\text{ mA}$ |

> **Nota de cálculo**: Considerando uma fonte de $5.0\text{ V}$ na entrada e queda direta aproximada de $0.35\text{ V}$ no diodo Schottky `SS12` ($V_{\text{ânodo}} \approx 4.65\text{ V}$), os valores de `330 Ω` (Vermelho) e `220 Ω` (Verde e Azul) equalizam a corrente nos três canais em torno de $8.3\text{ a }8.4\text{ mA}$, operando com ampla margem de segurança térmica.

---

## Especificações da PCB

* **Dimensões**: `27.5 mm x 29.0 mm` (bordas arredondadas com raio de `1.0 mm`).
* **Camadas**: 2 camadas (`F.Cu` para roteamento de sinais e componentes SMD; `B.Cu` com plano de terra `GND` contínuo).
* **Espessura da Placa**: `1.6 mm`.
* **Regras de Projeto (`Default`)**:
  * Largura de trilha: `0.2 mm`
  * Isolação (*clearance*): `0.2 mm`
  * Vias: Diâmetro `0.6 mm` / Furo `0.3 mm`

---

## Estrutura do Repositório

```text
├── 3_Leds.kicad_pro                  # Arquivo de projeto do KiCad 10.0
├── 3_Leds.kicad_sch                  # Esquemático eletrônico
├── 3_Leds.kicad_pcb                  # Layout da PCB
├── Datasheets/
│   └── APFA3010LSEEZGKQBKC.pdf       # Datasheet do LED RGB Kingbright
└── README.md                         # Documentação do projeto
```

---

## Autor

* **Artur F.G** ([@ArtEst777](https://github.com/ArtEst777))
