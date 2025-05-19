# 📦 Release Notes

## 🚀 Versão 1.4.0 – 2024-05-17

### ✨ Novas funcionalidades

- Adicionado suporte à **rastreabilidade individual SISBOV**, com visualização de eventos por animal. `[#55093]`
- Implementado relatório **"Custo de Produção por Animal"**, integrando dados de nutrição e insumos. `[#55012]`
- Tela de **cadastro de eventos sanitários** no módulo Rebanho. `[#54871]`

### 🧮 Cálculos e métricas

- Novo cálculo de **peso projetado** considerando datas de entrada e GPDs acumulados por animal. `[#54988]`
- Ajuste nos critérios de cálculo de **IMS % PV**, com histórico dos últimos 5 dias. `[#55037]`
- Correção no cálculo de **GPD médio** quando há transição de dieta no período. `[#55078]`

### 🌍 Internacionalização

- Adicionada tradução para inglês nos módulos:
  - Confinamento
  - Relatórios Nutricionais
  - Cadastro de Lotes `[#55045]`
- Datas e números agora seguem o locale configurado no perfil do usuário. `[#55063]`

### 🐛 Correções de bugs

- Corrigido erro na exportação XML do SISBOV que duplicava eventos. `[#55001]`
- Ajustada falha na listagem de lotes com status "Finalizado". `[#54976]`
- Resolvido problema que impedia salvar observações em telas de leitura de cocho. `[#55022]`

---

## 📌 Versões anteriores

Consulte a [documentação de versões anteriores](./historico.md) para mais detalhes.
