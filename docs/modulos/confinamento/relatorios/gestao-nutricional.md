# Gestão Nutricional

## Objetivo

Este relatório tem como finalidade monitorar o consumo nutricional por lote no confinamento.

## Localização no sistema

Módulo: **Confinamento**

Menu lateral > Aba "Fornecimento de Tratos" > Item: **Gestão Nutricional - Consumo realizado por Lote**

---

## Campos Exibidos

| Campo                  | Descrição                                                              | Regra/Origem                                                                   |
| ---------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Local**              | Nome da localidade/curral                                              | `mbw_localizacao.nome`                                                         |
| **Cab.**               | Quantidade de cabeças no lote                                          | `count(distinct animal_id)` na data                                            |
| **Sexo**               | Sexos dos animais: `M`, `F`, `M, F`                                    | Agrupado por sexo na data                                                      |
| **Peso Entrada**       | Peso médio de entrada dos animais na localidade atual                  | Peso obtido na entrada (via `obtenha_peso_na_data`)                            |
| **Dias Cocho Total**   | Média de dias em que os animais receberam trato em qualquer localidade | Soma de dias de cocho por animal desde a entrada no confinamento / qtd animais |
| **Dias Cocho no Lote** | Média de dias de trato na localidade atual                             | Soma de dias de cocho do animal na localidade / qtd animais                    |
| **Dieta Atual**        | Nome da dieta mais recente aplicada                                    | `produto_texto` de `mbw_material`                                              |
| **# Uso**              | Dias em que a dieta atual foi usada                                    | `count(distinct data)` em `saidas_produtos_geral` para a dieta atual           |
| **Transição**          | Indica mudança de dieta no lote                                        | 'SIM' se mais de uma dieta foi registrada; 'NÃO' caso contrário                |
| **Qtd. Total**         | Quantidade total fornecida no dia                                      | Soma de `consumo` dos animais na data                                          |
| **% Variação**         | Diferença entre o previsto e o realizado (%)                           | `(real - previsto)/previsto * 100`                                             |
| **Por Cab. M.O.**      | Consumo médio por cabeça de Matéria Natural                            | `consumo_mo / quantidade_cabecas`                                              |
| **Por Cab. M.S.**      | Consumo médio por cabeça de Matéria Seca                               | `consumo_ms / quantidade_cabecas`                                              |
| **Sobra D-3 a D0**     | Nota de sobra de cocho dos últimos 4 dias                              | `mbw_sobracocho.sobra` por dia -3 a dia 0                                      |
| **IMS PV 5 / 1 / 0**   | IMS dos dias -5, -1 e 0                                                | `consumo_ms / peso_projetado_total * 100`                                      |
| **IMS Médio**          | Média acumulada do IMS desde a entrada                                 | `(consumo_ms_acumulado / diarias) / (peso_acumulado / diarias) * 100`          |
| **Peso Atual**         | Peso vivo projetado médio                                              | `peso_entrada + soma(gpd)` por animal, média do lote                           |
| **GPD**                | Ganho de Peso Diário Médio                                             | Soma dos GPDs / qtd animais                                                    |

---

## Regras de Negócio Centrais

* [Peso Projetado](../conceitos/peso-projetado.md)

* **IMS (% PV):**

  * `consumo_ms / peso_projetado_total * 100`
  * Para dia atual, -1, -5 e média acumulada desde a entrada do animal no confinamento (mesmo com trocas de curral)

* **Transição de dieta:**

  * Verifica se houve aplicação de mais de uma dieta nos últimos dias

* **Variação Previsto x Realizado:**

  * Quantidade prevista: `definicao diaria de tratos`
  * Quantidade realizada: soma de `custos dos animais`

* **Sobra de Cocho:**

  * Pegas via `mbw_sobracochoitens`
  * Exibir dias: D-3, D-2, D-1, D0
  * Calcular média somente sobre dias com registro

---

## Origem dos Dados

* Base: `mbw_confinamento`, `mbw_custoporanimal`, `mbw_programa_nutricional`, `mbw_material`, `mbw_sobracocho`, entre outras.
* Query SQL associada: `GESTAO_NUTRICIONAL_CONSUMO_POR_lOTE`
* Backend: Endpoint DRF que executa esta query e retorna JSON formatado
* Frontend: Angular, componente `gestao-nutricional.component.ts`, usando binding com `vm.localidades`

---

## Telas Relacionadas

* **Frontend:** `/confinamento/gestao-nutricional`
* **AngularJS:** componente com binding para `localidade.xxx`

---

## Observações

* O campo "Responsável" foi removido da versão nova.
* As definições visuais são mantidas conforme mockup.
* As ajudas de tela (tooltips) são mantidas e mapeadas por tag `ng-ajuda` (ex: `monit_gestao_nutri__10__ims_pv`)

---

## Referências Cruzadas
