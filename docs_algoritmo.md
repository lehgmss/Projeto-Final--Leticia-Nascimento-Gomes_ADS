# 🧩 Descrição em Linguagem Algorítmica – Sistema Odonto Vida

## 🔷 Algoritmo Principal do Sistema

Algoritmo OdontoVida

    Enquanto sistema_ativo = verdadeiro Faça

        Exibir menu principal
        Ler opção escolhida pelo usuário

        Escolha opção
            Caso 1:
                Executar cadastrarPaciente
            Caso 2:
                Executar listarPacientes
            Caso 3:
                Executar atualizarPaciente
            Caso 4:
                Executar excluirPaciente
            Caso 5:
                Executar cadastrarConsulta
            Caso 6:
                Executar listarConsultas
            Caso 7:
                Executar atualizarConsulta
            Caso 8:
                Executar excluirConsulta
            Caso 0:
                sistema_ativo ← falso
            OutroCaso:
                Mostrar "Opção inválida"
        FimEscolha

    FimEnquanto

FimAlgoritmo

---

## 🔷 Procedimentos Relacionados a Pacientes

### 🟦 Cadastrar Paciente
Procedimento cadastrarPaciente
    Ler nome, telefone, email
    Se nome = vazio OU telefone = vazio OU email = vazio Então
        Mostrar "Dados obrigatórios não preenchidos"
        Retornar
    FimSe

    SQL ← "INSERT INTO pacientes (nome, telefone, email) VALUES (nome, telefone, email)"
    ExecutarSQL(SQL)

    Mostrar "Paciente cadastrado com sucesso!"
FimProcedimento

---

### 🟦 Listar Pacientes
Procedimento listarPacientes
    SQL ← "SELECT * FROM pacientes"
    registros ← ExecutarSQL(SQL)

    Para cada registro em registros Faça
        Mostrar registro.nome, registro.telefone, registro.email
    FimPara
FimProcedimento

---

### 🟦 Atualizar Paciente
Procedimento atualizarPaciente(id)
    SQL ← "SELECT * FROM pacientes WHERE id = id"
    registro ← ExecutarSQL(SQL)

    Se registro = nulo Então
        Mostrar "Paciente não encontrado"
        Retornar
    FimSe

    Ler novos dados
    SQL ← "UPDATE pacientes SET nome = novoNome, telefone = novoTelefone, email = novoEmail WHERE id = id"
    ExecutarSQL(SQL)

    Mostrar "Paciente atualizado com sucesso!"
FimProcedimento

---

### 🟦 Excluir Paciente
Procedimento excluirPaciente(id)
    SQL ← "SELECT * FROM pacientes WHERE id = id"
    registro ← ExecutarSQL(SQL)

    Se registro = nulo Então
        Mostrar "Paciente não encontrado"
        Retornar
    FimSe

    SQL ← "DELETE FROM pacientes WHERE id = id"
    ExecutarSQL(SQL)

    Mostrar "Paciente removido"
FimProcedimento

---

## 🔷 Procedimentos Relacionados a Consultas

### 🟩 Cadastrar Consulta
Procedimento cadastrarConsulta
    Ler paciente, data, descrição

    Se paciente vazio OU data inválida OU descrição vazia Então
        Mostrar "Dados inválidos"
        Retornar
    FimSe

    SQL ← "INSERT INTO consultas (data_consulta, descricao, paciente_id) VALUES (data, descricao, paciente)"
    ExecutarSQL(SQL)

    Mostrar "Consulta cadastrada!"
FimProcedimento

---

### 🟩 Listar Consultas
Procedimento listarConsultas
    SQL ← "SELECT consultas.*, pacientes.nome AS paciente FROM consultas JOIN pacientes ON pacientes.id = consultas.paciente_id ORDER BY data_consulta DESC"
    registros ← ExecutarSQL(SQL)

    Para cada registro em registros Faça
        Mostrar registro.data_consulta, registro.descricao, registro.paciente
    FimPara
FimProcedimento

---

### 🟩 Excluir Consulta
Procedimento excluirConsulta(id)
    SQL ← "SELECT * FROM consultas WHERE id = id"
    registro ← ExecutarSQL(SQL)

    Se registro = nulo Então
        Mostrar "Consulta não encontrada"
        Retornar
    FimSe

    SQL ← "DELETE FROM consultas WHERE id = id"
    ExecutarSQL(SQL)

    Mostrar "Consulta removida"
FimProcedimento
