# Tail Sampling

![alt tag](../imagens/otel-logo.png)

## Tail Sampling:

**Conceito:**

Tail sampling é uma técnica onde a amostragem é realizada após a conclusão de uma operação. Essa abordagem permite capturar e registrar informações detalhadas apenas sobre spans que são considerados relevantes, geralmente aqueles com resultados de erro ou latências elevadas.
A amostragem é baseada nos resultados da operação. Por exemplo, se uma transação falha, é registrado um span detalhado para essa transação, enquanto os spans de sucesso podem ser ignorados ou registrados em menor detalhe.

**Qual a diferença para Head Sampling?**

Head sampling é uma abordagem em que a decisão de registrar um span é feita no início da operação, antes de ela ser concluída. Assim que um evento específico (como uma requisição) é iniciado, é decidido se ele deve ser registrado com base em critérios predefinidos, como probabilidades ou tags.

A escolha entre tail sampling e head sampling depende muito dos objetivos da sua estratégia de monitoramento e observação. Se o foco é na identificação e análise de incidentes, o tail sampling é preferível, enquanto o head sampling pode ser mais útil para ter uma visão geral do desempenho de um sistema.

Ref.: [https://konst.fish/blog/OTel-Collector-SpanMetrics-Tempo](https://konst.fish/blog/OTel-Collector-SpanMetrics-Tempo)