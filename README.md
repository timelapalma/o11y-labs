# Conceitos sobre Observabilidade 
**Um resumo baseado no treinamento LFS148:**

**Observabilidade** é a capacidade de inferir os estados internos de um sistema com base na análise de suas saídas externas. Em termos práticos, trata-se da facilidade com que é possível compreender o funcionamento interno de uma aplicação ou serviço a partir dos dados que ele gera, como logs, métricas e rastreamentos.

**Sistemas distribuídos** são compostos por múltiplos computadores independentes, chamados de nós, que cooperam para executar tarefas como se fossem uma única unidade lógica. Esses sistemas são amplamente utilizados em cenários como a computação em nuvem, onde diferentes componentes de uma aplicação são executados em servidores distintos para viabilizar escalabilidade, alta disponibilidade e uso eficiente de recursos. Devido à sua complexidade e natureza dinâmica, entender o comportamento interno de cada componente em tempo real é desafiador o que torna a observabilidade um elemento essencial.

Para tornar um sistema distribuído "observável" é necessário **modelar seu estado** de forma a permitir o raciocínio sobre seu comportamento.

Este modelo é composto por três fatores principais:

*   **Carga de trabalho (Workload)**: Refere-se às operações executadas pelo sistema para cumprir seus objetivos. Envolve a entrada de requisições e sua decomposição em tarefas menores, geralmente processadas por diferentes serviços. Essas operações são frequentemente chamadas de transações.
*   **Abstrações de software**: Representam os componentes lógicos e estruturais do sistema distribuído, como balanceadores de carga, serviços, pods, contêineres e outras entidades que organizam e viabilizam a execução do trabalho.
*   **Máquinas físicas**: Compreende os recursos computacionais que suportam a execução do sistema, como CPU, memória, armazenamento e rede.

<img width="600" height="457" alt="image" src="https://github.com/user-attachments/assets/8ba2036a-6b08-48e0-851c-789caec5da4d" />

---

## Logs

Um log é uma estrutura de dados que registra eventos ocorridos em um sistema. Cada entrada normalmente contém um carimbo de data e hora e uma mensagem com os detalhes do evento. Criar um formato de log padronizado, no entanto, é uma tarefa complexa, pois diferentes tipos de software expõem diferentes tipos de informação. Os logs de um servidor HTTP, por exemplo, são bastante distintos dos logs do kernel. Mesmo entre sistemas similares, há pouca concordância sobre o que constitui um bom log.

Além do conteúdo, os formatos de log também variam conforme o público-alvo. Inicialmente, os logs eram projetados para leitura humana, em formato texto. No entanto, com o aumento da complexidade dos sistemas e do volume de logs, essa abordagem se tornou inviável. Como resposta, surgiu o conceito de log estruturado, onde os eventos são registrados como pares chave/valor, tornando-os legíveis por máquinas e mais fáceis de analisar. Além disso, com a popularização de aplicações conteinerizadas e efêmeras, tornou-se inviável acessar logs diretamente em cada máquina. Isso levou ao desenvolvimento de agentes e protocolos de envio de logs para sistemas centralizados, que possibilitam armazenamento eficiente, além de busca e filtragem em um único local.

<img width="1000" height="358" alt="image" src="https://github.com/user-attachments/assets/3b6c2636-7992-46aa-b8d0-5aa3b9c2d94b" />

---

## Métricas

<img width="750" height="399" alt="image" src="https://github.com/user-attachments/assets/1669a6a6-a092-41cb-9040-61d38a0cd107" />

Os logs são excelentes para fornecer informações detalhadas sobre eventos individuais, mas não são ideais para entender o estado geral de um sistema. É nesse ponto que entram as métricas. Uma métrica é um valor numérico obtido por meio da aplicação de uma operação estatística sobre um conjunto de eventos, representando assim uma visão agregada. As métricas são valiosas porque sua forma compacta permite visualizar facilmente, por meio de gráficos e dashboards, como um sistema evolui ao longo do tempo. Para isso, a indústria desenvolveu ferramentas para coleta de métricas, formatos e protocolos para sua transmissão, bancos de dados especializados em séries temporais para armazenamento e interfaces que tornam essas informações acessíveis e úteis para os usuários.

