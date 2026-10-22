# Documento de Consolidação
## Discovery de Gestão da Release Train

**Iniciativa:** Evolução do processo de gestão e acompanhamento das Release Trains  
**Card de referência:** 983307 — [Enabler] Discovery System Team  
**Equipes envolvidas:** Tooling and Integration / CE de Qualidade e System Team

## 1. Contexto e objetivo

Com o objetivo de aumentar a visibilidade, a rastreabilidade e a eficiência da gestão das Release Trains, as equipes de Tooling and Integration / CE de Qualidade e System Team realizaram um alinhamento técnico e funcional para definir a evolução do processo atual de acompanhamento das releases.

A iniciativa propõe substituir gradualmente a estrutura legada e os controles manuais realizados no Kanbanize por uma solução integrada ao LambdaTest (Test Manager), centralizando o acompanhamento das execuções de testes e permitindo a consolidação das métricas em dashboards no Looker, além da manutenção das notificações e dos resumos de progresso via Google Chat.

Este documento consolida o diagnóstico do processo atual, o modelo operacional proposto, os requisitos identificados, a divisão de responsabilidades e o plano de ação acordado durante o alinhamento referente ao card 983307 — [Enabler] Discovery System Team.

## 2. Participantes do alinhamento

- Felipe Milagres Guimarães — Tooling and Integration / CE de Qualidade.
- Francielle Fernandes Rocha — System Team.
- João Victor Tocilo Rossignoli EXT — System Team.

## 3. Diagnóstico do processo atual e modelo proposto

### 3.1. Processo atual — Kanbanize

O processo atual utiliza o Kanbanize para cadastrar cenários de teste, organizar as execuções e acompanhar o progresso das releases.

**Cadastro dos cenários:** os cenários são mantidos na raia de Cenários de Teste dos boards, contendo descrição, referência ao Figma, passos de execução, tags e informações complementares.

**Preparação das execuções:** a cada ciclo de testes, são criadas suites, aplicados filtros e realizadas clonagens de cards para organizar os cenários que serão executados. Esse modelo gera esforço operacional adicional e demanda manutenção de informações em estruturas distintas.

**Acompanhamento das releases:** as suites de teste são vinculadas aos cards de release no board de Gestão das Release Trains. Essas associações permitem acompanhar o percentual de progresso e alimentar as automações responsáveis pelas notificações no Google Chat.

### 3.2. Novo modelo proposto — LambdaTest

O modelo proposto utiliza os recursos do LambdaTest Test Manager para organizar os cenários e acompanhar as execuções, reduzindo a necessidade de clonagem e de controles paralelos.

**Organização por tribo e projeto:** os Test Cases serão organizados nos projetos correspondentes às tribos e aos times, contemplando passos de execução, tags, referências ao Figma e parâmetros personalizados.

**Execução por Test Runs:** os QAs selecionarão os cenários necessários e criarão Test Runs para cada ciclo de execução, como regressivos de Android e iOS ou fluxos específicos de negócio.

**Agrupamento por Milestones:** os Test Runs serão associados às Milestones correspondentes às releases, permitindo consolidar o progresso das execuções no nível da release e da tribo.

Essa estrutura será utilizada como base para a extração de dados pelas APIs do LambdaTest, alimentando as integrações e os dashboards previstos na iniciativa.

## 4. Requisitos funcionais e critérios de aceite

### 4.1. Visão por Squad e Tribo

**Necessidade:** visualizar o progresso das execuções de testes por Squad/Time e de forma consolidada por Tribo, considerando os resultados e os cenários ainda pendentes.

**Solução proposta:** consumir as APIs do LambdaTest para obter os dados dos Test Runs e das Milestones, estabelecendo os relacionamentos necessários para consolidar os indicadores.

**Critérios de aceite:**
- Disponibilizar a visão consolidada por Tribo e o detalhamento por Squad/Time.
- Apresentar os quantitativos de testes executados, aprovados, reprovados e pendentes, conforme os status disponíveis e as regras de cálculo acordadas.
- Definir e documentar as regras de cálculo dos percentuais de progresso.
- Garantir que as execuções sejam associadas à release correspondente.

### 4.2. Acompanhamento via Google Chat

**Necessidade:** manter o canal de comunicação atualizado com resumos periódicos das releases, facilitando o acompanhamento do progresso sem a necessidade de consultas manuais.

**Solução proposta:** integrar o bot do Google Chat às APIs do LambdaTest para consultar as informações de execução e disponibilizar os resumos de progresso.

**Critérios de aceite:**
- Consultar os dados de execução e progresso por meio das APIs do LambdaTest.
- Disponibilizar resumos das releases no canal definido.
- Preservar o funcionamento do bot durante o período de transição.
- Definir a periodicidade das atualizações e o formato das mensagens.

### 4.3. Dashboard consolidado no Looker

**Necessidade:** centralizar a visualização das métricas de execução de testes e, em uma evolução posterior, integrar informações de bugs do Kanbanize e Merge Requests do GitLab.

**Solução proposta:** desenvolver dashboards no Looker utilizando os dados de testes obtidos do LambdaTest e um repositório ou camada de dados que permita consolidar as diferentes fontes.

**Critérios de aceite:**
- Disponibilizar uma visão geral do progresso das releases e tribos.
- Permitir o detalhamento dos indicadores por Squad/Time.
- Documentar as fontes de dados e as regras de consolidação.
- Planejar a integração futura das informações de bugs e Merge Requests.

### 4.4. Modelo de transição e prova de conceito

