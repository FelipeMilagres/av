Padrão de nomenclatura dos Test Runs

Adotar um padrão único de nomenclatura para todas as execuções automatizadas de APIs, contemplando tanto execuções realizadas via GitLab CI/CD quanto execuções locais.

Execução via Pipeline:

"API Automation | {nomeApi} | {ambiente} | {DD-MM-YYYY HH:mm} | Pipeline #{CI_PIPELINE_ID}"

Execução local:

"API Automation | {nomeApi} | {ambiente} | {DD-MM-YYYY HH:mm} | LOCAL"

Regras de preenchimento:

- "{nomeApi}": nome da API conforme o mapeamento centralizado.
- "{ambiente}": ambiente utilizado na execução (HML, MOCK etc.).
- "{DD-MM-YYYY HH:mm}": data e horário da execução, utilizando o timezone "America/Sao_Paulo".
- "CI_PIPELINE_ID": identificador da pipeline do GitLab, quando disponível.
- "LOCAL": identificador fixo para execuções realizadas fora da pipeline.

O framework deverá identificar automaticamente a origem da execução e aplicar o padrão correspondente, mantendo a nomenclatura centralizada em um único componente reutilizável.

Exemplos:

"API Automation | Conta | HML | 30-10-2026 14:35 | Pipeline #123456"

"API Automation | Conta | HML | 30-10-2026 14:35 | LOCAL"

Não incluir informações adicionais no título. Dados como branch, commit, job e URL da pipeline deverão permanecer como metadados complementares, quando suportados pelo LambdaTest.
