## Controle escola
### Objetivo
Criar um software para uma escola poder controlar o cadastro de professores, alunos e cursos.

## Rotas backend
| Rota | Descrição |
| --- | --- |
| `POST /professor` | Incluir um novo professor |
| `GET /professor` | Listar todos os professores |
| `GET /professor?nome={nome}` | Listar os professores filtrando por nome |
| `GET /professor/{id}` | Detalhar algum professor |
| `PUT /professor/{id}` | Editar algum professor |
| `DELETE /professor/{id}` | Deletar algum professor |

| `POST /curso` | Incluir um novo curso |
| `GET /curso` | Listar todos os cursos |
| `GET /curso?nome={nome}&categoria={categoria}&valor={valor}` | Listar os cursos filtrando por nome, categoria e valor |
| `GET /curso/{id}` | Detalhar algum curso |
| `PUT /curso/{id}` | Editar algum curso |
| `PUT /curso/{id}/adicionar-professor/{professorId}` | Adicionar professor à algum curso |
| `PUT /curso/{id}/adicionar-aluno/{alunoId}` | Adicionar aluno à algum curso |
| `DELETE /curso/{id}` | Deletar algum curso |

| `POST /aluno` | Incluir um novo aluno |
| `GET /aluno` | Listar todos os alunos |
| `GET /aluno?nome={nome}` | Listar os alunos filtrando por nome |
| `GET /aluno/{id}` | Detalhar algum aluno |
| `PUT /aluno/{id}` | Editar algum aluno |
| `DELETE /aluno/{id}` | Deletar algum aluno |

## Modelo (Professor)
- Identificador: `long`
- Nome: `string`
- Sobrenome: `string`
- DataDeNascimento: `Datetime`
- Email: `string`
- Telefone: `string`
- Formacao: `Enum (EnsinoMedio, EnsinoTecnico, Graduado, PosGraduado, Mestrado, Douturado)`
- DataContratacao: `Datetime`
- Ativo: `bool`
- Todos os atributos são obrigatórios no momento de criação da entidade.

## Modelo (Curso)
- Identificador: `long`
- Nome: `string`
- Descricao: `string`
- DataCriacao: `Datetime`
- Categoria: `Enum (Básico, Médio, Avançado)`
- Valor: `decimal`
- CargaHoraria: `int`
- ProfessorId: `Datetime`
- Ativo: `bool`
- Todos os atributos são obrigatórios no momento de criação da entidade, exceto ProfessorId.

## Modelo (Aluno)
- Identificador: `long`
- Nome: `string`
- Sobrenome: `string`
- DataDeNascimento: `Datetime`
- Email: `string`
- Telefone: `string`
- DataMatricula: `Datetime`
- Ativo: `bool`
- Todos os atributos são obrigatórios no momento de criação da entidade.

## Requisitos
### Professor
1. `POST /professor`
- Deve validar o e-mail.

1. `GET /professor`
- Deve listar apenas id, nome e ativo.

2. `GET /professor?nome={nome}`
- Deve listar apenas id e nome. Filtrar pelo nome usando o `like` no banco de dados tanto pela coluna "nome", quanto a coluna "sobrenome" e não usar diferenciar letras minusculas e maiusculas. Exemplo: Se buscar por "gui", deve listar "Guilherme".

3. `GET /professor/{id}`
- Deve listar todas as propriedades do professor.

4. `PUT /professor/{id}`
- Deve poder editar email, telefone, ativo e formacao.

### Curso
1. `GET /curso`
- Deve listar apenas id e nome, descricao, ativo e categoria.

2. `GET /curso?nome={nome}&categoria={categoria}&valorMinimo={valor}`
- Deve listar apenas id e nome, descricao e categoria. Filtrar pelo nome usando o `like` no banco de dados e não usar diferenciar letras minusculas e maiusculas. Filtrar pela categoria e valor. Exemplo: Se buscar por "info", deve listar "Técnico em Informática".

3. `GET /curso/{id}`
- Deve listar todas as propriedades do curso.

4. `PUT /curso/{id}`
- Deve poder editar descricao, categoria, valor, cargaHoraria, ativo e professorId.

5. `PUT /curso/{id}/adicionar-professor/{professorId}`
- Somente um professor ativo pode ser adicionado ao curso.
- Somente um curso ativo pode ter um professor adicionado.

6. `PUT /curso/{id}/adicionar-aluno/{alunoId}`
- Somente um aluno ativo pode ser adicionado ao curso.
- Somente um curso ativo pode ter um aluno adicionado.

### Aluno
1. `POST /aluno`
- Deve validar o e-mail.

2. `GET /aluno`
- Deve listar apenas id, nome e ativo.

3. `GET /aluno?nome={nome}`
- Deve listar apenas id e nome. Filtrar pelo nome usando o `like` no banco de dados tanto pela coluna "nome", quanto a coluna "sobrenome" e não usar diferenciar letras minusculas e maiusculas. Exemplo: Se buscar por "gui", deve listar "Guilherme".

4. `GET /aluno/{id}`
- Deve listar todas as propriedades do aluno.

5. `PUT /aluno/{id}`
- Deve poder editar email, telefone, ativo.

### Geral
- Endpoints que recebem o id da entidade, devem retornar um erro tratado caso não encontrem a entidade no banco.
- Endpoints com regras de negócio, como verificações como se a entidade está ativa no banco, devem retornar um erro tratado.
- Deve existir validações para campos obrigatórios recebidos nas requests e devem retornar um erro tratado caso não passe a verificação.
- Todos os endpoints são privados e devem exigir autenticação.

## Front end
### Geral
- Deve existir uma tela de login para o usuário acessar o sistema. As demais páginas devem ser privadas e acessadas somente se o usuário estiver logado.
- Deve existir uma tela inicial com um menu para guiar pelo sistema, para as páginas dos professores, cursos e alunos.

### Professor
- Deve existir uma tela que lista todos os professores, e um input para filtrar pelo nome.
- Deve existir uma tela para cadastrar um novo professor.
- Deve existir uma tela para detalhar algum professor. Nessa mesma tela deve existir um botão para deletar o professor. Nessa mesma tela, deve ser possível vincular um professor à algum curso.
- Deve existir uma tela para editar algum professor.

### Curso
- Deve existir uma tela que lista todos os professores, e inputs para filtrar pelo nome, categoria, e valor.
- Deve existir uma tela para cadastrar um novo curso.
- Deve existir uma tela para detalhar algum curso. Nessa mesma tela deve existir um botão para deletar o curso.
- Deve existir uma tela para editar algum curso.

### Aluno
- Deve existir uma tela que lista todos os alunos, e um input para filtrar pelo nome.
- Deve existir uma tela para cadastrar um novo aluno.
- Deve existir uma tela para detalhar algum aluno. Nessa mesma tela deve existir um botão para deletar o aluno. Nessa mesma tela, deve ser possível vincular um aluno à algum curso.
- Deve existir uma tela para editar algum aluno.