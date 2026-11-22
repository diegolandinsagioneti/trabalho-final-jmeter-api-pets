# Trabalho Final — Testes de Performance com Apache JMeter

## 📌 Objetivo

Este projeto foi desenvolvido como atividade prática da disciplina de **Automação de Testes de Performance**, com o objetivo de implementar e executar testes de carga utilizando o **Apache JMeter 5.6.3**.

O trabalho contempla dois modelos de carga: **modelo fechado (Closed Workload)** e **modelo aberto (Open Workload)**, realizando autenticação e operações de cadastro e consulta de pets em uma API REST.

## 🛠️ Tecnologias utilizadas

- Apache JMeter 5.6.3
- Node.js
- API REST com autenticação JWT
- GitHub para versionamento e entrega

## 🔗 API utilizada

Repositório original: https://github.com/tiagotaq/api-de-pets

A API é executada localmente no endereço:

`http://localhost:3000`

### Endpoints testados

| Método | Endpoint | Descrição |
|---|---|---|
| POST | /login | Autenticação e obtenção do token JWT |
| POST | /pets | Cadastro de um novo pet |
| GET | /pets | Consulta dos pets cadastrados |

Todas as operações de cadastro e consulta são realizadas após a autenticação.

## 📊 Cenários de teste

### 1. Modelo fechado — Closed Workload

Simula uma quantidade controlada de usuários virtuais executando repetidamente o fluxo de operações.

**Configuração:**
- 5 usuários virtuais
- Ramp-up de 5 segundos
- Duração de 60 segundos
- Loop infinito durante o período configurado

**Fluxo executado:**

1. Realizar login.
2. Extrair o token JWT.
3. Cadastrar um pet utilizando POST /pets.
4. Consultar os pets utilizando GET /pets.
5. Repetir o fluxo até o término da execução.

### 2. Modelo aberto — Open Workload

Simula novas execuções chegando à aplicação de acordo com uma taxa definida, independentemente da conclusão das execuções anteriores.

**Configuração:**
- Taxa-alvo de 1 nova execução por segundo
- Duração de 60 segundos para novas chegadas
- Pausa final de 30 segundos
- Autenticação realizada em cada execução

**Fluxo executado:**

1. Realizar login.
2. Extrair o token JWT.
3. Cadastrar um pet utilizando POST /pets.
4. Consultar os pets utilizando GET /pets.

## 📈 Resultados dos testes

Os dois modelos foram executados e analisados utilizando o Aggregate Report do Apache JMeter.

| Indicador | Modelo fechado | Modelo aberto |
|---|---:|---:|
| Total de requisições | 5.537 | 180 |
| Tempo médio de resposta | 50 ms | 18 ms |
| Percentil 95 (P95) | 109 ms | 57 ms |
| Throughput | 92,2 req/s | 3,1 req/s |
| Taxa de erros | 0,00% | 0,00% |

### Análise dos resultados

O modelo fechado apresentou maior volume de requisições, devido à execução contínua de cinco usuários virtuais.

O modelo aberto apresentou um volume controlado de novas execuções, mantendo aproximadamente uma chegada por segundo.

Em ambos os cenários, as requisições executadas apresentaram **0% de erros**, demonstrando que a API respondeu corretamente às operações testadas sob as cargas configuradas.

## ▶️ Como executar o projeto

### Pré-requisitos

- Apache JMeter 5.6.3
- Node.js e npm
- API de Pets disponível localmente

### 1. Preparar a API

Clone o repositório original:

```bash
git clone https://github.com/tiagotaq/api-de-pets.git
```

Acesse a pasta do projeto:

```bash
cd api-de-pets
```

Instale as dependências:

```bash
npm install
```

Inicie a aplicação:

```bash
npm start
```

A API deverá estar disponível em `http://localhost:3000`.

### 2. Executar os testes no JMeter

1. Abra o Apache JMeter.
2. Importe o arquivo `Trabalho Final - Performance API Pets.jmx`.
3. Verifique as configurações da API e as credenciais de teste.
4. Habilite o Thread Group desejado.
5. Execute o teste.
6. Analise os resultados no Aggregate Report.

## ✅ Conclusão

O trabalho permitiu aplicar os conceitos de testes de performance baseados em modelos de carga aberto e fechado, utilizando o Apache JMeter.

Foram implementados fluxos de autenticação JWT, cadastro e consulta de pets, incluindo validações das respostas HTTP.

Os testes foram executados com sucesso, sem falhas registradas nas cargas avaliadas.

---

**Disciplina:** Automação de Testes de Performance

**Ferramenta:** Apache JMeter 5.6.3
