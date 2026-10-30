Vamos seguir com a opção 1: manter o padrão de nomenclatura originalmente definido, sem incluir o ambiente no título.

O ambiente continuará sendo uma variável obrigatória ("LAMBDATEST_ENVIRONMENT") para identificar e controlar corretamente a execução, mas não deverá fazer parte do título do Test Run.

Padrão definitivo:

- Pipeline: "API Automation | {nomeApi} | {DD-MM-YYYY HH:mm} | Pipeline #{CI_PIPELINE_ID}"
- Local: "API Automation | {nomeApi} | {DD-MM-YYYY HH:mm} | LOCAL"

Manter o timezone "America/Sao_Paulo".

Não confundir a identificação da origem da execução (Pipeline ou LOCAL) com o ambiente utilizado (HML, MOCK etc.).

Preservar o ambiente como informação de configuração e, caso suportado, como metadado complementar do Test Run.
