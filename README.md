
ORGANIZAÇÃO DE TEST CASES E TEST RUNS — LAMBDATEST TEST MANAGER

1. Objetivo

Padronizar a organização dos Test Cases e Test Runs no LambdaTest Test Manager, adotando uma estrutura orientada a APIs, independente da divisão organizacional por tribos ou times.

A proposta considera que uma mesma API pode ser compartilhada por diferentes equipes. Portanto, sua identificação, seus casos de teste e seu histórico de execução devem permanecer centralizados, sem duplicidade de registros.

A organização deverá seguir duas estruturas distintas:

- Test Cases: um card representando cada API.
- Test Runs: uma pasta por API, concentrando todo o histórico de execuções daquela API.

2. Organização dos Test Cases

Todos os cards referentes às APIs deverão ficar diretamente dentro de uma única pasta chamada:

"APIs"

Não deverá existir uma subpasta individual para cada API.

Estrutura esperada

All Test Cases:

- APIs
  - API - Conta
  - API - Clientes
  - API - Cartões
  - API - Limites
  - API - Contratos
  - API - Pix
  - API - ServeRest

Regras

1. Cada API deverá possuir exatamente um Test Case representativo.
2. Todos os Test Cases deverão ficar diretamente dentro da pasta "APIs".
3. O nome dos cards deverá seguir o padrão "API - {nomeApi}".
4. Não criar um Test Case individual para cada endpoint.
5. Não criar um Test Case individual para cada cenário automatizado.
6. Não organizar os cards por tribo ou time.
7. APIs compartilhadas entre equipes deverão possuir um único card.
8. O identificador do Test Case ("testCaseId") deverá ser utilizado pelo framework para identificar o card correspondente.

A existência de múltiplos endpoints ou cenários dentro de uma mesma API não deverá alterar essa estrutura.

Caso futuramente existam versões independentes de uma API, com contratos e ciclos de manutenção distintos, essa situação poderá ser avaliada separadamente.

3. Organização dos Test Runs

Diferentemente dos Test Cases, os Test Runs deverão possuir uma estrutura hierárquica, pois precisamos manter o histórico de execuções separado por API.

A pasta raiz deverá se chamar:

"APIs - Automação"

Dentro dela, deverá existir uma subpasta para cada API.

Estrutura esperada

All Test Runs:

- APIs - Automação
  - Conta
    - API Automation | Conta | Data | Build
    - API Automation | Conta | Data | Build
  - Clientes
    - API Automation | Clientes | Data | Build
  - Cartões
    - API Automation | Cartões | Data | Build
  - Limites
    - API Automation | Limites | Data | Build
  - Contratos
    - API Automation | Contratos | Data | Build
  - Pix
    - API Automation | Pix | Data | Build
  - ServeRest
    - API Automation | ServeRest | Data | Build

Regras

1. Todas as execuções automatizadas de APIs deverão ficar dentro de "APIs - Automação".
2. Cada API deverá possuir uma única subpasta.
3. Todos os Test Runs daquela API deverão ser armazenados dentro da respectiva subpasta.
4. Não criar uma pasta para cada execução.
5. Não criar pastas por endpoint.
6. Não criar pastas por cenário.
7. Não criar pastas por tribo ou time.
8. Não duplicar pastas de APIs compartilhadas entre equipes.
9. O nome das subpastas deverá corresponder ao nome da API, sem o prefixo "API -".

O objetivo é manter todo o histórico de execução de uma API em um único local.

4. Padrão de nomenclatura dos Test Runs

Cada execução deverá possuir uma identificação própria.

Utilizar o seguinte padrão:

"API Automation | {nomeApi} | {DD-MM-YYYY HH:mm} | {Build}"

Exemplo:

"API Automation | Conta | 30-10-2026 14:30 | Build 125"

Quando não houver identificação de build, como em execuções locais, utilizar um identificador alternativo apropriado.

Cada nova execução deverá gerar um novo Test Run, preservando o histórico anterior.

5. Mapeamento centralizado das APIs

Utilizar o arquivo existente:

"lambdatest.api-mapping.json"

O objetivo é manter uma configuração mínima, evitando armazenar informações que podem ser recuperadas dinamicamente pela API do LambdaTest.

A estrutura deverá conter somente:

- Identificador interno da API no framework.
- Nome oficial da API.
- Test Case ID correspondente.

Exemplo

{
  "serveRest": {
    "name": "ServeRest",
    "testCaseId": "01JM673DTFK066B51F5A8X0AGYG"
  },
  "conta": {
    "name": "Conta",
    "testCaseId": "ID_DO_TEST_CASE"
  }
}

Responsabilidade dos campos

