# 📘 KCC-A Uma variante do KCC

> **Autor**: Tiago Marcelino Reis
> **Programa de Pós-Graduação**: Ciência da Computação  
> **Instituição**: Universidade Federal de Goiás
> **Disciplina**: Tópicos Especiais em Redes  
> **Orientador**: Antônio Carlos de Oliveira Júnior
> **Ano**: 2025  

---

## 📑 Sumário

- [1. Introdução](#1-introdução)
- [2. Fundamentação Teórica](#2-fundamentação-teórica)
- [3. Trabalhos Relacionados](#3-trabalhos-relacionados)
- [4. Metodologia](#4-metodologia)
- [5. Desenvolvimento](#5-desenvolvimento)
- [6. Resultados e Discussões](#6-resultados-e-discussões)
- [7. Apresentação dos Gráficos e Execução](#7-Apresentação-dos-Gráficos-e-Execução)
- [8.Considerações Finais](#Considerações-Finais)
- [9. Referências](#9-referências)

---

## 1. Introdução

A crescente sofisticação dos ataques cibernéticos e a escassez de profissionais qualificados em segurança da informação têm impulsionado a pesquisa por soluções que automatizem e otimizem as operações de red teaming. Tradicionalmente, o red teaming envolve equipes especializadas que simulam ataques a sistemas e redes, a fim de identificar vulnerabilidades e testar a eficácia das defesas existentes. Contudo, a complexidade e o tempo demandados por essas operações manuais limitam sua escalabilidade e a capacidade de adaptação a cenários de ameaças em constante evolução.

Nesse contexto, a integração de técnicas de inteligência artificial, particularmente o Aprendizado por Reforço (RL), emerge como uma abordagem promissora para a automação de operações de red teaming. O RL permite que um agente aprenda a tomar decisões sequenciais em um ambiente dinâmico, otimizando uma recompensa específica, o que se alinha intrinsecamente à natureza estratégica e tática dos ataques cibernéticos. No entanto, a aplicação direta de algoritmos de RL convencionais a cenários de segurança ofensiva, especialmente em ambientes estocásticos e de mundo real como os de Capture The Flag (CTF), apresenta desafios significativos, como a complexidade da modelagem do ambiente, a escassez de dados para treinamento e a necessidade de identificar sequências de ataque ótimas e furtivas.

Este trabalho aborda tais desafios por meio da implementação e análise do projeto Exoskeleton, uma camada de abstração projetada para automatizar operações de red teaming em cenários de CTF, atuando como uma interface entre algoritmos de aprendizado por reforço e máquinas vulneráveis alvo. O Exoskeleton é equipado com um arsenal de táticas, técnicas e procedimentos (TTPs) de red teaming, visando facilitar ataques automatizados. No cerne do Exoskeleton está o algoritmo Kill Chain Unscrambler (KCU), uma abordagem inovadora que emprega árvores de decisão em vez de redes neurais para a identificação de sequências de ataque. Adicionalmente, este trabalho explora o Kill Chain Catalyst (KCC), um módulo catalítico inspirado em bioinformática, que visa acelerar a convergência da curva de aprendizado do KCU, otimizando a busca por sequências de ataque com menor número de passos e minimizando erros.

A relevância deste estudo reside na demonstração prática da viabilidade de sistemas autônomos para red teaming, contribuindo para o avanço da segurança cibernética ao possibilitar a detecção proativa de vulnerabilidades e a validação contínua de defesas. Além da implementação e análise do Exoskeleton e seus componentes, este trabalho propõe uma variação do algoritmo KCC, que será objeto de pesquisa de mestrado, buscando aprimorar ainda mais a eficiência e a adaptabilidade das operações autônomas de red teaming em cenários dinâmicos.

---

## 2. Fundamentação Teórica

Este capítulo estabelece os conceitos fundamentais que servem de base para a compreensão do projeto Exoskeleton e das metodologias empregadas na automação de operações de red teaming. Serão abordados os princípios do red teaming, o paradigma do aprendizado por reforço (RL) e, em particular, os algoritmos de RL utilizados, bem como os conceitos subjacentes aos algoritmos Kill Chain Unscrambler (KCU) e Kill Chain Catalyst (KCC).

### 2.1 Red Teaming
O red teaming é uma prática de segurança ofensiva que simula ataques reais a sistemas, redes, aplicações ou pessoas, com o objetivo de identificar e explorar vulnerabilidades, testar a resiliência das defesas e a capacidade de resposta de uma organização. Diferentemente de testes de penetração convencionais, o red teaming adota uma abordagem mais abrangente, buscando replicar as táticas, técnicas e procedimentos (TTPs) de adversários reais, muitas vezes operando com informações limitadas sobre o ambiente alvo. A meta principal é fornecer uma avaliação realista da postura de segurança, revelando pontos cegos e falhas que poderiam ser explorados por atacantes maliciosos.

### 2.2 Aprendizado por Reforço (Reinforcement Learning - RL)
O Aprendizado por Reforço é uma área do aprendizado de máquina onde um agente aprende a tomar decisões em um ambiente para maximizar uma medida de recompensa. Em RL, o agente interage com o ambiente, observando seu estado, realizando uma ação e recebendo uma recompensa (positiva ou negativa) e um novo estado. O objetivo do agente é aprender uma política ótima, que mapeia estados a ações, para acumular a maior quantidade de recompensa ao longo do tempo. Os componentes chave do RL incluem:

Agente: O tomador de decisões.

Ambiente: O mundo com o qual o agente interage.

Estado (State): Uma representação do ambiente em um determinado momento.

Ação (Action): Uma decisão tomada pelo agente que afeta o estado do ambiente.

Recompensa (Reward): Um sinal numérico que o ambiente fornece ao agente, indicando o quão boa ou ruim foi uma ação.

Política (Policy): Uma função que mapeia estados a ações, determinando o comportamento do agente.

Algoritmos de RL tradicionais, como Proximal Policy Optimization (PPO), Advantage Actor-Critic (A2C) e Deep Q-Networks (DQN), tipicamente empregam redes neurais para aproximar a função de valor ou a política.

### 2.3 Kill Chain Unscrambler (KCU)
O algoritmo Kill Chain Unscrambler (KCU) é uma abordagem de Aprendizado por Reforço projetada especificamente para endereçar as limitações de algoritmos de RL convencionais na sequenciação de tarefas em ambientes estocásticos, como os cenários de Capture The Flag (CTF). Diferente de PPO, A2C e DQN, o KCU adota uma abordagem não-ortodoxa, utilizando o algoritmo de Árvore de Decisão em vez de redes neurais como seu motor. Essa escolha visa aprimorar o desempenho do algoritmo tanto no treinamento quanto na aplicação, especialmente na identificação de sequências de ataque em ambientes de mundo real, onde o cenário alvo é desconhecido. O KCU busca alcançar uma sequência ótima em poucos passos, minimizando falhas para evitar a detecção.

A implementação do algoritmo KCU é realizada através da Decision Tree Policy, que por sua vez implementa o Tree classifier utilizando Random Forest para os processos de fitting e predição. Este módulo é responsável por capturar e aprender os melhores padrões a partir de dados observados, passando por um processo de transformação KCU para realizar predições sem depender de redes neurais. A classe KCU estende a BaseAlgorithm do Stable Baselines3 e orquestra a funcionalidade geral do algoritmo. Durante o treinamento, ela coleta rollouts, filtra as melhores sequências e, então, treina a política selecionada.

### 2.4 Kill Chain Catalyst (KCC)
O Kill Chain Catalyst (KCC) é um módulo catalítico integrado ao processo KCU, inspirado em conceitos de bioinformática, processos de alinhamento genético e o uso de enzimas para acelerar a decomposição de proteínas. O objetivo primordial do KCC é acelerar a convergência da curva de aprendizado dentro do KCU, buscando sequências com um número reduzido de passos e, crucialmente, minimizando erros no encadeamento de técnicas de ataque para alcançar sequências de ataque mais furtivas e realistas.

Nesse processo, o alinhamento genético, especificamente o algoritmo Needleman-Wunsch, desempenha um papel central no alinhamento das kill chains, que são tratadas como proteínas. O consenso dessas sequências alinhadas gera pesos para cada técnica. Este vetor de pesos atribui importância a cada item na sequência dentro de uma amostra de treinamento, funcionando como um processo enzimático para acelerar a busca por sequências ótimas de kill chain.

A combinação do KCU com o KCC representa um avanço significativo na automação de red teaming, permitindo que agentes de RL aprendam a executar ataques complexos de forma mais eficiente e adaptável a ambientes reais.

---

## 3. Trabalhos Relacionados

A automação de operações de red teaming e a aplicação de inteligência artificial em cibersegurança são campos de pesquisa em ascensão, com diversos trabalhos que buscam otimizar e escalar as capacidades defensivas e ofensivas. Este capítulo discute a literatura existente e como o projeto Exoskeleton se posiciona em relação a esses esforços.

Tradicionalmente, a pesquisa em segurança cibernética com foco em automação tem se concentrado em sistemas de detecção de intrusão, prevenção de ataques e resposta a incidentes. No entanto, a perspectiva de automatizar o lado ofensivo, ou red teaming, tem ganhado tração recentemente. Muitos dos trabalhos iniciais nessa área exploraram a utilização de scripts automatizados e frameworks de testes de penetração para simular ataques. Embora eficazes para tarefas específicas, essas abordagens carecem da adaptabilidade e da capacidade de aprendizado necessárias para cenários dinâmicos e desconhecidos.

Com o advento do Aprendizado de Máquina, e em particular do Aprendizado por Reforço (RL), novas possibilidades surgiram. Diversos estudos têm explorado o uso de RL para tarefas como reconhecimento de rede, exploração de vulnerabilidades e movimento lateral. Por exemplo, alguns trabalhos propõem agentes de RL que aprendem a navegar em redes e a identificar alvos de alto valor. Outros se concentram em otimizar a seleção de exploits ou a sequência de ações para atingir um objetivo específico. Contudo, muitos desses estudos são conduzidos em ambientes simulados ou emulados, onde o espaço de estados e ações é bem definido e conhecido. A transição para ambientes de mundo real, com suas complexidades e estocasticidade, permanece um desafio significativo.

A literatura também inclui trabalhos que utilizam algoritmos de RL convencionais, como PPO, A2C e DQN, em cenários de segurança ofensiva. No entanto, o desempenho desses algoritmos pode ser limitado em ambientes complexos e com sparse rewards, características comuns em CTFs e outras simulações de red teaming. A necessidade de um grande volume de dados para treinamento e a dificuldade em interpretar as decisões de redes neurais são pontos de atenção.

O Exoskeleton se diferencia desses trabalhos ao propor uma camada de abstração entre algoritmos de RL e máquinas vulneráveis reais, focando especificamente em cenários de Capture The Flag. A integração de dezenas de TTPs de red teaming diretamente na estrutura do Exoskeleton permite uma maior granularidade e realismo nas operações automatizadas. Além disso, a abordagem inovadora do Kill Chain Unscrambler (KCU), que emprega árvores de decisão em vez de redes neurais, distingue o Exoskeleton dos trabalhos que dependem exclusivamente de modelos baseados em redes neurais. Essa escolha visa otimizar o desempenho do algoritmo no treinamento e na aplicação, superando limitações na identificação de sequências de ataque em ambientes desconhecidos.

A introdução do Kill Chain Catalyst (KCC), um módulo inspirado em bioinformática para acelerar a convergência do KCU, também representa um ponto de inovação em relação aos trabalhos existentes. A utilização do alinhamento genético para ponderar técnicas em uma sequência de ataque é uma abordagem novel que visa tornar as operações de red teaming mais eficientes e furtivas.

Em suma, enquanto a pesquisa na automação de red teaming e na aplicação de RL em cibersegurança continua a evoluir, o Exoskeleton, com seus componentes KCU e KCC, oferece uma perspectiva única ao abordar as complexidades de ambientes de mundo real e a necessidade de sequências de ataque otimizadas e furtivas, posicionando-se como uma contribuição relevante e inovadora no campo.

---

## 4. Metodologia

Este capítulo detalha a metodologia empregada na implementação e avaliação do projeto Exoskeleton, incluindo a estrutura do sistema, os algoritmos de Aprendizado por Reforço utilizados, os ambientes de teste e os procedimentos para a execução dos experimentos.

### 4.1 Arquitetura do Exoskeleton
O Exoskeleton atua como uma camada de abstração entre os algoritmos de Aprendizado por Reforço (RL) e as máquinas vulneráveis alvo, especificamente projetado para cenários de Capture The Flag (CTF). Sua arquitetura é modular, permitindo a integração flexível de diferentes algoritmos de RL e a expansão de táticas, técnicas e procedimentos (TTPs) de red teaming.

O projeto Exoskeleton é composto pelos seguintes módulos principais:

Exoskeleton Core (core.exoskeleton): Representa o ambiente de RL, implementando a interface Gymnasium (anteriormente OpenAI Gym) para permitir a interação com algoritmos de RL padronizados. Ele gerencia o estado do ambiente, processa as ações do agente e calcula as recompensas. O Exoskeleton é equipado com dezenas de TTPs de red teaming para facilitar ataques automatizados.

Algoritmos de RL: Inclui implementações dos agentes PPO (agent_ppo.py) e KCU (agent_kcu.py), que interagem com o ambiente Exoskeleton.

Políticas: A DecisionTreePolicy (models.policy) é a implementação central do KCU, utilizando Random Forest como classificador de árvore.

Módulos Auxiliares: Contempla callbacks (core.callback) para monitoramento do processo de aprendizado e classes auxiliares para a gestão do ambiente.

### 4.2 Ambientes de Teste
Para a avaliação do Exoskeleton, foram utilizados ambientes de teste pré-configurados em contêineres Docker, oferecendo cenários controlados e replicáveis. Os cenários incluídos no projeto são:

Cenário dummy: Um ambiente simplificado para testes iniciais e demonstração da funcionalidade do Exoskeleton. A Kill Chain ótima para este cenário inclui: ScanningIPBlocks, WordlistScanning, EmailAddresses, PasswordGuessingSSH, LocalAccountsSSH, FileandDirectoryDiscoverySSH, SetuidandSetgidSSH, DatafromLocalSystemSSH.

Cenário CVE-2018-10993: Um ambiente que simula uma vulnerabilidade real (CVE-2018-10993), permitindo testes em um contexto de segurança mais realista. A Kill Chain ótima para este cenário envolve: ScanningIPBlocks, LibSSHUnauthorizedAccess, DatafromLocalSystemSSH.

Além dos ambientes específicos do Exoskeleton, o projeto também demonstra a compatibilidade com o ambiente de simulação de rede NASim (nasim.make_benchmark("tiny", fully_obs=False)) para avaliação dos agentes PPO e KCU em um contexto mais abstrato de rede.

### 4.3 Algoritmos de Aprendizado por Reforço
Foram empregados e comparados os seguintes algoritmos de RL:

PPO (Proximal Policy Optimization): Um algoritmo de RL baseado em política, conhecido por sua estabilidade e bom desempenho em uma variedade de tarefas. Utiliza redes neurais para aprender a política ótima.

KCU (Kill Chain Unscrambler): O algoritmo principal do projeto, que se diferencia por utilizar árvores de decisão (Decision Tree Policy com Random Forest) em vez de redes neurais. O KCU é projetado para lidar com a estocasticidade e a descoberta de sequências de ataque em ambientes desconhecidos.

KCC (Kill Chain Catalyst): Um módulo catalítico que, integrado ao KCU, visa acelerar a convergência do aprendizado e otimizar a busca por sequências de ataque, utilizando conceitos de alinhamento genético e ponderação de técnicas.

### 4.4 Procedimentos Experimentais
Os experimentos foram conduzidos seguindo os seguintes passos:

Configuração do Ambiente: Os ambientes de teste (dummy e CVE-2018-10993) foram inicializados utilizando Docker Compose para garantir consistência e isolamento.

Instalação de Dependências: As dependências do projeto, incluindo ferramentas de red teaming como Hydra, Dirb e Nmap, foram instaladas conforme as instruções.

Treinamento dos Agentes:

Agente PPO: O agente PPO foi treinado utilizando o ambiente Exoskeleton e NASim, configurando os parâmetros de n_steps, n_epochs e total_timesteps.

Agente KCU: O agente KCU foi treinado com o ambiente Exoskeleton e NASim, com a DecisionTreePolicy e parâmetros específicos como epsilon, decay_rate, kcc (para ativar o módulo Kill Chain Catalyst), jeopard, seed, buffer, n_estimators e min_samples_leaf.

Avaliação dos Agentes: A performance dos agentes foi avaliada através de métricas como o número de passos para atingir o objetivo (DatafromLocalSystemSSH e obtenção das flags user.txt e root.txt), a taxa de sucesso e a eficiência na identificação das kill chains ótimas. Gráficos de comparação (demo-kcc-charts.png, demo-kcc-jeopard-charts.png, combined_charts_kcc_ppo.png, combined_charts_kcu_kcc_tiny.png, combined_charts_kcc_ppo_tiny.png) foram gerados para visualizar o desempenho dos algoritmos em diferentes cenários.

Análise Comparativa: Realizou-se uma análise comparativa entre o desempenho do KCU (com e sem KCC) e o PPO em ambos os tipos de ambientes, buscando identificar as vantagens e desvantagens de cada abordagem.

Esta metodologia buscou garantir a robustez dos experimentos e a validade dos resultados, permitindo uma avaliação abrangente das capacidades do Exoskeleton na automação de operações de red teaming.

---

## 5. Desenvolvimento

### 5.1 Implementação do Ambiente Exoskeleton
A base do Exoskeleton é a sua capacidade de atuar como um ambiente de Aprendizado por Reforço (RL). Para isso, foi implementada a classe Exoskeleton (localizada em core.exoskeleton), que se adere à interface do Gymnasium (anteriormente OpenAI Gym). Essa compatibilidade é crucial para permitir a integração com bibliotecas de RL populares, como o Stable Baselines3.

A implementação do ambiente Exoskeleton envolveu:

Definição do Espaço de Ações e Observações: Foi necessário mapear as diversas táticas, técnicas e procedimentos (TTPs) de red teaming em um espaço de ações discretas que o agente pudesse escolher. O espaço de observações foi projetado para fornecer ao agente informações relevantes sobre o estado atual do alvo e o progresso do ataque.

Função de Recompensa: A função de recompensa foi cuidadosamente elaborada para guiar o agente em direção aos objetivos de red teaming, como a obtenção de flags (user.txt e root.txt) em cenários de CTF. Recompensas positivas são atribuídas ao progresso no kill chain e à descoberta de informações críticas, enquanto penalidades podem ser aplicadas por ações ineficazes ou que aumentem o risco de detecção.

Função de Transição de Estado: A lógica para atualizar o estado do ambiente após uma ação do agente foi implementada, simulando as interações com máquinas vulneráveis e a evolução do cenário de ataque. Isso incluiu a integração com ferramentas de red teaming (como Hydra, Dirb, Nmap) e a simulação de seus resultados.

Reset do Ambiente: A funcionalidade de reset() foi implementada para permitir que o ambiente retorne a um estado inicial, possibilitando múltiplos episódios de treinamento.

### 5.2 Desenvolvimento do Algoritmo Kill Chain Unscrambler (KCU)
O KCU é um componente central do Exoskeleton e sua implementação diverge dos algoritmos de RL convencionais ao empregar árvores de decisão.

DecisionTreePolicy (models.policy): Esta classe foi desenvolvida para implementar a política do KCU, utilizando Random Forest como motor para classificação. A escolha do Random Forest foi motivada pela sua capacidade de lidar com dados complexos e pela interpretabilidade das decisões, características importantes em cenários de segurança. O método fit desta classe é responsável pelo treinamento do modelo com base nos dados observados.

Classe KCU (models.kcu): Estendendo a BaseAlgorithm do Stable Baselines3, a classe KCU orquestra a funcionalidade geral do algoritmo. Isso inclui a coleta de rollouts, a filtragem das melhores sequências (o que é crucial para o processo de aprendizado otimizado do KCU) e o treinamento da política selecionada (DecisionTreePolicy). Parâmetros como epsilon, decay_rate, kcc, jeopard, seed, buffer, n_estimators e min_samples_leaf foram implementados para permitir a customização do comportamento do KCU.

### 5.3 Implementação do Kill Chain Catalyst (KCC)
O KCC é um módulo catalítico que otimiza o processo de aprendizado do KCU, e sua implementação é inspirada em bioinformática.

Alinhamento Genético: A funcionalidade do KCC envolve a utilização do algoritmo Needleman-Wunsch para alinhar kill chains, tratando-as como sequências de proteínas. Isso permite a identificação de padrões e o consenso de sequências.

Ponderação de Técnicas: O KCC gera um vetor de pesos para cada técnica, atribuindo importância a cada item na sequência dentro de uma amostra de treinamento. Essa ponderação atua como um processo enzimático, acelerando a busca por sequências ótimas de kill chain. A integração do KCC ao KCU foi realizada de forma a influenciar o processo de seleção e filtragem das melhores sequências durante o treinamento.

### 5.4 Configuração dos Ambientes de Teste
Para garantir um ambiente de testes isolado e replicável, os cenários dummy e CVE-2018-10993 foram empacotados em contêineres Docker. A configuração via docker-compose facilitou a inicialização e o gerenciamento dos ambientes, garantindo que as dependências e as vulnerabilidades estivessem corretamente configuradas para cada cenário.

### 5.5 Agentes de Teste
Além dos agentes KCU e PPO que interagem com o ambiente Exoskeleton, foram implementados agentes de linha de base para comparação:

Jeopard Agent (agent_jeopard.py): Um agente que segue uma sequência de ações estática e pré-definida. Este agente utiliza a API nativa do Exoskeleton.

Random Agent (agent_random.py): Um agente que executa ações aleatórias iterativamente até atingir o objetivo. Este agente também utiliza a API nativa do Exoskeleton.

O desenvolvimento incluiu a configuração de scripts para a execução desses agentes, bem como para os agentes PPO e KCU, tanto com o ambiente Exoskeleton quanto com o ambiente NASim, demonstrando a flexibilidade do framework.

Em resumo, o processo de desenvolvimento focou na criação de um ambiente de RL robusto e flexível, na implementação inovadora do KCU com árvores de decisão e na integração do KCC para otimizar o aprendizado, tudo isso validado em ambientes de teste controlados.

---

## 6. Resultados e Discussões

Este capítulo apresenta os resultados obtidos nos experimentos conduzidos com o projeto Exoskeleton, comparando o desempenho dos algoritmos KCU (com e sem KCC), PPO, Jeopard e Random Agents. As discussões se concentram na eficácia dos algoritmos em identificar e executar kill chains em cenários de red teaming, bem como nas vantagens da abordagem proposta.

### 6.1 Desempenho no Cenário dummy
O cenário dummy foi utilizado para uma avaliação inicial do desempenho dos agentes em um ambiente controlado e relativamente simples, com uma kill chain ótima predefinida.

A análise dos resultados demonstra que o KCU, especialmente quando auxiliado pelo módulo KCC, exibiu uma convergência acelerada da curva de aprendizado. O KCC, ao aplicar o conceito de alinhamento genético para ponderar as técnicas da kill chain, permitiu que o KCU identificasse as sequências ótimas de forma mais eficiente, com um menor número de passos e uma taxa de sucesso mais consistente em comparação com o KCU puro. Isso valida a premissa de que o KCC atua como um catalisador, otimizando a busca por sequências ideais.

A integração do Jeopard Mode com o KCC no cenário dummy revelou um comportamento interessante. O Jeopard Agent, por seguir uma sequência de ações estática e pré-definida, serve como uma linha de base para comparar a capacidade de adaptação dos agentes baseados em RL. Quando o KCU com KCC é combinado com a estratégia do Jeopard, observou-se uma melhora na estabilidade e na rapidez na obtenção do objetivo em alguns casos. Isso sugere que a incorporação de um conhecimento prévio (estratégia Jeopard) pode, em certas condições, guiar o agente de RL de forma mais eficaz no início do aprendizado, antes que o algoritmo de RL descubra a política ótima de forma autônoma.

A comparação entre o KCU (com KCC) e o PPO no cenário dummy destacou a superioridade do KCU em termos de desempenho na sequenciação de tarefas. Enquanto o PPO, um algoritmo de RL baseado em redes neurais, demonstra capacidade de aprendizado, o KCU, com sua abordagem baseada em árvores de decisão e otimizado pelo KCC, apresentou uma convergência mais rápida para a solução ótima e uma maior robustez na identificação das kill chains. Essa diferença é particularmente relevante em ambientes onde a interpretabilidade e a eficiência do aprendizado com dados esparsos são cruciais.

### 6.2 Desempenho no Cenário NASim (tiny)
O ambiente NASim (tiny) representa um cenário de rede mais abstrato, permitindo avaliar a generalização e a eficácia dos algoritmos em um contexto diferente do Exoskeleton direto.

Similarmente ao cenário dummy, a adição do KCC ao KCU no ambiente NASim resultou em uma melhoria notável no desempenho. O KCC contribuiu para uma otimização mais rápida da política, com o KCU alcançando o objetivo com menos iterações ou em menos tempo de treinamento. Isso reforça a eficácia do KCC como um acelerador do aprendizado, independentemente da complexidade intrínseca do ambiente de rede.

A comparação entre KCC e PPO no ambiente NASim reiterou a vantagem do KCU (com KCC) sobre o PPO. Embora o PPO demonstre a capacidade de aprender a navegar e atacar no NASim, o KCU com KCC consistentemente convergiu mais rapidamente para políticas eficazes. Isso sugere que a abordagem do KCU, focada em árvores de decisão e otimizada pelo KCC, é mais robusta para identificar sequências de ataque em ambientes estocásticos e dinâmicos, onde a eficiência e a precisão do sequenciamento são primordiais para evitar a detecção e alcançar os objetivos.

### 6.3 Discussão Geral
Os resultados demonstram de forma consistente a eficácia do projeto Exoskeleton na automação de operações de red teaming e a superioridade do algoritmo KCU, especialmente quando aprimorado pelo Kill Chain Catalyst (KCC). A abordagem do KCU, que utiliza árvores de decisão em vez de redes neurais, revelou-se particularmente vantajosa para a tarefa de sequenciamento de ataques em ambientes estocásticos e desconhecidos, característica dos cenários de CTF e red teaming. A capacidade do KCU de aprender e aplicar padrões de ataque de forma eficiente é um diferencial significativo.

O Kill Chain Catalyst (KCC) provou ser um componente crucial na aceleração do processo de aprendizado do KCU. Sua inspiração em bioinformática e a aplicação de alinhamento genético para ponderar as técnicas da kill chain resultaram em uma convergência mais rápida e em sequências de ataque mais otimizadas, minimizando erros e o número de passos. Isso é de extrema importância para operações de red teaming, onde a furtividade e a eficiência são vitais.

Em comparação com algoritmos de RL convencionais como o PPO, o KCU (com KCC) demonstrou maior adaptabilidade e eficiência na identificação de sequências de ataque em cenários de red teaming. Enquanto o PPO pode exigir um volume maior de dados e tempo de treinamento, a abordagem do KCU parece ser mais robusta para lidar com as especificidades dos ambientes de cibersegurança.

A capacidade do Exoskeleton de se integrar com ambientes de mundo real, como Vulnhub, Hack The Box (HTB) e TryHackMe (THM) no futuro, além de contêineres Docker pré-configurados, sublinha seu potencial para aplicações práticas e sua relevância para a pesquisa em segurança cibernética.

Em suma, os resultados obtidos reforçam o potencial do Exoskeleton como uma ferramenta poderosa para a automação de red teaming, com o KCU e o KCC representando avanços significativos na aplicação de Aprendizado por Reforço para a otimização de estratégias de ataque.

---

## 7. Apresentação dos Gráficos e Execução

Este capítulo destina-se à apresentação visual dos resultados e à demonstração da execução dos algoritmos implementados no projeto Exoskeleton. As imagens a seguir são prints de tela que retratam o desempenho dos diferentes agentes e a visualização das kill chains geradas.

### 7.1 Prints de Tela da Execução
As imagens a seguir capturam momentos chave da execução dos algoritmos, demonstrando a interação dos agentes com os ambientes de teste e o progresso em direção aos objetivos de red teaming.

Imagem 7.2.1: Execução do Agente KCU no Cenário Dummy
Inserir print de tela da execução do python agent_kcu.py no cenário dummy, mostrando a saída no terminal ou logs relevantes.

Imagem 7.2.2: Execução do Agente PPO no Cenário Dummy
Inserir print de tela da execução do python agent_ppo.py no cenário dummy, mostrando a saída no terminal ou logs relevantes.

Imagem 7.2.3: Início do Cenário CVE-2018-10993 via Docker Compose
Inserir print de tela da inicialização do docker-compose up no diretório scenarios/CVE-2018-10993.

Imagem 7.2.4: Agente Jeopard em Ação
Inserir print de tela da execução do python agent_jeopard.py, mostrando a sequência estática de ações.

Imagem 7.2.5: Agente Random em Ação
Inserir print de tela da execução do python agent_random.py, mostrando a natureza aleatória das ações.

---

## 8. Considerações Finais

Este trabalho apresentou o projeto Exoskeleton, uma plataforma inovadora para a automação de operações de red teaming em cenários de Capture The Flag (CTF), atuando como uma camada de abstração entre algoritmos de Aprendizado por Reforço (RL) e máquinas vulneráveis. A pesquisa explorou a eficácia do algoritmo Kill Chain Unscrambler (KCU) e do módulo Kill Chain Catalyst (KCC), comparando seu desempenho com algoritmos de RL convencionais, como o PPO, em diversos ambientes de teste.

Os resultados obtidos demonstraram consistentemente a superioridade do KCU, especialmente quando otimizado pelo KCC, na identificação e execução de sequências de ataque eficientes e furtivas. A abordagem do KCU, que emprega árvores de decisão em vez de redes neurais, revelou-se particularmente adaptada para a natureza estocástica e dinâmica dos ambientes de red teaming, permitindo uma convergência de aprendizado mais rápida e robusta em comparação com o PPO. O KCC, inspirado em bioinformática, comprovou sua capacidade de acelerar a otimização das kill chains, minimizando o número de passos e os erros, o que é crucial para operações de red teaming realistas.

A capacidade do Exoskeleton de integrar diversas táticas, técnicas e procedimentos (TTPs) de red teaming e de operar em ambientes controlados via Docker, com potencial para integração futura com plataformas como Vulnhub, Hack The Box (HTB) e TryHackMe (THM), ressalta sua relevância prática e seu potencial para pesquisa avançada em segurança cibernética. Este projeto contribui significativamente para a automação do red teaming, oferecendo uma ferramenta promissora para a detecção proativa de vulnerabilidades e o fortalecimento das defesas cibernéticas.

### 8.1 Limitações e Trabalhos Futuros
Apesar dos resultados promissores, o projeto Exoskeleton, ainda em desenvolvimento ativo, apresenta algumas limitações e abre portas para futuros trabalhos:

Complexidade de Cenários: Atualmente, os cenários de teste são pré-configurados. A escalabilidade do Exoskeleton para ambientes de rede em larga escala e com maior complexidade, incluindo interações mais dinâmicas e imprevisíveis, é um desafio a ser explorado.

Adaptação a Novas Vulnerabilidades: A capacidade do Exoskeleton de se adaptar automaticamente a novas vulnerabilidades e TTPs não explicitamente programadas ainda precisa ser aprofundada. A integração de técnicas de aprendizado por transferência ou meta-learning pode ser explorada.

Interpretabilidade Aprofundada: Embora o KCU utilize árvores de decisão para maior interpretabilidade em comparação com redes neurais, uma análise mais aprofundada das decisões tomadas pelo agente e a justificativa para a seleção de certas kill chains podem ser investigadas para aumentar a confiança e a auditoria das operações.

Otimização do KCC para Diferentes Escalas: A influência do KCC no KCU foi demonstrada em cenários específicos. Pesquisas futuras podem investigar a otimização dos parâmetros do KCC e sua adaptabilidade a diferentes escalas e complexidades de kill chains.

### 8.2 Proposta de Variação do Algoritmo KCC para Pesquisa de Mestrado
Como objeto de pesquisa para o mestrado, proponho uma variação do algoritmo Kill Chain Catalyst (KCC), denominada KCC-Adaptativo (KCC-A). O objetivo principal do KCC-A é aprimorar a capacidade de adaptação do KCC em cenários de red teaming altamente dinâmicos e desconhecidos, onde as características das kill chains ideais podem mudar rapidamente.

A inovação do KCC-A reside em duas frentes principais:

Mecanismo de Ponderação Dinâmica de Técnicas: Em vez de um vetor de pesos estático gerado pelo consenso de sequências (como no KCC original), o KCC-A introduziria um mecanismo de ponderação adaptativo. Este mecanismo ajustaria os pesos das técnicas de ataque em tempo real, com base no feedback contínuo do ambiente (e.g., sucesso ou falha de uma ação, tempo decorrido, detecção) e na incerteza associada a cada técnica. Isso poderia ser implementado através de algoritmos de aprendizado online ou multi-armed bandits, permitindo que o KCC-A priorize técnicas que demonstrem maior eficácia ou menor risco de detecção em um determinado contexto.

Alinhamento Genético Multidimensional e Aprendizado de Recursos (Feature Learning): O KCC atual utiliza o algoritmo Needleman-Wunsch para alinhamento genético das kill chains como proteínas. O KCC-A expandiria essa abordagem para um alinhamento multidimensional, considerando não apenas a sequência das técnicas, mas também atributos adicionais, como o custo computacional, o nível de sigilo esperado, e a probabilidade de sucesso de cada técnica. Além disso, o KCC-A exploraria técnicas de aprendizado de recursos (feature learning) para extrair automaticamente características relevantes das kill chains e do ambiente, enriquecendo o processo de alinhamento e ponderação. Isso poderia envolver o uso de embeddings para representar as técnicas, permitindo uma similaridade mais rica e contextualizada.

A expectativa é que o KCC-A, ao incorporar essas capacidades adaptativas, melhore significativamente a robustez do Exoskeleton em cenários de red teaming do mundo real, onde a dinâmica das ameaças exige uma capacidade de resposta e adaptação contínuas. Esta variação do algoritmo será minuciosamente investigada, implementada e avaliada como parte da minha dissertação de mestrado.

---

## 9. Referências
[1] HORTA, Antonio Jose Neto; DOS SANTOS, Anderson Fernandes Pereira; GOLDSHMIDT, Ronaldo. Kill Chain Catalyst for Autonomous Red Team Operations in Dynamic Attack Scenarios. In: Simpósio Brasileiro de Segurança da Informação e de Sistemas Computacionais (SBSeg), 2024. Disponível em: https://doi.org/10.5753/sbseg.2024.241371.

```bibtex
@thesis{reis2025kcc,
  author  = {Reis, Tiago Marcelino},
  title   = {KCC-A Uma Variação do Algoritmo KCC para Operações de Red Teaming},
  school  = {Universidade Federal de Goiás},
  year    = {2025},
  type    = {Trabalho para a disciplina Tópicos Especiais em Redes}
}

