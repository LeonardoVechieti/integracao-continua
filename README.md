# Integração Contínua - Projeto Golang

Este projeto utiliza GitHub Actions para automação de lint, testes e build de um projeto em Golang. O workflow é acionado automaticamente para branches específicas e executa uma série de etapas para garantir a qualidade do código.

## Requisitos

- Golang v1.22
- Docker e Docker Compose
- GitHub Secrets para variáveis de banco de dados:
  - `DB_HOST`
  - `DB_PASSWORD`
  - `DB_USER`
  - `DB_NAME`
  - `DB_PORT`

## Workflow de Integração Contínua

### Gatilhos

O workflow é acionado nas seguintes condições:
- **push** para a branch `main`
- **pull request** direcionado à branch `main`

### Jobs

#### `ci` - Continuous Integration

Executado no ambiente Ubuntu mais recente com os seguintes passos:

1. **Checkout do código**
   - Usa o repositório local para a execução.

2. **Setup do Go**
   - Instala a versão 1.22 do Go.

3. **Inicialização do Banco de Dados**
   - Usa o Docker Compose para subir um container PostgreSQL.

4. **Lint**
   - Executa o `golangci-lint` para verificar a qualidade do código nas pastas `controllers/`, `database/`, `models/` e `routes/`.

5. **Testes**
   - Executa os testes unitários especificados no arquivo `main_test.go` usando as variáveis de ambiente do banco de dados, que são fornecidas via `GitHub Secrets`.

6. **Build**
   - Compila o arquivo `main.go`.

7. **Upload do artefato**
   - Após a compilação, o artefato resultante é armazenado e disponibilizado.

## Como Configurar o Projeto

1. Clone este repositório:
   ```bash
   git clone <url_do_repositorio>
   cd <nome_do_projeto>
