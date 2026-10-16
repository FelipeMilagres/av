Resultado da execução

Testes executados
17

Testes aprovados
13

Testes com falha
4

Taxa de aprovação
76,47%


Os quatro testes que falharam verificam comportamentos que a API ServeRest utilizada não atende: rejeição de e-mails duplicados com diferença entre maiúsculas e minúsculas, ocultação de senhas na listagem pública, restrição de cadastro de administradores fora do domínio esperado e bloqueio de exclusão sem autenticação. Esses resultados demonstram que a automação também foi utilizada para identificar limitações da API, embora os cenários não tenham sido aprovados.

Análise técnica

O candidato apresentou uma solução organizada em Cypress, com testes separados por funcionalidade, comandos reutilizáveis, uso de fixtures e configuração de evidências com Allure. A automação contempla fluxos de cadastro, autenticação, edição e exclusão de usuários, além de cenários negativos e verificações de segurança. Também demonstra conhecimento na integração com GitHub Actions e na geração de relatórios para acompanhamento das execuções.
Como ponto de atenção, a cobertura ainda não contempla integralmente o escopo previsto no desafio. Embora exista uma documentação ampla de cenários, parte deles não está implementada na suíte executada, especialmente em funcionalidades de produtos e em critérios complementares da heurística PREDADOR, como validações abrangentes de headers, contratos de resposta e limitação de requisições. O gerenciamento de dados pode ser aprimorado para garantir maior independência entre testes e estabilidade em execuções sucessivas.
As quatro falhas registradas estão relacionadas a comportamentos não atendidos pela API ServeRest e não devem ser interpretadas automaticamente como falhas na implementação dos testes. Entretanto, a execução também registrou um erro de preparação de login com e-mail vazio, que merece verificação para assegurar a confiabilidade da suíte. Apesar disso, os resultados demonstram que a maior parte dos cenários implementados foi executada com sucesso, com evidências disponíveis para análise.

Principais pontos positivos
- Boa organização dos testes e reutilização de comandos.
- Cobertura de fluxos positivos, negativos e cenários de segurança.
- Uso de fixtures e geração dinâmica de dados em parte dos testes.
- Integração com GitHub Actions e geração de relatórios Allure.
- Captura de evidências para apoiar a análise das falhas.

Principais pontos de atenção
- Ampliar a cobertura para atender melhor ao escopo solicitado.
- Evoluir a cobertura de headers, contratos de resposta e rate limit.
- Revisar a preparação dos dados de autenticação e a repetibilidade da execução.
- Alinhar a documentação de cenários à cobertura efetivamente automatizada.

Status do desafio de API

Aprovado com ressalvas

O candidato demonstra uma boa base técnica em automação de APIs, organização de código, testes negativos, integração contínua e relatórios. A solução atende aos principais aspectos estruturais, mas ainda possui oportunidades de evolução na abrangência da cobertura e na confiabilidade da execução.