# 🖥️ VanTech - Data Solutions
## Sistema de Espelho de Ponto · Documentação Técnica

![Status](https://img.shields.io/badge/status-ativo-10b981?style=flat-square)
![Versão](https://img.shields.io/badge/versão-1.0.0-1a56db?style=flat-square)
![Tecnologia](https://img.shields.io/badge/tecnologia-HTML%20%7C%20CSS%20%7C%20JavaScript-f59e0b?style=flat-square)
![Colaboradores](https://img.shields.io/badge/colaboradores-5.030-8b5cf6?style=flat-square)

---

## 📋 Sobre o Projeto

Sistema web corporativo completo para **monitoramento, consulta e visualização de espelhos de ponto**, desenvolvido para a empresa fictícia **VanTech - Data Solutions Ltda.**

O sistema simula um software real de RH com aparência profissional, geração automática de 5.030 colaboradores com histórico de ponto realista, exportação em PDF e CSV, gráficos executivos e controle de pendências de assinatura.

---

## ✨ Funcionalidades

### 📊 Dashboard Executivo
- 8 cards KPI: total de colaboradores, ativos, desligados, férias, horas extras, horas negativas, espelhos assinados e pendentes
- 7 gráficos profissionais via **Chart.js**: horas extras por setor, tipos de ocorrência, horas por dia, faltas semanais, distribuição por cargo, Top 10 colaboradores e pendências de assinatura
- Seletor de competência que atualiza todos os indicadores em tempo real

### 👥 Colaboradores
- Tabela paginada com **5.030 registros** gerados proceduralmente
- Busca em tempo real por **nome ou matrícula**
- Filtros por setor, cargo, situação e status de pendência
- Ordenação clicável em todas as colunas
- Exportação CSV

### 📄 Espelho de Ponto
- Layout **idêntico ao modelo corporativo** (padrão insoft4/TOTVS)
- Cabeçalho com empresa, CNPJ, competência, período, matrícula, CPF, PIS, cargo, setor, tipo salário e data de admissão
- Tabela diária com: Data, Dia, Jornada Prevista, Marcações (Ent/Saí Almoço/Ret/Saída), Total Horas (Normal/Extra/Comp), Adicional Noturno, Ocorrência e Abono
- Linhas coloridas por tipo de ocorrência:
  - 🟩 Verde — Férias
  - 🟥 Vermelho — Falta / Esquecimento de marcação
  - 🟨 Amarelo — Feriado
  - ⬜ Cinza — Fim de semana (FOLGA COMPENSATÓRIA / DSR)
- Códigos de ocorrência: `00013FÉRIAS`, `00021ATESTADOS`, `00101ABONO`, `FALTA MARCAÇÃO`
- Rodapé **Resumo Pagamentos** com código, descrição, referência e horas
- Linha de assinatura do funcionário

### 📤 Exportar Espelhos
- Painel de busca por matrícula, nome ou setor
- Seleção individual ou em massa (todos os resultados)
- **Exportação PDF** individual ou em lote (múltiplos espelhos em um único arquivo)
- **Exportação CSV** com BOM UTF-8 para compatibilidade com Excel

### ⏱️ Jornadas
- Tabela com 8 jornadas cadastradas (J001–J008)
- Regras de horas extras: 50% (até 2h) e 100% (acima de 2h, sábado, domingo/feriado)
- Configurações de banco de horas e tolerâncias

### ⚙️ Parâmetros
- Dados da empresa, configurações de apuração
- Fluxo de assinatura: Colaborador → Gestor → RH
- Configurações de exportação

### 🔔 Pendências
- KPIs separados: Pendente Colaborador, Pendente Gestor, Pendente RH, Aprovados
- Tabela com status granular por etapa de aprovação

---

## 🏗️ Arquitetura

```
vantech-ponto.html          ← arquivo único auto-contido
├── <style>                 ← Design System completo (CSS Variables)
├── <body>
│   ├── #sidebar            ← Navegação fixa
│   ├── #main
│   │   ├── .topbar         ← Seletor de competência
│   │   └── .content
│   │       ├── #page-dashboard
│   │       ├── #page-colaboradores
│   │       ├── #page-pendencias
│   │       ├── #page-exportar
│   │       ├── #page-jornadas
│   │       └── #page-parametros
│   └── #mirror-overlay     ← Modal do espelho de ponto
└── <script>
    ├── Geração de dados    ← LCG determinístico
    ├── Lógica de ponto     ← genDayPoint / computeSummary
    ├── Renderização        ← Tabelas, filtros, paginação
    ├── Gráficos            ← Chart.js
    └── Exportação          ← PDF / CSV
```

### Tecnologias utilizadas

| Camada | Tecnologia |
|---|---|
| Interface | HTML5 + CSS3 (Custom Properties) |
| Lógica | JavaScript ES6+ (Vanilla) |
| Gráficos | Chart.js 4.4.1 (via CDN) |
| PDF | Impressão nativa do browser (window.print) |
| Dados | Gerador pseudo-aleatório LCG determinístico |

> **Sem dependências de build** — nenhum npm, webpack ou framework necessário. Um único arquivo `.html` que roda em qualquer browser moderno.

---

## 🚀 Como usar

### Opção 1 — Direto no browser
```bash
# Simplesmente abra o arquivo no browser
open vantech-ponto.html
# ou arraste o arquivo para o navegador
```

### Opção 2 — Servidor local
```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .

# Acesse: http://localhost:8080/vantech-ponto.html
```

---

## 📊 Dados Gerados

| Item | Quantidade |
|---|---|
| Total de colaboradores | 5.030 |
| Colaboradores ativos | 5.000 |
| Desligados (Maio/2026) | 16 |
| Desligados (Junho/2026) | 14 |
| Em férias (Maio) | 10 (início 04/05, 30 dias) |
| Em férias (Junho) | 10 (início 01/06, 30 dias) |
| Setores | 15 |
| Cargos distintos | 65+ |
| Competências disponíveis | Maio/2026 e Junho/2026 |

### Distribuição de Ocorrências
| Tipo | Probabilidade |
|---|---|
| Dia normal com variações | ~91% |
| Falta injustificada | 2% |
| Atestado médico | 1% |
| Abono | 1% |
| Esquecimento de marcação | 1,5% |
| Sábado trabalhado | 7% dos sábados |

### Status de Espelhos
| Status | % |
|---|---|
| Assinado | 64,4% |
| Pendente Colaborador | 13,6% |
| Pendente Gestor | 15,0% |
| Pendente RH | 7,0% |

---

## 📐 Regras de Negócio

- ✅ Desligamentos apenas em **dias úteis**, distribuídos em dias alternados
- ✅ **Sem marcações após desligamento**
- ✅ Férias exibidas com evento `00013FÉRIAS` e horas de DSR
- ✅ Feriados nacionais: Dia do Trabalho (01/05), Corpus Christi (21/05 e 11/06)
- ✅ Sábado → **FOLGA COMPENSATÓRIA** · Domingo → **DSR**
- ✅ Horas extras calculadas sobre jornada de **8h48 (528 min)**
- ✅ Extras 50% (até 2h) e 100% (acima de 2h, fins de semana e feriados)
- ✅ Adicional noturno para marcações após **22h00**
- ✅ Tolerância de atraso: **10 minutos**
- ✅ Cache de sumários para performance com 5.030 registros

---

## 🎨 Design System

```css
:root {
  --brand:      #1a56db;   /* Azul principal */
  --sidebar-bg: #0f172a;   /* Sidebar escura */
  --success:    #10b981;   /* Verde — ativo/assinado */
  --warning:    #f59e0b;   /* Amarelo — férias/pendente */
  --danger:     #ef4444;   /* Vermelho — desligado/falta */
  --border:     #e2e8f0;   /* Bordas suaves */
  --surface-2:  #f8fafc;   /* Background alternado */
}
```

---

## 📁 Estrutura de Arquivos

```
/
├── vantech-ponto.html          ← Sistema completo
├── vantech-ponto-codigo.pdf    ← Documentação técnica do código
└── README.md                   ← Este arquivo
```

---

## 🔮 Melhorias Futuras

- [ ] Backend Node.js + Express com API REST
- [ ] Banco de dados PostgreSQL com Prisma ORM
- [ ] Autenticação JWT com perfis (RH / Gestor / Colaborador)
- [ ] Assinatura digital integrada
- [ ] Exportação para Excel (.xlsx) com formatação
- [ ] Tema escuro
- [ ] App mobile (React Native)
- [ ] Integração com sistemas de folha (TOTVS, SAP)
- [ ] Notificações por e-mail para pendências
- [ ] Dashboard em tempo real com WebSockets

---

## 👨‍💻 Desenvolvido com

- **Geração de dados** — Linear Congruential Generator (LCG) determinístico
- **SPA sem framework** — navegação por manipulação de classes CSS
- **PDF nativo** — `window.open` + `window.print` com CSS `@media print`
- **Gráficos** — Chart.js 4.4.1 (bar, line, doughnut, pie)

---

<div align="center">

**VanTech - Data Solutions Ltda.**  
CNPJ: 12.345.678/0001-90 · São Paulo - SP

*Sistema de Espelho de Ponto — v1.0.0*

</div>
