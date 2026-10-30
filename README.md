IMPLEMENTAÇÃO DE INTEGRAÇÃO COM LAMBDATEST TEST MANAGER

1. Contexto do projeto

O projeto atual de automação de APIs já está desenvolvido e funcional. Ele foi construído em JavaScript com Node.js e utiliza uma arquitetura centralizada para simular o comportamento do Postman, abstraindo a construção e execução das requisições HTTP.

A principal classe da arquitetura é a "BaseApiRequest", responsável por centralizar as operações relacionadas às requisições, incluindo sua construção, execução, tratamento das respostas e demais funcionalidades necessárias.

As demais classes possuem responsabilidades mais específicas: utilizam a "BaseApiRequest" para realizar as requisições e recebem os resultados para executar as validações e asserções dos cenários.

Premissa fundamental: não quero reconstruir, substituir ou refatorar desnecessariamente a arquitetura existente. O projeto já funciona e deve preservar suas funcionalidades, responsabilidades e padrões atuais. A implementação deve ser incremental, respeitando a estrutura existente.

2. Objetivo da implementação

Implementar a integração do framework com o LambdaTest Test Manager, permitindo que as execuções automatizadas sejam registradas, acompanhadas e rastreadas diretamente na ferramenta de gestão de testes.

A proposta é utilizar uma abordagem diferente da gestão tradicional de testes funcionais de interface.

Considerando a pirâmide de testes, a camada de API possui uma quantidade significativamente maior de cenários de validação do que a camada de interface.

Por exemplo:

- Um fluxo funcional de frontend pode possuir 10 cenários.
- As APIs envolvidas nesse mesmo fluxo podem possuir 100, 200 ou até 300 cenários de validação.

Portanto, não é interessante criar e gerenciar um caso de teste individual no board para cada cenário automatizado de API.

2.1. Modelo de gestão proposto

A proposta é trabalhar com o conceito de um card por API, no qual serão referenciados os cenários automatizados relacionados àquela API.

Cada card deverá possuir o mapeamento dos identificadores dos casos de teste cadastrados no LambdaTest Test Manager.

Dessa forma:

- O card representa a API que está sendo automatizada.
- Os cenários de automação ficam agrupados logicamente no código.
- Os IDs dos casos de teste do Test Manager são associados à API correspondente.
- A automação utiliza esses identificadores para realizar a integração e registrar os resultados das execuções.

O objetivo é evitar uma gestão excessivamente granular no board, mantendo a rastreabilidade necessária.

3. Documentação oficial e referências da API LambdaTest

Utilize obrigatoriamente a documentação oficial do LambdaTest como referência técnica para desenvolver a integração.

Referências:

- Documentação oficial da API: https://www.lambdatest.com/support/api-doc/
- Swagger / OpenAPI: https://api.lambdatest.com/api-doc/

Consulte especialmente os recursos relacionados ao Test Manager.

Antes de implementar qualquer funcionalidade, analise:

1. Endpoints disponíveis e respectivos métodos HTTP.
2. Parâmetros obrigatórios e opcionais.
3. Modelos de requisição e resposta.
4. Mecanismos de autenticação e autorização.
5. Operações de criação e gerenciamento de Test Runs.
6. Consulta e associação de Test Cases.
7. Atualização dos resultados de execução.
8. Upload e associação de evidências e relatórios.
9. Consulta de projetos, suítes e demais estruturas necessárias.
10. Limitações de tamanho, formato e envio de arquivos.

Diretriz obrigatória: não invente endpoints, métodos, parâmetros ou funcionalidades. Utilize exclusivamente recursos confirmados na documentação oficial.

Caso algum recurso necessário não esteja documentado, não seja suportado ou dependa de permissões específicas, sinalize a limitação antes de propor uma implementação alternativa.

Verifique também se os recursos identificados estão disponíveis para o modelo de licença e as permissões utilizados no ambiente.

4. Arquitetura da integração

A integração deverá respeitar a arquitetura atual do projeto.

Não concentre a comunicação com o LambdaTest dentro da classe "BaseApiRequest".

Essa classe deve continuar responsável pelas operações de requisição HTTP relacionadas à execução dos testes.

Crie uma camada específica para a integração com o LambdaTest Test Manager.

Como referência arquitetural, avalie a criação de componentes com responsabilidades semelhantes às seguintes:

- "LambdaTestManager": centraliza a comunicação com a API do Test Manager.
- "TestRunManager": gerencia a criação, atualização e finalização dos Test Runs.
- "TestCaseMapper": mantém o relacionamento entre APIs, cenários automatizados e IDs dos casos de teste.
- "EvidenceManager": gerencia a identificação e o envio dos relatórios e evidências.
- "NotificationManager": centraliza o envio das notificações de execução.

