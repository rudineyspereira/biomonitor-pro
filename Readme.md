# BioMonitor Pro 🌲📊
### Plataforma Avançada de Inteligência Florestal, Bioeconomia e Econometria (SNIF & PEVS/IBGE)

[![Licença: MIT](https://img.shields.io/badge/License-MIT-emerald.svg)](LICENSE)
[![IBGE PEVS](https://img.shields.io/badge/Data-PEVS%2FIBGE-16a34a.svg)](https://sidra.ibge.gov.br/)
[![SNIF](https://img.shields.io/badge/Index-SNIF%20Inflation%20Adjusted-15803d.svg)](https://snif.florestal.gov.br/)
[![Single-File Architecture](https://img.shields.io/badge/Architecture-Single--File%20SPA-0284c7.svg)](#arquitetura-e-stack)
[![Status da Versão](https://img.shields.io/badge/Release-v2.5%20(1994--2025)-indigo.svg)](#séries-históricas-e-cobertura)

---

## 📌 Visão Geral & Posicionamento

O **BioMonitor Pro** é uma solução de inteligência de dados voltada à **bioeconomia**, **silvicultura de precisão** e **extrativismo vegetal sustentável**. O ecossistema consolida microdados do **Serviço Florestal Brasileiro (SNIF)** e da **Pesquisa da Extração Vegetal e da Silvicultura (PEVS/IBGE)**, cobrindo uma série histórica ininterrupta de **1994 a 2025**.

Diferente de painéis de visualização convencionais que exibem números brutos em moeda nominal, o **BioMonitor Pro** aplica deflatores e correções cambiais/inflacionárias aos valores históricos. Além disso, incorpora formulações de economia industrial (índices de concentração de mercado e especialização geográfica) e modelagem preditiva *what-if* para suporte à tomada de decisão em políticas públicas, ESG e investimentos florestais.

---

## 🔬 Fundamentação Metodológica e Indicadores

A plataforma implementa métricas analíticas e matemáticas fundamentadas:

### 1. Preço Médio Implícito Ponderado
Calculado a partir da relação direta entre a receita deflacionada e o volume físico extraído ou colhido:

$$P_{implícito} = \frac{\sum V_{\text{corrigido}}}{\sum Q_{\text{física}}}$$

Permite diferenciar ganhos reais de produtividade e margem de oscilações nominais de preço.

### 2. Índice de Concentração de Herfindahl-Hirschman (HHI)
Mensura o nível de dispersão ou concentração geográfica da produção florestal entre as unidades federativas:

$$\text{HHI} = \sum_{i=1}^{n} \left( s_i \right)^2$$

onde $s_i$ representa o percentual de *market share* do estado $i$ no total nacional ($s_i \in [0, 100]$):
* **$\text{HHI} < 1.500$**: Mercado distribuído e altamente competitivo territorialmente.
* **$1.500 \le \text{HHI} \le 2.500$**: Concentração geográfica moderada.
* **$\text{HHI} > 2.500$**: Alta concentração produtiva em poucas regiões/estados.

### 3. Quociente Locacional (QL / Especialização Regional)
Avalia a vocação produtiva e a intensidade relativa de determinada cadeia bioeconômica na economia florestal de um estado:

$$\text{QL} = \frac{e_i / e}{E_i / E}$$

onde:
* $e_i$: Faturamento do produto $i$ no estado.
* $e$: Faturamento florestal total do estado.
* $E_i$: Faturamento do produto $i$ no Brasil.
* $E$: Faturamento florestal total do Brasil.

> **$\text{QL} > 1,0$** indica vantagem comparativa revelada e especialização regional consolidada.

### 4. Projeção Econométrica & Intervalos de Confiança
Módulo preditivo com modelagem de regressão linear de tendência combinada a amortecimento sazonal, gerando horizontes de até 10 anos ($2026-2035$) com intervalos de confiança calculados a 95%:

$$y_t = \alpha + \beta t + \epsilon_t, \quad \text{IC}_{95\%} = \hat{y}_t \pm 1,96 \cdot \sigma_{\text{residual}}$$

## ⚡ Funcionalidades do Aplicativo

O painel está estruturado em 7 módulos funcionais:

| Módulo | Descrição Analítica |
| :--- | :--- |
| **Visão Geral & Mercado** | Curvas históricas comparativas (Silvicultura vs. Extrativismo), cálculo de CAGR, top produtos e estados líderes. |
| **Preços Médios & Inflação** | Comparação em tempo real entre valores nominais (PEVS) e valores corrigidos (SNIF), expondo ganhos reais de rentabilidade. |
| **Botânica & Silvicultura** | Classificação taxonômica por gêneros (*Eucalyptus*, *Pinus*, nativas) e destinação morfológica (frutos, cascas, exudatos, toras, lenha). |
| **Regionalização, HHI & QL** | Painel espacial com cálculo automático do índice HHI e matriz de especialização do estado (QL). |
| **Projeção & Simulador What-If** | Simulador paramétrico com sliders para choques de volume físico ($\pm 50\%$) e variações de preço ($\pm 50\%$). |
| **Benchmarking Comparativo** | Visão lado a lado (*Dual Target View*) para confrontar o desempenho de dois estados ou produtos florestais. |
| **Tabela Analítica de Microdados** | Tabela dinâmica paginada com busca instantânea em memória e exportação para CSV/Excel e PDF/Impressão. |

---

## 🛠️ Arquitetura e Stack

A aplicação adota o padrão **Single-File SPA (Zero-Dependency Run)**:
* **Interface & Responsividade:** HTML5 semântico com Tailwind CSS (JIT via CDN) e padrão Glassmorphism.
* **Mecanismo de Renderização Gráfica:** Chart.js com instanciamento e destruição reativa de canvases para evitar *memory leaks*.
* **Processamento de Dados:** Motor em Vanilla JavaScript ES6+, executando agregações, filtros multidimensionais, cálculo de deflatores e regressões inteiramente no lado do cliente (*client-side execution*).
* **Portabilidade:** Funciona de forma autônoma sem necessidade de servidor Node, containers Docker ou etapas de *bundling* (Webpack/Vite).

---

## 🚀 Como Executar

### Execução Local Direta
1. Clone o repositório ou baixe o arquivo HTML:
   ```bash
   git clone https://github.com/seu-usuario/biomonitor-pro.git
   cd biomonitor-pro
   ```
2. Abra o arquivo diretamente no navegador:
   ```bash
   # Linux / MacOS
   open dashboard_florestal_avancado.html

   # Windows
   start dashboard_florestal_avancado.html
   ```

### Execução via GitHub Pages
1. Vá até as **Settings** do repositório no GitHub.
2. Navegue até a seção **Pages** (na barra lateral).
3. Selecione a branch `main` e a pasta `/ (root)`.
4. Clique em **Save**. O dashboard estará disponível online instantaneamente com suporte a dispositivos móveis e desktop.

---

## 📂 Estrutura de Dados dos Registros

Os dados consumidos pela plataforma seguem a seguinte estrutura de propriedades por registro:

```json
{
  "ano": 2024,
  "uf": "PARÁ",
  "reg": "Norte",
  "prod": "Açaí (fruto)",
  "cat": "EXTRATIVO",
  "uso": "Alimentícios",
  "parte": "Fruto/semente",
  "esp": "Açaí",
  "un": "Toneladas",
  "qtd": 168527,
  "v_orig": 737925,
  "v_corrig": 769392.7
}
```

---

## 🎯 Casos de Uso e Público-Alvo

* **Setor Florestal & Celulose:** Análise de expansão de maciços florestais e monitoramento de séries de preços históricos da madeira em tora.
* **Cooperativas & Bioeconomia Comunitária:** Monitoramento da valorização de produtos da sociobiodiversidade (Açaí, Castanha-do-pará, Babaçu, Carnaúba, Erva-mate).
* **Gestores Públicos e Órgãos Ambientais:** Identificação de clusters de produção, planejamento do Plano ABC+ e monitoramento da transição extrativismo-silvicultura.
* **Pesquisadores e Economistas:** Exploração de séries temporais limpas com valores deflacionados para modelos econométricos e publicações científicas.

---

## 📄 Licença

Distribuído sob a licença **MIT**. Consulte `LICENSE` para mais informações.
