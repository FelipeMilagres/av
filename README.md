Adequar o script de transformação do ETL ao padrão dos cenários da tribo

### Contexto
O projeto **`kanbanize-lambdatest-migration`** realiza a extração dos cards e cenários de teste do Kanbanize, a transformação dos dados para o formato esperado pelo LambdaTest e o carregamento dos cenários na plataforma de destino.

A migração é realizada de forma incremental, por tribo, board e time, com disponibilização dos cenários migrados e das respectivas evidências em pastas específicas no Drive.

### Objetivo
Migrar os cenários de teste do time para o LambdaTest e disponibilizá-los em uma pasta específica, permitindo que os squads realizem posteriormente a organização dos cenários nas respectivas estruturas dos projetos.

### Escopo da atividade
- Extrair e preparar os cenários de teste do Kanbanize.
- Executar o processo de transformação e carregamento dos cenários no LambdaTest.
- Disponibilizar os cenários migrados em uma pasta específica, seguindo o padrão `Migração - <Nome do Time>`.
- Registrar as evidências da execução do processo de migração.
- Disponibilizar os cenários para que os squads realizem sua organização nas pastas correspondentes aos projetos.

### Evidências da entrega
- Planilha com os cenários exportados.
- Preview do terminal demonstrando a execução do processo.
- Evidência da execução dos testes unitários.
- Captura de tela dos cenários disponibilizados no LambdaTest.

### Critérios de conclusão
- Cenários previstos no escopo migrados para o LambdaTest.
- Pasta do time criada e cenários disponibilizados conforme o padrão definido.
- Evidências da migração armazenadas no Drive e acessíveis para consulta.
- Link da pasta de evidências registrado nos comentários do card.

**Fora do escopo:** a reorganização dos cenários dentro das pastas específicas de cada projeto, que será realizada pelos respectivos squads.



**Entrega concluída — Migração de cenários para o LambdaTest**

A migração dos cenários de teste do time foi concluída por meio do projeto `kanbanize-lambdatest-migration`, e os cenários foram disponibilizados no LambdaTest, seguindo o padrão de organização definido para a iniciativa.

As evidências da execução foram armazenadas no Drive, contemplando a planilha de cenários exportados, o preview do terminal, a execução dos testes unitários e a captura dos cenários migrados.

**Evidências da entrega:** [Inserir link da pasta do Drive]

Os cenários estão disponíveis para que o squad realize a organização nas respectivas pastas dos projetos, conforme sua estrutura e necessidade.