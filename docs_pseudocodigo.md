# Pseudocódigo - Sistema Odonto Vida (CRUD)

## Entidade: Paciente

// Criação (Create)
PROCEDIMENTO CriarPaciente(nome, telefone, email)
  SE nome vazio OU telefone vazio OU email vazio ENTÃO
    RETORNE erro, "Campos obrigatórios"
  SENÃO
    executarSQL("INSERT INTO pacientes (nome, telefone, email) VALUES (nome, telefone, email)")
    RETORNE sucesso
  FIMSE
FIMPROCEDIMENTO

// Leitura (Read) - por id
FUNÇÃO ObterPacientePorId(id)
  registro <- executarSQL("SELECT * FROM pacientes WHERE id = id")
  SE registro existe ENTÃO
    RETORNE registro
  SENÃO
    RETORNE nulo
  FIMSE
FIMFUNÇÃO

// Listar todos (Read All)
FUNÇÃO ListarPacientes()
  lista <- executarSQL("SELECT * FROM pacientes")
  RETORNE lista
FIMFUNÇÃO

// Atualizar (Update)
PROCEDIMENTO AtualizarPaciente(id, nome, telefone, email)
  registro <- ObterPacientePorId(id)
  SE registro = nulo ENTÃO
    RETORNE erro, "Paciente não encontrado"
  SENÃO
    SE nome vazio OU telefone vazio OU email vazio ENTÃO
      RETORNE erro, "Campos inválidos"
    SENÃO
      executarSQL("UPDATE pacientes SET nome=nome, telefone=telefone, email=email WHERE id=id")
      RETORNE sucesso
    FIMSE
  FIMSE
FIMPROCEDIMENTO

// Exclusão (Delete)
PROCEDIMENTO DeletarPaciente(id)
  registro <- ObterPacientePorId(id)
  SE registro = nulo ENTÃO
    RETORNE erro, "Paciente não encontrado"
  SENÃO
    executarSQL("DELETE FROM pacientes WHERE id=id")
    RETORNE sucesso
  FIMSE
FIMPROCEDIMENTO


## Entidade: Consulta

// Criação (Create)
PROCEDIMENTO CriarConsulta(data_consulta, descricao, paciente_id)
  SE data_consulta inválida OU descricao vazio OU paciente_id inválido ENTÃO
    RETORNE erro, "Dados inválidos"
  SENÃO
    executarSQL("INSERT INTO consultas (data_consulta, descricao, paciente_id) VALUES (data_consulta, descricao, paciente_id)")
    RETORNE sucesso
  FIMSE
FIMPROCEDIMENTO

// Leitura (List / Read)
FUNÇÃO ListarConsultas()
  lista <- executarSQL("SELECT consultas.*, pacientes.nome AS paciente FROM consultas JOIN pacientes ON pacientes.id = consultas.paciente_id ORDER BY data_consulta DESC")
  RETORNE lista
FIMFUNÇÃO

// Exclusão (Delete)
PROCEDIMENTO DeletarConsulta(id)
  registro <- executarSQL("SELECT * FROM consultas WHERE id=id")
  SE registro = nulo ENTÃO
    RETORNE erro, "Consulta não encontrada"
  SENÃO
    executarSQL("DELETE FROM consultas WHERE id=id")
    RETORNE sucesso
  FIMSE
FIMPROCEDIMENTO
