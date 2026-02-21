# api-escola
novo repositorio de api
Objetivos:
Permitir a criação, leitura, atualização e exclusão de registros essenciais (Alunos, Professores, Turmas, Disciplinas e Notas).
Eliminar o uso de planilhas isoladas, garantindo que a secretaria e os professores acessem de forma facil
Evitar perca de documentos importante
Evitar conflito de horarios 

Gets Previstos:
Método,Rota,Descrição,Acesso
GET,/alunos,Lista alunos com paginação,Admin / Secretaria
POST,/notas,Registra uma nova nota,Professor
GET,/meu-desempenho,Visualiza notas do usuário logado,Aluno
PUT,/turmas/{id},Altera horários ou sala de uma turma,Admin

Entidades do banco:
Usuarios = id (PK), nome, email, senha_hash, cpf, data_nascimento, tipo (Aluno, Professor, Admin), status (Ativo/Inativo).
Disciplinas: id (PK), nome, descricao, carga_horaria
Turmas: id (PK), codigo (ex: 9ANO-A-2026), ano_letivo, turno
Matricula: id, aluno_id (FK), turma_id (FK), data_matricula.
Alocacação: id, professor_id (FK), disciplina_id (FK), turma_id (FK)
Notas:id, matricula_id (FK), disciplina_id (FK), valor_nota, bimestre
Frequencia: id, matricula_id (FK), disciplina_id (FK), data, presenca
Relaçâo: Um para Muitos (1:N): Uma Turma tem muitos Alunos (via Matrícula); Muitos para Muitos (N:N): Um Professor pode dar várias Disciplinas, e uma Disciplina pode ser dada por vários Professores. 

Fluxo cliente
O professor preenche o formulário e clica em "Salvar". O navegador dispara uma requisição POST /notas contendo o JSON com os dados e um Token JWT no cabeçalho (Header) para provar quem ele é.
API (Server):
Middleware de Autenticação: A API verifica se o token é válido.
Middleware de Autorização: A API checa se o usuário tem a função (role) de "Professor".
Validação de Dados: O sistema confere se a nota está entre 0 e 10.
Controller/Service: A lógica de negócio processa a informação e solicita ao Banco de Dados a gravação.

