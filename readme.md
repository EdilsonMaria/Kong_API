# Kong API Gateway com Konga e PostgreSQL

Este projeto demonstra a configuração e utilização de um API Gateway Kong com suporte a uma interface de gerenciamento web Konga, utilizando um banco de dados PostgreSQL. Além disso, um serviço simples é exposto por meio de containers Docker, permitindo fácil integração e testes locais.

## Estrutura do Repositório

O repositório contém as seguintes pastas:

### `kong_docker`
Contém o arquivo `docker-compose.yml` responsável por subir os seguintes serviços:
- **kong-database**: Serviço PostgreSQL utilizado pelo Kong para armazenamento de dados.
- **kong**: API Gateway Kong, configurado para gerenciar requisições de APIs.
- **konga**: Interface web para gerenciar o Kong.

### `service`
Contém um serviço simples escrito em Go com:
- **`main.go`**: Código que gera um serviço HTTP que responde com uma mensagem configurada via variável de ambiente.
- **`Dockerfile`**: Configuração para construir a imagem Docker do serviço.
- **`docker-compose.yml`**: Configuração para subir três instâncias do serviço simples, cada uma em um container.

## Objetivos

- Demonstrar como configurar e gerenciar um API Gateway usando o Kong.
- Expor um serviço simples por meio de múltiplos containers para testar balanceamento de carga e roteamento de APIs.
- Usar o Konga como interface para simplificar a configuração e monitoramento do Kong.

## Como Funciona

1. **Kong**: Atua como um gateway para gerenciar e proteger o acesso aos serviços backend.
2. **Konga**: Permite configurar e monitorar o Kong por meio de uma interface gráfica.
3. **PostgreSQL**: Armazena configurações e dados operacionais do Kong.
4. **Serviço Simples**: Exposto em três containers, simula um backend acessado via o gateway.

### Fluxo
1. O Kong é configurado para rotear requisições para os serviços Go.
2. O Konga é utilizado para configurar rotas, plugins e monitorar o gateway.
3. As requisições enviadas para o Kong são redirecionadas para os containers do serviço.

## Como Rodar Localmente

1. Clone o repositório:
   ```bash
   git clone <url-do-repositorio>
   cd <nome-do-repositorio>
   ```

2. Suba os serviços do Kong e Konga:
   ```bash
   cd kong_docker
   docker-compose up -d
   ```

3. Suba os serviços simples:
   ```bash
   cd ../service
   docker-compose up -d
   ```

4. Acesse os seguintes serviços:
   - **Kong Gateway**: [http://localhost:8000](http://localhost:8000)
   - **Konga Interface**: [http://localhost:1337](http://localhost:1337)
   - **Serviço Simples (via Kong)**: Configurado através do Konga para roteamento.

5. Configure rotas no Konga:
   - Acesse o Konga na porta `1337`.
   - Conecte-se ao Kong usando a URL `http://kong:8001`.
   - Configure rotas para o serviço simples exposto.

## Requisitos

- Docker e Docker Compose instalados.

