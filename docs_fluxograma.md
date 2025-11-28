# Fluxograma (Mermaid) - Sistema Odonto Vida

## Fluxograma Geral das Operações CRUD

```mermaid
flowchart TD
  A[Início - Requisição do Usuário] --> B{Requisição}
  B -->|Criar Paciente| C1[Form: preencher nome, telefone, email]
  C1 --> D1[Validar dados]
  D1 -->|Válido| E1[Executar INSERT INTO pacientes]
  D1 -->|Inválido| F1[Mostrar erro]

  B -->|Listar Pacientes| G1[Executar SELECT * FROM pacientes]
  G1 --> H1[Mostrar tabela de pacientes]

  B -->|Excluir Paciente| I1[Receber id do paciente]
  I1 --> J1[Executar DELETE FROM pacientes WHERE id=...]
  J1 --> K1[Atualizar lista]

  B -->|Criar Consulta| C2[Form: data, descrição, selecionar paciente]
  C2 --> D2[Validar dados]
  D2 -->|Válido| E2[Executar INSERT INTO consultas]
  D2 -->|Inválido| F2[Mostrar erro]

  B -->|Listar Consultas| G2[Executar SELECT JOIN pacientes]
  G2 --> H2[Mostrar tabela de consultas]

  E1 --> Z[Fim - Sucesso]
  J1 --> Z
  E2 --> Z
```

## Fluxograma - Detalhado: Criação de Paciente

```mermaid
flowchart TD
  A[Começar] --> B[Usuário envia formulário de paciente]
  B --> C{Campos preenchidos?}
  C -->|Não| D[Mostrar mensagem: "Preencha todos os campos"]
  C -->|Sim| E[Executar INSERT no banco]
  E --> F[Redirecionar para pagina de pacientes]
  F --> G[Fim]
```

## Fluxograma - Detalhado: Criação de Consulta

```mermaid
flowchart TD
  A[Começar] --> B[Usuário envia formulário de consulta]
  B --> C{Campos preenchidos e paciente selecionado?}
  C -->|Não| D[Mostrar erro]
  C -->|Sim| E[Executar INSERT em consultas]
  E --> F[Redirecionar para pagina de consultas]
  F --> G[Fim]
```
