# Peso Projetado

> Calcula o **peso vivo estimado** de um animal em determinada data com base no peso de entrada no confinamento e na **soma dos ganhos de peso diários (GPD)** desde então.

## Variáveis

- [Peso de Entrada](./peso-entrada.md)
- [GPD](./gpd.md)
- Σ(GPD_diário): Soma acumulada dos GPDs desde o início do confinamento até a data de cálculo.

## Regras de Cálculo

1. Identificar a data de entrada no confinamento do animal
2. Obter os dias de consumo do animal
3. Para cada dia de consumo entre a entrada e a data de cálculo:
   - Consultar o **programa nutricional vigente**.
   - Identificar o **GPD previsto** para aquele dia.
4. Somar os GPDs acumulados.
5. Somar ao peso de entrada.

## Exemplo

```plaintext
peso_entrada = 270 kg
dias no confinamento = 10
GPD acumulado = 15k

peso_projetado = 270kg + (15kg) = 285 kg
```
