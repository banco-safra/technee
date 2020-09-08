# Technee

## Aspectos técnicos

### APIs

Estão disponibilizados alguns endpoints de APIs cujas chamadas e resultados simulam o que seriam algumas funcionalidades caso implementadas em ambiente produtivo.

As APIs seguem a abordagem arquitetural REST. Esta abordagem disponibiliza informações de sistemas através de URLs que respondem textos em JSON e utilizam recursos do protocolo HTTP. Esta abordagem é amplamente conhecida e com abundante material disponibilizado na internet.

Aquelas que tratam de consulta de informações bancárias foram inspiradas e são semelhantes às APIs do **Open Banking United Kingdom**. Assim, para informações mais completas além das presentes neste guia, consulte as [especificações](https://openbanking.atlassian.net/wiki/spaces/DZ/pages/16385802/Specifications) do Open Banking. As outras APIs fora do escopo do Open Banking foram inspiradas nos padrões do Open Banking, mas não haverá documentação no Open Banking United Kingdon sobre elas.

Para acesso às APIs, deve-se fazer um fluxo de Client Credentials do OAUTH2.0. Para maiores mais informações não presentes neste guia, consulte a [documentação oficial do OAUTH2.0](https://oauth.net/2/grant-types/client-credentials/).

#### Endpoints

São disponibilizadas funcionalidades através dos seguintes endpoints:

##### Consulta dados da conta
`GET [host]/open-banking/v1/accounts/{accountId}`

##### Consulta saldo da conta
`GET [host]/open-banking/v1/accounts/{accountId}/balances`

##### Consulta extrato da conta
`GET [host]/open-banking/v1/accounts/{accountId}/transactions`

##### Transfere valores entre contas
`GET [host]/accounts/v1/accounts/{accountId}/transfers`

##### Cadastra uma intenção de abertura de conta (Opt In)
`POST [host]/accounts/v1/optin`

##### Lista os Morning  Calls
`GET [host]/media/v1/youtube?{filtros via query strings}`

##### Consulta se a aplicação que fornece as APIs está funcionando
`GET [host]/health`

#### Host

O host `https://af3tqle6wgdocsdirzlfrq7w5m.apigateway.sa-saopaulo-1.oci.customer-oci.com/fiap-sandbox` deve ser adicionado antes do caminho de cada um dos endpoints acima.

Ex:

* `GET https://af3tqle6wgdocsdirzlfrq7w5m.apigateway.sa-saopaulo-1.oci.customer-oci.com/fiap-sandbox/health`
* `GET https://af3tqle6wgdocsdirzlfrq7w5m.apigateway.sa-saopaulo-1.oci.customer-oci.com/fiap-sandbox/accounts/v1/optin`

#### Parâmetros dos cenários simulados

Para acesso aos cenários simulados disponíveis com headers, bodies, query parameters etc., importe este [Postman Collection](https://github.com/banco-safra/technee/blob/master/documentacao-tecnica/technee.postman_collection.json) no [Postman](https://www.postman.com/).

Para entendimento do fluxo de negócio envolvido nos cenários simulados e outros detalhes técnicos, consulte este [documento em PDF](https://github.com/banco-safra/technee/blob/master/documentacao-tecnica/APIs.pdf)

#### OAUTH

Para acesso às APIs, um access token deve ser utilizado e enviado em todas as requisições. Para obtenção do access token:

1 - Concatene o client_id e secret enviado aos times separando-os com : (dois pontos). Ex:

abcedfgh_SEU_CLIENT_ID_abcedfgh:abcedfgh_SEU_SECRET_abcedfgh

2 - Converta em uma string em BASE64:

YWJjZWRmZ2hfU0VVX0NMSUVOVF9JRF9hYmNlZGZnaDphYmNlZGZnaF9TRVVfU0VDUkVUX2FiY2VkZmdo

3 - Submeta a string no header Authorization com o tipo Basic via POST no endpoint https://idcs-902a944ff6854c5fbe94750e48d66be5.identity.oraclecloud.com/oauth2/v1/token:

`Authorization: Basic YWJjZWRmZ2hfU0VVX0NMSUVOVF9JRF9hYmNlZGZnaDphYmNlZGZnaF9TRVVfU0VDUkVUX2FiY2VkZmdo`

4 - Com o access_token retornado, faça as chamadas nos outros endpoints (transfers, optin, balances etc.) passando-o no header Authorization com o tipo Bearer:

`Authorization: Bearer eyJ4NXQj...EuwHBw`

O modelo completo desta chamada encontra-se no [Postman Collection](https://github.com/banco-safra/technee/blob/master/documentacao-tecnica/FIAP.postman_collection.json) e no [documento em PDF](https://github.com/banco-safra/technee/blob/master/documentacao-tecnica/APIs.pdf).

## Suporte técnico

### Issues no GitHub
Podem ser abertos [Issues](https://github.com/banco-safra/technee/issues) no GitHub do Hackathon para **dúvidas técnicas** das APIs. 

Para verificar a disponibilidade do ambiente das APIs:
- o endpoint de health check (GET [host]/health) deve responder um HTTP Status Code 200 (Ok) utilizando um access token válido.

