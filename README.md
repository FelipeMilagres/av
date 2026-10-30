Vamos seguir com a opção 1.

Utilize a variável "CI_PIPELINE_ID" do GitLab para identificar as execuções realizadas pela pipeline.

Para o horário, utilize o timezone "America/Sao_Paulo", garantindo que a data e hora apresentadas no Test Run correspondam ao horário local.

Regras:

- Execução via GitLab: utilizar "CI_PIPELINE_ID".
- Execução local: utilizar "LOCAL" como identificador.
- Sempre incluir data e horário no título.
- Manter o padrão de nomenclatura já definido:

"API Automation | {nomeApi} | {DD-MM-YYYY HH:mm} | {identificador}"

Centralize o tratamento de data, horário e identificação da execução, evitando duplicidade de lógica.
