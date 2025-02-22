# Lab Cloud Run

Laboratório Cloud Run da Pós Graduação Go Expert FullCycle.

## Descrição

Foco: Desenvolver um sistema em Go que, ao receber um CEP, identifique a cidade e forneça a previsão do tempo, incluindo a temperatura em Celsius, Fahrenheit e Kelvin. O sistema deverá ser implantado no Google Cloud Run.

Requisitos: O sistema deve aceitar um CEP válido de 8 dígitos, buscar a localização correspondente e, com base nisso, obter as temperaturas, formatando-as em Celsius, Fahrenheit e Kelvin.

Cenários:

Em caso de sucesso:
- Código HTTP: 200
- Response Body: { "temp_C": 28.5, "temp_F": 28.5, "temp_K": 28.5 }
Em caso de falha, caso o CEP não seja válido (com formato correto):
- Código HTTP: 422
- Mensagem: invalid zipcode
​​​Em caso de falha, caso o CEP não seja encontrado:
- Código HTTP: 404
- Mensagem: can not find zipcode
- Deverá ser realizado o deploy no Google Cloud Run.

Dicas:

Utilize a API viaCEP (ou similar) para encontrar a localização que deseja consultar a temperatura: https://viacep.com.br/
Utilize a API WeatherAPI (ou similar) para consultar as temperaturas desejadas: https://www.weatherapi.com/
Para realizar a conversão de Celsius para Fahrenheit, utilize a seguinte fórmula: F = C * 1,8 + 32
Para realizar a conversão de Celsius para Kelvin, utilize a seguinte fórmula: K = C + 273
Sendo F = Fahrenheit
Sendo C = Celsius
Sendo K = Kelvin

Entrega:

O código-fonte completo da implementação.
Testes automatizados demonstrando o funcionamento.
Utilize docker/docker-compose para que possamos realizar os testes de sua aplicação.
Deploy realizado no Google Cloud Run (free tier) e endereço ativo para ser acessado.

## Executar o desafio

1. Inicie os containers Docker e execute a aplicação executando o seguinte comando na raiz do projeto:
`docker-compose up -d`

## Portas

- HTTP (web server): 8080

## Testes

1. Acesse o arquivo /api_test.go

2. Execute cada teste, selecionando o teste que deseja e clicando em "run test".

## Endereço do Cloud Run
https://cloud-run-54irf5cqoa-uc.a.run.app/cep?cep=41650000