Esses nomes são sugestões, não uma exigência de implementação. Analise a estrutura existente e escolha a organização que melhor se adapte ao projeto, evitando abstrações desnecessárias.

A integração deverá ser modular, reutilizável e independente da lógica de execução das requisições.

5. Mapeamento dos cenários e APIs

O framework deverá possuir uma configuração centralizada que permita relacionar cada API aos respectivos IDs dos casos de teste cadastrados no LambdaTest Test Manager.

Exemplo conceitual:

API: Clientes

- Cenário: Consulta de cliente por CPF.
- Test Case ID: 12345.
- Cenário: Consulta de cliente inexistente.
- Test Case ID: 12346.
- Cenário: Consulta de cliente com CPF inválido.
- Test Case ID: 12347.

API: Cartões

- Cenário: Consulta de cartão ativo.
- Test Case ID: 22345.
- Cenário: Consulta de cartão bloqueado.
- Test Case ID: 22346.

O exemplo serve apenas para ilustrar o relacionamento esperado. A estrutura definitiva deverá considerar os padrões já existentes no projeto.

Requisitos:

- Permitir cadastrar novas APIs sem alterar a lógica central da integração.
- Permitir associar múltiplos cenários a uma mesma API.
- Identificar os cenários efetivamente executados.
- Recuperar os respectivos IDs no Test Manager.
- Evitar associações duplicadas ou incorretas.
- Permitir identificar cenários sem mapeamento e apresentar alertas apropriados.
- Não enviar para o Test Manager casos de teste que não participaram daquela execução.

6. Fluxo de execução e integração

Quando a automação for executada, principalmente por meio da pipeline CI/CD, o framework deverá realizar automaticamente as seguintes operações.

Etapa 1 — Identificação dos cenários

Identificar quais APIs e respectivos cenários estão sendo executados.

Utilizar o mapeamento previamente configurado no projeto para recuperar os IDs dos casos de teste correspondentes no LambdaTest Test Manager.

A integração deverá considerar somente os cenários efetivamente executados.

Etapa 2 — Criação do Test Run

Criar automaticamente um Test Run no LambdaTest Test Manager para representar a execução da automação de APIs.

Esse Test Run deverá seguir um padrão de nomenclatura que permita identificar facilmente:

- Tipo de execução: API Automation.
- Projeto ou aplicação.
- Data e horário da execução.
- Identificação da pipeline ou build.
- Outras informações relevantes para rastreabilidade.

Exemplo de nomenclatura:

"API Automation | [Projeto] | [DD-MM-YYYY HH:mm] | [Build]"

O Test Run deverá ser criado dentro de uma pasta ou estrutura específica destinada às execuções automatizadas de backend/API, mantendo a organização separada das execuções de frontend.

Após sua criação, os casos de teste mapeados deverão ser associados ao respectivo Test Run, utilizando os recursos oficialmente disponibilizados pela API.

Etapa 3 — Execução dos cenários

Após a criação do Test Run e a associação dos casos de teste, o framework deverá executar os cenários normalmente, sem modificar o comportamento atual da automação.

Os resultados deverão ser coletados de maneira estruturada, permitindo relacionar cada execução ao seu respectivo Test Case ID.

É importante garantir que o mecanismo de integração não interfira na execução dos testes e que uma falha de asserção não interrompa a coleta dos resultados dos demais cenários.

Etapa 4 — Atualização dos resultados

Após a execução dos cenários, atualizar automaticamente os resultados no LambdaTest Test Manager.

A integração deverá contemplar os seguintes comportamentos:

Em caso de sucesso:

- Registrar o resultado como "Passed".
- Anexar as evidências geradas pela automação.
- Associar corretamente o resultado ao caso de teste correspondente.
- Finalizar corretamente os casos de teste e o Test Run, conforme o fluxo suportado pela ferramenta.

Em caso de falha:

- Registrar o resultado como "Failed".
- Anexar as evidências disponíveis da execução, incluindo os relatórios gerados pela automação.
- Preservar as informações necessárias para identificar o cenário que apresentou erro.
- Registrar, quando suportado, a mensagem de erro e os detalhes da falha.
- Garantir que o resultado final do Test Run represente a falha ocorrida.

Importante: o envio das evidências deverá acontecer independentemente do resultado da execução, tanto para cenários aprovados quanto reprovados.

As evidências devem aproveitar os relatórios que o próprio framework já gera, evitando duplicidade de mecanismos de reporting.

