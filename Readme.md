# Lab Cloud Run - API de CEP e Previsão do Tempo

Laboratório Cloud Run da Pós Graduação Go Expert FullCycle.

## Descrição

Esta API em Go, quando recebe um CEP, identifica a cidade correspondente e fornece a previsão do tempo, incluindo a temperatura em Celsius, Fahrenheit e Kelvin.

## Funcionalidades

- Recebe um CEP válido de 8 dígitos
- Busca a localização usando a API ViaCEP
- Obtém a previsão do tempo atual para a cidade usando a API WeatherAPI
- Retorna as temperaturas em Celsius, Fahrenheit e Kelvin

## Requisitos

- Docker e Docker Compose
- Go 1.19+ (para desenvolvimento local)
- Acesso à internet (para comunicação com as APIs externas)

## Como Executar

### Com Docker (Recomendado)

1. Clone o repositório:
   ```
   git clone https://github.com/seu-usuario/goexpert-cloud-run.git
   cd goexpert-cloud-run
   ```

2. Inicie os containers Docker:
   ```
   docker-compose up -d
   ```

3. A API estará disponível em: http://localhost:8080

## Testes 

### Executando testes localmente

```bash
# Todos os testes
go test -v

# Com cobertura
go test -cover -v
```

### Descrição dos Testes Automatizados

O arquivo `api_test.go` contém os seguintes testes:

- **TestInvalidCEP**: Verifica se a API retorna erro 422 quando um CEP inválido é fornecido
- **TestInvalidMethod**: Verifica se a API retorna erro 405 quando um método HTTP diferente de GET é usado
- **TestValidCEP**: Verifica se a API retorna as temperaturas corretamente para um CEP válido

## Testes Manuais

### Cenários de Teste

1. **CEP Válido**:
   ```
   curl http://localhost:8080/cep?cep=01001000
   ```
   **Resultado Esperado**: Código HTTP 200 com JSON contendo as temperaturas
   ```json
   { "temp_C": 28.5, "temp_F": 83.3, "temp_K": 301.5 }
   ```

2. **CEP com Formato Inválido**:
   ```
   curl http://localhost:8080/cep?cep=123
   ```
   **Resultado Esperado**: Código HTTP 422 com mensagem "invalid zipcode"

3. **CEP Não Encontrado**:
   ```
   curl http://localhost:8080/cep?cep=99999999
   ```
   **Resultado Esperado**: Código HTTP 404 com mensagem "can not find zipcode"

4. **Método HTTP Inválido**:
   ```
   curl -X POST http://localhost:8080/cep?cep=01001000
   ```
   **Resultado Esperado**: Código HTTP 405 com mensagem "Invalid request method"

## Deploy no Google Cloud Run

A aplicação está disponível publicamente no seguinte endereço:
https://cep-weather-service-522784420355.southamerica-east1.run.app

### Testando a Aplicação no Google Cloud Run

Você pode testar a aplicação implantada no Google Cloud Run usando os seguintes métodos:

#### Via Navegador

   - Acesse: https://cep-weather-service-522784420355.southamerica-east1.run.app/cep?cep=01001000
   - Resultado: Página com as temperaturas em JSON

#### Via Curl

1. Envie o CEP:
   ```bash
   curl https://cep-weather-service-522784420355.southamerica-east1.run.app/cep?cep=01001000
   ```

2. Execute a requisição e verifique a resposta

### Exemplos de CEPs para Teste

- **São Paulo (Centro)**: 01001000
- **Rio de Janeiro (Centro)**: 20010000
- **Salvador**: 40010000
- **Brasília**: 70040010
- **Curitiba**: 80010010