---

## Traces

<img width="1000" height="772" alt="image" src="https://github.com/user-attachments/assets/2437019c-9a1f-48c4-a1fe-4b54edd93238" />


À medida que os sistemas distribuídos cresceram em escala, ficou claro que as soluções tradicionais de logging eram insuficientes para diagnosticar problemas complexos. Isso ocorre porque, muitas vezes, é necessário entender a cadeia de eventos que levou a determinado comportamento do sistema. Em uma máquina única, usamos stack traces para rastrear exceções até a linha de código correspondente. Em ambientes distribuídos, essa visibilidade direta não existe.

Nesses casos, é comum que engenheiros realizem filtragens extensivas para localizar logs relevantes e, em seguida, reconstruam o contexto completo — identificando qual requisição originou o evento e como ela percorreu diferentes serviços ou microsserviços no sistema. Esse processo é frequentemente manual, exige comparação de timestamps e conhecimento aprofundado sobre a aplicação.

**Traces Distribuídos**

A demanda acima criou a necessidade de sistemas de correlação mais complexos, e a partir de um recurso desenvolvido pelo google chamado Dapper o termo **Trace Distribuído** se tornou popular, é uma técnica de observabilidade que permite rastrear o caminho completo de uma requisição à medida que ela atravessa diferentes componentes de um sistema distribuído, como APIs, microsserviços, filas e bancos de dados.

Em vez de olhar eventos isolados (como nos logs) ou dados agregados (como nas métricas), o tracing captura e correlaciona os eventos individuais gerados por cada serviço envolvido no processamento de uma requisição.

---

## Os Tais Três Pilares da Observabilidade

Telemetria é o processo de coletar e enviar automaticamente dados de sistemas remotos ou distribuídos para monitorar e acompanhar seu desempenho ou estado. Esses dados oferecem uma visão em tempo real de como as partes de uma aplicação estão funcionando. A telemetria é a base das ferramentas de observabilidade, permitindo que desenvolvedores e administradores identifiquem problemas e otimizem sistemas sem precisar verificar manualmente cada componente.

À primeira vista, logs, métricas e traces parecem ter um ciclo de vida parecido: tudo começa com a instrumentação, que coleta e gera os dados. Depois, os dados precisam estar em um formato estruturado, ser coletados e enviados, muitas vezes com a ajuda de agentes que enriquecem, processam e agrupam as informações antes de enviá-las a um sistema de backend. Esse backend geralmente usa um banco de dados para armazenar, indexar e buscar grandes volumes de dados. Por fim, há uma interface visual para que os usuários consigam analisar os dados.

Na prática, no entanto, desenvolvemos sistemas específicos para cada tipo de telemetria, pois cada um traz desafios técnicos próprios — principalmente porque lidam com dados de naturezas diferentes:

* Logs
* Métricas
* Traces

> O formato dos dados, os protocolos de transmissão e os modelos de armazenamento variam bastante conforme o tipo de dado. Mesmo dentro de um único tipo, não há consenso universal sobre como estruturar ou transmitir essas informações.

> Além disso, a forma como usamos esses dados também varia: um sistema pode precisar fazer buscas em texto livre, analisar eventos individuais, detectar padrões históricos, visualizar fluxos de requisições ou encontrar gargalos de desempenho. Essas necessidades impactam diretamente o modo como projetamos o armazenamento, os tipos de consulta e as ferramentas de análise.

<img width="750" height="354" alt="image" src="https://github.com/user-attachments/assets/129156e9-1f8b-47e5-bc11-48b3a750ded4" />

Ter sistemas dedicados para logs, métricas e traces é o motivo pelo qual costumamos nos referir a eles como os três pilares da observabilidade. A noção de "pilares" oferece uma boa estrutura mental porque destaca os seguintes pontos:

* Existem diferentes categorias de telemetria
* Cada pilar tem suas próprias características e pode ser útil de forma independente
* Os pilares se complementam e precisam ser combinados para formar uma base sólida para alcançar a observabilidade
