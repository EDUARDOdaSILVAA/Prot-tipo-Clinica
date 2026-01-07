========================================================================
             UNIVERSIDADE TECNOLÓGICA FEDERAL DO PARANÁ
               BACHARELADO EM CIÊNCIA DA COMPUTAÇÃO
             DISCIPLINA: ANÁLISE E PROJETO DE SOFTWARE
========================================================================

PROJETO: Sistema Iluminar
VERSÃO: 1.0 (Protótipo Interativo)

AUTORES:
- Eduardo da Silva
- Izabelly Bartolini Farias
- José Vinicius Grecco
- Juliana Carvalho

========================================================================
1. DESCRIÇÃO DO PROJETO
========================================================================
O Sistema Iluminar foi desenvolvido para apoiar a gestão administrativa e 
terapêutica do Instituto Iluminar. Este software implementa os principais 
requisitos funcionais descritos na documentação do projeto, permitindo:

1. Gestão de Pacientes (Cadastro, Listagem e Exclusão).
2. Gestão de Funcionários (Cadastro e Listagem).
3. Agendamento de Sessões Terapêuticas (com verificação de disponibilidade).
4. Realização de Atendimento (Registro de atividades e evolução).
5. Persistência de dados em memória (Listas voláteis) durante a execução.

O sistema utiliza uma interface via linha de comando (CLI) para interagir
com o usuário, simulando o fluxo real de operação de uma clínica.

========================================================================
2. ESTRUTURA DE ARQUIVOS
========================================================================
O código fonte segue o padrão MVC (Model-View-Controller) com DAOs:

/IluminarProject
  |-- src/
      |-- Controle/   (Lógica de Negócio: SessaoManager.java, SalaManager.java)
      |-- DAOs/          (Acesso a Dados: DAOManager.java, PacienteDAO.java, etc.)
      |-- Entidades/        (Entidades: Paciente.java, Funcionario.java, etc.)
      |-- Main/         (Interface: MainCLI.java)
  |-- README.TXT

========================================================================
3. PRÉ-REQUISITOS
========================================================================
- Java Development Kit (JDK) 8 ou superior instalado.
- Terminal ou Prompt de Comando acessível.

========================================================================
4. INSTRUÇÕES DE COMPILAÇÃO
========================================================================
Não é necessário utilizar IDEs complexas. Para compilar via terminal:

1. Abra o terminal na pasta raiz do projeto (/IluminarProject).

2. (Opcional) Crie a pasta para os binários:
   Linux/Mac: mkdir bin
   Windows:   md bin

3. Compile o código executando o comando abaixo:
   
   javac -d bin -sourcepath src src/view/MainCLI.java

   * Se não houver mensagens de erro, a compilação foi bem-sucedida.

========================================================================
5. INSTRUÇÕES DE EXECUÇÃO
========================================================================
Para iniciar o sistema, execute o comando abaixo na raiz do projeto:

   java -cp bin view.MainCLI

--- COMO USAR ---
O sistema abrirá um menu interativo numérico:

[1] Gerenciar Pacientes: Cadastre novos pacientes informando CPF, Nome, 
    Idade e Escola.
[2] Gerenciar Funcionários: Cadastre terapeutas informando CPF, Nome, 
    Cargo e Salário.
[3] Agendar Sessão: Requer um Paciente e um Funcionário previamente 
    cadastrados. O sistema validará a disponibilidade da Sala.
[4] Realizar Sessão: Digite o ID da sessão gerada no passo anterior 
    para registrar atividades e notas de desempenho.

NOTA: Como o banco de dados é simulado em memória, todos os dados são
perdidos ao encerrar o programa (Opção 0).

========================================================================
6. PADRÕES DE PROJETO (DESIGN PATTERNS)
========================================================================
O desenvolvimento seguiu rigorosamente o Diagrama de Classes (DCP):

- SINGLETON: Utilizado nas classes DAO (Ex: PacienteDAO.getInstance()) 
  para garantir uma única instância de armazenamento de dados.
- DAO (Data Access Object): Separação completa entre a lógica de negócio
  e a camada de acesso aos dados.
- CONTROLLER/MANAGER: As classes 'SessaoManager' e 'SalaManager' 
  implementam as regras de negócio e validações descritas nos 
  Contratos de Operações.

========================================================================
Casos de uso -- CO
- iniciarAgendamento (MainCLI - Fluxo de preparação) 
- verificarDisponibilidadeSalas (SalaManager) 
- listaSalasDisponiveis (SalaManager) 
- marcarSessao (SessaoManager) 
- iniciarSessao (SessaoManager) 
- registrarAtividade (SessaoManager) 
- finalizarSessao (SessaoManager) 
- solicitarGerarRelatorio (RelatorioManager) 
- exibirPrevisualizacao (RelatorioManager - retorno formatado)