**Necessidade:** realizar a adoção gradual do novo modelo sem comprometer as entregas das releases em andamento.

**Solução proposta:** iniciar com uma prova de conceito (POC) na Tribo de Cartão, utilizando a Release 16/26 como referência inicial, conforme o planejamento registrado na reunião.

**Critérios de aceite:**
- Realizar o ciclo de testes piloto utilizando o LambdaTest.
- Validar a organização dos cenários, as execuções e o vínculo com a release.
- Validar a consistência das informações utilizadas no acompanhamento.
- Definir os critérios para descontinuar o controle duplicado no Kanbanize para a tribo piloto.
- Registrar os aprendizados e os ajustes necessários antes da expansão para as demais tribos.

## 5. Divisão de responsabilidades e arquitetura técnica

### 5.1. Tooling and Integration / CE de Qualidade — Felipe Milagres

Responsável pela disponibilização dos recursos de acesso, apoio técnico à integração e evolução da estrutura de métricas.

Principais entregas:
- Criar e disponibilizar um usuário de serviço e as credenciais necessárias para consumo das APIs do LambdaTest pelo System Team.
- Fornecer a documentação Swagger e o detalhamento dos endpoints necessários para consultar Test Runs e Milestones.
- Apoiar a construção dos dashboards no Looker com as métricas de testes do LambdaTest.
- Apoiar o processo de migração dos cenários das demais tribos.
- Apoiar a análise de inconsistências nos dados e nos relacionamentos necessários para a consolidação das métricas.

As credenciais deverão ser disponibilizadas por um mecanismo seguro, com permissões compatíveis com a finalidade da integração.

### 5.2. System Team — João Victor e Francielle

Responsável pelo desenvolvimento da integração e pela evolução dos mecanismos de acompanhamento das releases.

Principais entregas:
- Implementar o consumo das APIs do LambdaTest pelo bot do Google Chat.
- Disponibilizar resumos e informações de progresso das releases.
- Manter a lógica atual do bot operacional durante o período de transição.
- Apoiar a validação funcional dos dados e dos indicadores utilizados no acompanhamento.
- Planejar a futura integração das informações do GitLab e do Kanbanize à camada central de dados, para enriquecimento dos dashboards do Looker.

## 6. Plano de ação e próximos passos

### 6.1. Disponibilização de acesso e documentação
**Responsável:** Tooling and Integration / CE de Qualidade.

Disponibilizar as credenciais do usuário de serviço e a documentação dos endpoints do LambdaTest necessários para a integração.

**Entrega esperada:** acesso técnico viabilizado e documentação disponível para desenvolvimento.

### 6.2. Integração com o Google Chat
**Responsáveis:** João Victor e equipe System Team.

Implementar o consumo das APIs do LambdaTest para manter o bot atualizado com as informações de progresso da Release 16/26.

**Entrega esperada:** bot consultando os dados do LambdaTest e disponibilizando os resumos acordados.

### 6.3. Execução da POC na Tribo de Cartão
**Responsáveis:** Tooling and Integration / CE de Qualidade e System Team, conforme suas respectivas frentes.

Executar o ciclo de testes piloto utilizando o LambdaTest, validando a organização dos cenários, os Test Runs, as Milestones e o acompanhamento da release.

**Entrega esperada:** processo piloto validado, com registro de inconsistências e ajustes necessários.

### 6.4. Desenvolvimento dos dashboards no Looker
**Responsáveis:** a definir entre as equipes envolvidas, conforme a divisão de trabalho acordada.

Construir as visões consolidadas de progresso por Tribo e o detalhamento por Squad/Time, utilizando os dados do LambdaTest.

**Entrega esperada:** dashboards com indicadores e regras de cálculo documentados e validados.

### 6.5. Evolução para uma visão unificada
**Responsáveis:** Tooling and Integration / CE de Qualidade e System Team.

Planejar a consolidação das informações de testes do LambdaTest, bugs do Kanbanize e Merge Requests do GitLab, permitindo uma visão integrada do andamento das releases.

**Entrega esperada:** estratégia de integração das fontes documentada, com definição das dependências e das etapas de implementação.

## 7. Pontos pendentes de definição

Os seguintes pontos devem ser detalhados antes da conclusão da implementação:

- **Definição das métricas:** regras de cálculo dos percentuais de progresso, tratamento de cenários reexecutados e definição dos status considerados.
- **Relacionamento entre entidades:** critérios para vincular Test Runs, Milestones, Squads, Tribos e releases.
- **Atualização dos dados:** periodicidade de consulta às APIs, atualização dos dashboards e envio das mensagens no Google Chat.
- **Transição operacional:** critérios para encerrar o controle duplicado no Kanbanize e expandir o modelo para as demais tribos.
- **Governança de acesso:** gestão das credenciais, permissões do usuário de serviço e procedimento para renovação ou revogação dos acessos.
- **Escopo do dashboard:** definição da primeira versão, priorizando as métricas provenientes do LambdaTest, e planejamento das integrações futuras com Kanbanize e GitLab.
- **Responsabilidade pela implementação do Looker:** confirmação dos responsáveis pela construção, manutenção e validação dos dashboards.

## 8. Anexos e evidências da reunião

- **Data:** 15/10/2026, às 10h34 (GMT-3).
- **Duração:** 16 minutos e 45 segundos.
- **Gravação:** Indicadores da release — reunião de 15/10/2026.
- **Transcrição:** Indicadores da release — transcript de 15/10/2026.

Os links da gravação e da transcrição devem ser mantidos junto a este documento para consulta e rastreabilidade das decisões registradas.