Caso a ferramenta permita anexação de arquivos por caso de teste ou por execução, avalie a melhor estratégia considerando a rastreabilidade e as limitações da API.

Etapa 5 — Finalização do Test Run

Depois de atualizar todos os resultados e anexar as evidências:

- Garantir que todos os casos de teste executados tenham seus resultados registrados.
- Consolidar a quantidade de cenários aprovados e reprovados.
- Identificar eventuais cenários não executados ou não mapeados.
- Finalizar o Test Run utilizando o mecanismo oficialmente suportado pelo LambdaTest.

O resultado geral deverá refletir fielmente o resultado da execução automatizada.

Uma execução com pelo menos um cenário reprovado não poderá ser apresentada como uma execução totalmente aprovada.

Etapa 6 — Notificações

Ao finalizar a integração e a atualização dos resultados no Test Manager, disparar uma notificação automática informando o resultado da execução.

A notificação deverá contemplar a possibilidade de envio por e-mail e Google Chat, considerando os mecanismos disponíveis no ambiente.

Execução com sucesso:

- Identificação do projeto.
- Data e horário.
- Identificação da pipeline/build.
- Resultado geral da execução.
- Quantidade de cenários aprovados.
- Quantidade de cenários reprovados, se aplicável.
- Link para consultar o Test Run no LambdaTest.

Execução com falha:

- Identificação do projeto.
- Data e horário.
- Identificação da pipeline/build.
- Quantidade de cenários aprovados e reprovados.
- Identificação dos erros encontrados.
- Link para consultar o Test Run e suas evidências.

A notificação deverá ser enviada somente após a consolidação dos resultados, garantindo que as informações apresentadas correspondam ao estado final da execução.

7. Configurações e variáveis de ambiente

Centralizar as configurações necessárias em variáveis de ambiente (".env"), evitando informações sensíveis diretamente no código.

Avaliar a necessidade de variáveis para:

- Credenciais de autenticação do LambdaTest.
- URL base da API.
- Identificador do projeto no Test Manager.
- Identificador da suíte ou pasta de destino.
- Configurações relacionadas à integração.
- Configurações de notificação.
- Identificadores necessários para comunicação com o Google Chat.

Os nomes definitivos deverão seguir o padrão de nomenclatura já utilizado no projeto.

Garantir que:

- Tokens e credenciais nunca sejam expostos nos logs.
- O arquivo ".env" permaneça fora do versionamento.
- Exista um arquivo ".env.example" com as variáveis necessárias, sem credenciais reais.
- A integração possa ser habilitada ou desabilitada por configuração.
- As configurações locais e da pipeline sejam compatíveis.

8. Tratamento de erros e resiliência

A integração deverá possuir tratamento adequado para falhas de comunicação com o LambdaTest.

Considerar situações como:

- Erro de autenticação.
- Falta de permissão.
- Indisponibilidade da API.
- Timeout.
- Limite de requisições (rate limit).
- Erro na criação do Test Run.
- Erro na associação dos casos de teste.
- Erro na atualização dos resultados.
- Falha no upload das evidências.
- Falha no envio das notificações.

Implementar, quando apropriado:

- Logs estruturados.
- Tratamento de exceções.
- Retentativas controladas para falhas transitórias.
- Controle para evitar duplicidade de Test Runs.
- Registro das operações que falharam.
- Possibilidade de reprocessamento de etapas pendentes, quando tecnicamente viável.

Premissa importante: uma falha na integração com o Test Manager não deve apagar, sobrescrever ou comprometer os resultados produzidos pela automação.

O framework deverá preservar os resultados localmente, permitindo identificar o problema de integração e realizar uma recuperação posterior.

Avalie também a política de encerramento da pipeline: falhas nos testes devem reprovar a execução; falhas na integração devem ser identificadas separadamente, sem mascarar o resultado real dos testes.

9. Integração com a pipeline CI/CD

A integração deverá ser compatível com a execução automatizada pela pipeline existente.

Avalie o fluxo atual e identifique o melhor ponto para inicializar e finalizar a integração.

O comportamento esperado é:

1. Inicialização da pipeline.
2. Identificação do projeto e da execução.
3. Identificação dos cenários e respectivos IDs.
4. Criação do Test Run.
5. Associação dos casos de teste.
6. Execução da automação.
7. Coleta e consolidação dos resultados.
8. Atualização dos resultados no Test Manager.
9. Upload das evidências.
10. Finalização do Test Run.
11. Envio das notificações.
12. Encerramento da pipeline com o status correto.

Considerar a possibilidade de execução local e execução pela pipeline, mantendo o mesmo mecanismo de integração.

