# Descrição em Linguagem Algorítmica - Sistema Odonto Vida

Algoritmo: Gerenciamento de Pacientes e Consultas

Variáveis:
  id: inteiro
  nome, telefone, email, descricao: texto
  data_consulta: data
  paciente_id: inteiro
  registros, registro: conjuntos/registro

Procedimentos:
  // Iniciar conexão com BD
  ConectarBanco():
    Abrir conexão com MySQL (host, user, pass, database)
    Se falha -> Mostrar erro e parar

  // Criar Paciente
  CriarPaciente(nome, telefone, email):
    Se nome = "" OU telefone = "" OU email = "" Então
      Mostrar("Dados obrigatórios não preenchidos")
      Retornar
    FimSe
    SQL <- "INSERT INTO pacientes (nome, telefone, email) VALUES (nome, telefone, email)"
    ExecutarSQL(SQL)
    Redirecionar para "pacientes.php"

  // Listar Pacientes
  ListarPacientes():
    SQL <- "SELECT * FROM pacientes"
    registros <- ExecutarSQL(SQL)
    Para cada registro em registros:
      Mostrar nome, telefone, email
    FimPara

  // Deletar Paciente
  DeletarPaciente(id):
    SQL <- "DELETE FROM pacientes WHERE id = " + id
    ExecutarSQL(SQL)
    Redirecionar para "pacientes.php"

  // Criar Consulta
  CriarConsulta(data_consulta, descricao, paciente_id):
    Se data_consulta inválida OU descricao = "" OU paciente_id <= 0 Então
      Mostrar("Dados inválidos")
      Retornar
    FimSe
    SQL <- "INSERT INTO consultas (data_consulta, descricao, paciente_id) VALUES (data_consulta, descricao, paciente_id)"
    ExecutarSQL(SQL)
    Redirecionar para "consultas.php"

  // Listar Consultas
  ListarConsultas():
    SQL <- "SELECT consultas.*, pacientes.nome AS paciente FROM consultas JOIN pacientes ON pacientes.id = consultas.paciente_id ORDER BY data_consulta DESC"
    registros <- ExecutarSQL(SQL)
    Para cada registro em registros:
      Mostrar data_consulta, descricao, paciente
    FimPara

FimAlgoritmo
