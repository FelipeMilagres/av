Avaliação do desafio de automação Mobile — Reinaldo Matheus

Status final: Aprovado com ressalvas

Checklist de avaliação
1. Foram criados 10 cenários de teste que cobrem as principais funcionalidades do aplicativo?
Status: Atendido. A solução contempla os principais fluxos funcionais previstos no desafio, incluindo autenticação, navegação, formulários e interações com a interface.
2. Os cenários incluem login/cadastro, navegação entre telas, preenchimento de formulários e mensagens de erro?
Status: Atendido. Os testes enviados contemplam os quatro grupos de cenários solicitados.
3. O padrão Page Object foi implementado corretamente?
Status: Atendido. O código separa elementos e ações em classes específicas por tela, com uma classe base para comportamentos reutilizáveis.
4. A solução utiliza arquivo de dados para data-driven testing?
Status: Atendido. O arquivo login.json é utilizado para parametrizar os testes de login com diferentes credenciais.
5. O código é reutilizável e demonstra capacidade de escrever testes de forma eficiente?
Status: Atendido. A solução utiliza métodos compartilhados, classe base e Page Objects, favorecendo a organização e a reutilização do código.
6. O projeto está configurado para executar testes em emuladores Android e iOS?
Status: Atendido parcialmente. Existem configurações específicas para as duas plataformas. Foi necessário ajustar dependências e configurações para viabilizar a execução. O Android executou sem falhas, enquanto o iOS apresentou uma falha na localização do botão button-Active.
7. A solução integra-se com o BrowserStack para execução em dispositivos reais?
Status: Atendido parcialmente. A configuração de integração está presente, mas não foram apresentadas evidências de execução na plataforma.
8. A captura automática de screenshots de falhas está configurada?
Status: Atendido. A configuração prevê a captura de screenshots em caso de falha e sua anexação ao relatório Allure.
9. Foram gerados relatórios detalhados de testes?
Status: Atendido. Foi apresentado relatório Allure com resumo dos resultados e informações do ambiente de execução.
10. Os relatórios incluem resumo, screenshots, logs e informações do ambiente?
Status: Atendido parcialmente. O relatório apresenta informações relevantes sobre a execução e o ambiente, mas não foi possível confirmar a presença de todos os anexos e logs previstos.
11. A pipeline GitLab CI/CD foi configurada para automatizar a execução dos testes?
Status: Atendido. O arquivo .gitlab-ci.yml contempla a execução dos testes, a geração de relatórios e a publicação de artefatos.
12. A pipeline demonstra capacidade de executar testes em ambientes diferentes?
Status: Atendido parcialmente. A configuração contempla execução via BrowserStack, mas não foram apresentadas evidências de execução integrada da pipeline nos diferentes ambientes.
13. O código-fonte completo foi entregue via GitHub ou GitLab?
Status: Atendido. Foram disponibilizados arquivos de código, configurações e documentação para a avaliação, embora existam divergências entre os arquivos enviados e os logs de execução.
14. O README contém instruções de configuração do ambiente e execução dos testes?
Status: Atendido parcialmente. A documentação descreve instalação, configuração, execução e geração de relatórios, mas apresenta inconsistências em relação à estrutura dos arquivos e aos comandos disponíveis.

Comentário consolidado para o card

O candidato desenvolveu uma solução de automação mobile utilizando JavaScript, WebdriverIO, Appium, Mocha e Chai. A solução contempla os principais fluxos de login, cadastro, navegação, formulários e validações de erro, utilizando Page Objects, dados parametrizados via JSON, relatórios Allure e configuração de CI/CD.

Durante a avaliação, foram necessários ajustes em dependências e configurações para viabilizar a execução do projeto. Após os ajustes, a execução local no Android ocorreu sem falhas. No iOS, houve uma falha no teste de formulário, relacionada à localização do botão button-Active.

A solução possui configuração para BrowserStack e GitLab CI/CD, porém não foram apresentadas evidências de execução bem-sucedida nessas integrações. Também foram identificadas inconsistências entre os arquivos enviados, a documentação e os logs de execução.

De forma geral, o candidato demonstra conhecimento prático em automação mobile e atende aos principais requisitos do desafio. Considerando os resultados obtidos e os pontos de atenção identificados, o desafio fica Aprovado com ressalvas.