Quando executado localmente, permitir identificar a execução e registrar os resultados sem depender exclusivamente de variáveis disponibilizadas pelo CI/CD.

10. Diretrizes técnicas obrigatórias

A implementação deverá respeitar os seguintes princípios:

1. Não comprometer o funcionamento atual da automação.
2. Não concentrar a integração com o LambdaTest dentro da "BaseApiRequest".
3. Criar uma camada específica para integração com o LambdaTest Test Manager.
4. Reutilizar os padrões de código já existentes.
5. Evitar duplicidade de responsabilidades.
6. Não criar abstrações desnecessárias.
7. Centralizar as configurações necessárias em variáveis de ambiente.
8. Não expor tokens, senhas ou credenciais.
9. Reutilizar os relatórios e evidências já produzidos pelo framework.
10. Implementar tratamento de erros para falhas de comunicação.
11. Garantir a rastreabilidade entre API, cenário automatizado, Test Case ID e Test Run.
12. Evitar duplicidade de registros e associações incorretas.
13. Manter compatibilidade com a versão atual das dependências.
14. Preservar a possibilidade de execução independente do framework.
15. Criar testes para validar a própria camada de integração, preferencialmente utilizando mocks quando não for necessário acessar o LambdaTest real.

11. Estratégia de implementação

Antes de iniciar qualquer alteração, execute uma análise completa do projeto.

Fase 1 — Diagnóstico

1. Analise toda a estrutura atual do projeto.
2. Identifique as classes existentes, especialmente a "BaseApiRequest".
3. Entenda como os cenários são executados.
4. Identifique como os resultados são tratados.
5. Analise como os relatórios e evidências são gerados.
6. Identifique o mecanismo atual de execução na pipeline.
7. Verifique as dependências e versões utilizadas.

Fase 2 — Análise da API LambdaTest

1. Consulte a documentação oficial e o Swagger/OpenAPI.
2. Identifique os endpoints necessários.
3. Verifique os recursos disponíveis para criação de Test Runs.
4. Verifique como associar Test Cases.
5. Identifique como atualizar resultados.
6. Verifique como anexar evidências.
7. Identifique como finalizar uma execução.
8. Analise os requisitos de autenticação e permissões.

Fase 3 — Proposta arquitetural

Antes de modificar os arquivos, apresente:

- Diagnóstico da arquitetura atual.
- Componentes que serão criados.
- Componentes existentes que precisarão de ajustes.
- Estratégia de mapeamento dos cenários.
- Fluxo de comunicação com o LambdaTest.
- Estratégia de tratamento de erros.
- Variáveis de ambiente necessárias.
- Endpoints oficiais que serão utilizados.
- Possíveis limitações técnicas identificadas.

Fase 4 — Implementação incremental

Implemente a integração em etapas independentes e validáveis:

1. Autenticação e comunicação com o LambdaTest.
2. Mapeamento de APIs e Test Cases.
3. Criação do Test Run.
4. Associação dos casos de teste.
5. Atualização dos resultados.
6. Upload das evidências.
7. Finalização do Test Run.
8. Notificações.
9. Integração com a pipeline.
10. Testes e validação do fluxo completo.

Após cada etapa, valide o funcionamento antes de avançar para a próxima.

Não altere arquivos ou funcionalidades que não sejam necessários para a integração.

12. Resultado esperado

Ao final, quero ter um framework de automação de APIs que funcione de maneira independente para executar e validar os cenários, mas que também possua integração com o LambdaTest Test Manager.

O fluxo ideal será:

1. A pipeline inicia a execução da automação.
2. O framework identifica os cenários executados.
3. Recupera os IDs dos casos de teste associados às APIs.
4. Cria um Test Run para aquela execução.
5. Associa os casos de teste correspondentes.
6. Executa os cenários e coleta seus resultados.
7. Atualiza os resultados no Test Manager.
8. Anexa os relatórios e evidências da execução.
9. Finaliza o Test Run conforme o resultado.
10. Dispara a notificação de sucesso ou falha.

Objetivo final: ter rastreabilidade completa das execuções automatizadas de API no LambdaTest Test Manager, sem precisar cadastrar individualmente centenas de cenários no board, mantendo um modelo de gestão baseado em uma referência por API e com integração automatizada do início ao fim.

A implementação deverá priorizar a simplicidade, a reutilização e a manutenção, respeitando integralmente a arquitetura já existente no projeto.

Orientação final: antes de começar a codificação, apresente o diagnóstico e a proposta arquitetural. Não execute uma refatoração ampla nem tome decisões estruturais sem justificar sua necessidade. O foco é evoluir o template existente, não reconstruí-lo.