- Chave principal: identificação interna utilizada pelo framework.
- "name": nome da API, utilizado para localizar sua pasta no Test Runs.
- "testCaseId": identificador do card correspondente na pasta "APIs" dos Test Cases.

Não adicionar ao arquivo:

- ID da pasta de Test Runs.
- ID do Test Run.
- Identificadores de endpoints.
- Informações estruturais que possam ser consultadas diretamente na ferramenta.

O mapeamento deverá ser a fonte central de relacionamento entre a API automatizada e seu Test Case.

6. Localização dinâmica das pastas dos Test Runs

O framework deverá localizar dinamicamente a pasta correspondente à API, sem exigir que seu identificador seja cadastrado manualmente no JSON.

O fluxo esperado será:

1. Recuperar o identificador do projeto LambdaTest.
2. Consultar a estrutura de pastas dos Test Runs por meio da API oficial.
3. Localizar a pasta raiz "APIs - Automação".
4. Recuperar as subpastas existentes.
5. Identificar a subpasta correspondente ao campo "name" do mapeamento.
6. Recuperar o identificador dessa pasta.
7. Utilizar esse identificador na criação do Test Run.

A consulta deverá ser otimizada, preferencialmente realizada uma única vez por execução, mantendo os identificadores recuperados em memória para reutilização.

Tratamento de situações excepcionais

- Pasta raiz inexistente: apresentar erro de configuração.
- Pasta da API inexistente: apresentar erro e não criar o Test Run em outro local.
- Nome duplicado ou ambíguo: interromper a operação para aquela API.
- API sem mapeamento: sinalizar a configuração incompleta.
- Test Case ID inválido: impedir a associação incorreta.

Não criar pastas automaticamente.

Importante: validar na documentação oficial se os endpoints necessários para listar e consultar as pastas dos Test Runs estão disponíveis. Não presumir que a recuperação dinâmica seja suportada sem comprovação.

Caso exista alguma limitação na API, apresentar a limitação e propor uma alternativa antes de implementar.

7. Relacionamento entre Test Cases e Test Runs

A associação lógica deverá seguir este modelo:

Elemento| Test Cases| Test Runs
Pasta raiz| APIs| APIs - Automação
Organização| Cards diretamente na pasta| Subpastas por API
Identificação| API - Conta| Conta
Identificador| Test Case ID| Folder ID recuperado dinamicamente
Finalidade| Representar a API| Armazenar o histórico de execuções

O framework deverá utilizar o mesmo cadastro centralizado para identificar a API e seu respectivo Test Case.

A localização da pasta de destino deverá ser realizada separadamente, por meio da consulta à estrutura do Test Runs.

Não presumir que o Test Case ID determina automaticamente o ID da pasta de destino.

8. Regras de manutenção e escalabilidade

A estrutura deverá permitir adicionar novas APIs sem necessidade de alterar a lógica central do framework.

Para cadastrar uma nova API, será necessário:

1. Criar seu Test Case dentro da pasta "APIs".
2. Utilizar o padrão de nomenclatura "API - {nomeApi}".
3. Criar a subpasta correspondente dentro de "APIs - Automação".
4. Adicionar a API ao "lambdatest.api-mapping.json", informando seu nome e Test Case ID.

Após esse cadastro, o framework deverá conseguir localizar automaticamente a pasta e utilizar os identificadores correspondentes.

Não realizar alterações estruturais no código para cada nova API.

9. Referências oficiais

Utilizar a documentação oficial para validar as operações de consulta e criação:

LambdaTest API Documentation:
https://www.lambdatest.com/support/api-doc/

Swagger / OpenAPI:
https://api.lambdatest.com/api-doc/

Não utilizar endpoints presumidos ou funcionalidades não documentadas.

10. Diretriz final

A organização deverá seguir obrigatoriamente o seguinte conceito:

TEST CASES

- Uma pasta raiz chamada "APIs".
- Todos os cards diretamente dentro dela.
- Um único Test Case por API.
- Nomenclatura "API - {nomeApi}".

TEST RUNS

- Uma pasta raiz chamada "APIs - Automação".
- Uma subpasta para cada API.
- Todos os Test Runs de uma mesma API dentro de sua respectiva pasta.
- Histórico de execuções preservado.

MAPEAMENTO

- Identificador interno da API.
- Nome da API.
- Test Case ID.
- Identificação dinâmica da pasta de Test Runs.

Não organizar por tribo, time, endpoint ou cenário.

O foco é manter uma estrutura simples, padronizada e escalável, considerando a API como um componente de negócio independente da estrutura organizacional das equipes.

Antes de implementar, analise a estrutura existente e apresente os ajustes necessários. Preserve as funcionalidades atuais e evite criar configurações redundantes.
