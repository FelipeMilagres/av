Checklist de API — classificação e observações

1. Cobertura de testes da API - Não atendido

A automação cobre login, usuários e carrinhos, com cenários positivos e negativos. Entretanto, não contempla integralmente a API, e a quantidade de testes executados não comprova 100% de cobertura dos endpoints, parâmetros e regras de negócio.

2. Entendimento da arquitetura RESTful - Atendido

Os testes utilizam métodos HTTP adequados aos fluxos de consulta, criação, atualização e exclusão, validando códigos de status e respostas. Há também cobertura de regras de negócio e recursos protegidos por autenticação.

3. Cenários de falha - Atendido

Foram implementados cenários negativos para credenciais inválidas, campos obrigatórios, e-mails duplicados, IDs inválidos, ausência de token, estoque insuficiente e duplicidade de produtos, demonstrando preocupação com validações e comportamentos de erro.

4. Autenticação JWT - Atendido

A suíte contempla login com credenciais válidas, obtenção e utilização do token JWT em rotas protegidas, além de cenários de acesso sem token e tentativa de acesso administrativo por usuário sem permissão.

5. Legibilidade, modularidade e boas práticas - Parcialmente

O projeto está organizado por recurso, possui classe base compartilhada, utilitário para geração de dados e uso de bibliotecas apropriadas. Contudo, a organização estrutural não comprova, por si só, aderência integral às boas práticas esperadas para uma solução sustentável de nível sênior.

6. Gerenciamento de dados de teste - Parcialmente

O uso de Faker e de testes parametrizados favorece a geração de dados dinâmicos e reduz colisões. Entretanto, é necessário assegurar o isolamento, a limpeza e a repetibilidade dos dados, especialmente considerando a execução paralela e o uso de ambiente compartilhado.

7. Integração com pipeline de CI - Atendido

Existe workflow no GitHub Actions que inicializa a API via Docker Compose, configura o Java, executa os testes Maven e prevê etapas posteriores de geração e publicação de relatórios.

8. Geração e disponibilização de relatórios - Parcialmente

O projeto possui configuração do Allure e etapas para gerar, armazenar e publicar relatórios. Entretanto, a evidência de execução apresentada comprova o sucesso dos testes, mas não confirma isoladamente que todos os artefatos foram gerados e disponibilizados corretamente na pipeline.

9. Entrega do código-fonte - Atendido

A documentação referencia o repositório GitHub do projeto, e foram disponibilizados os arquivos de código, configuração, dados de teste e documentação necessários à avaliação.

10. Documentação dos testes - Atendido

O arquivo TESTING_API.MD apresenta o mapeamento das suítes, cenários, endpoints e validações, enquanto Requisitos.md relaciona os requisitos aos respectivos testes.

11. README e instruções de execução - Atendido

O README descreve pré-requisitos, dependências, estrutura do projeto, configuração do ambiente, comandos para executar as suítes e orientações para geração dos relatórios.

Resultado geral do desafio

Aprovado com ressalvas. A solução apresenta uma base consistente de automação de API, com cenários funcionais e negativos, autenticação, organização por recurso e integração contínua. As principais ressalvas estão na abrangência da cobertura, na garantia de repetibilidade dos dados e na comprovação da publicação dos relatórios. Para uma posição sênior, esses pontos devem ser aprofundados na entrevista técnica.