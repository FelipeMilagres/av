Vamos adotar a estratégia de bloqueio de publicação caso não seja possível garantir a associação do Test Run à pasta correta.

A organização por API é um requisito da arquitetura definida, portanto não devemos publicar execuções na raiz ou em pastas diferentes como fallback.

Antes de implementar:

1. Investigue os endpoints documentados e os recursos disponíveis no tenant LambdaTest.
2. Verifique se existe alguma operação suportada para associar o Test Run à pasta correspondente.
3. Caso a documentação pública não contemple esse recurso, avalie se existe suporte adicional disponibilizado pelo tenant.
4. Não utilize endpoints não documentados ou mecanismos presumidos.

Comportamento esperado:

- Se a associação à pasta for suportada, criar o Test Run normalmente no diretório correspondente à API.
- Se não for possível confirmar a associação, interromper a publicação e registrar um erro claro de integração.
- Preservar os resultados e relatórios localmente e como artefatos da pipeline.
- Não perder nem mascarar o resultado real dos testes por causa da falha de integração.

Não implementar fallback para a raiz do Test Runs.

Caso a funcionalidade não seja suportada, apresentar a limitação técnica e as alternativas disponíveis antes de prosseguir.
