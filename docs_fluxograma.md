# 📊 Fluxograma – Sistema Odonto Vida (CRUD)

A seguir estão os fluxogramas do sistema, representando os processos de Pacientes e Consultas.

---

## 🧩 Fluxograma Geral do Sistema (CRUD)

```mermaid
flowchart TD
    A[Início] --> B[Usuário seleciona operação]

    B --> C{Operação escolhida?}

    C -->|Cadastrar Paciente| CP[Formulário de Cadastro de Paciente]
    C -->|Listar Pacientes| LP[Listar registros da tabela Pacientes]
    C -->|Atualizar Paciente| AP[Formulário de Edição]
    C -->|Excluir Paciente| EP[Selecionar Paciente para Exclusão]

    C -->|Cadastrar Consulta| CC[Formulário de Cadastro de Consulta]
    C -->|Listar Consultas| LC[Listar registros da tabela Consultas]
    C -->|Atualizar Consulta| AC[Formulário de Edição de Consulta]
    C -->|Excluir Consulta| EC[Selecionar Consulta para Exclusão]

    %% ------- PACIENTES --------

    CP --> VCP{Dados válidos?}
    VCP -->|Não| ECP[Exibir mensagem de erro]
    VCP -->|Sim| ICP[INSERT no banco → tabela pacientes]
    ICP --> FIM[Fim]

    LP --> FIM

    AP --> VAP{Dados válidos?}
    VAP -->|Não| EAP[Erro na atualização]
    VAP -->|Sim| UAP[UPDATE pacientes]
    UAP --> FIM

    EP --> DEP{Paciente existe?}
    DEP -->|Não| EEP[Erro: paciente não encontrado]
    DEP -->|Sim| REP[DELETE pacientes]
    REP --> FIM

    %% ------- CONSULTAS --------

    CC --> VCC{Dados válidos?}
    VCC -->|Não| ECC[Erro no cadastro]
    VCC -->|Sim| ICC[INSERT consultas]
    ICC --> FIM

    LC --> FIM

    AC --> VAC{Dados válidos?}
    VAC -->|Não| EAC[Erro na atualização]
    VAC -->|Sim| UAC[UPDATE consultas]
    UAC --> FIM

    EC --> DEC{Consulta existe?}
    DEC -->|Não| EEC[Erro: consulta não encontrada]
    DEC -->|Sim| REC[DELETE consultas]
    REC --> FIM

