DOCUMENTO DE REQUISITOS
Painel Digital Escolar

Projeto: Painel Digital Escolar
Disciplina: Desenvolvimento de Sistemas
Tecnologias previstas: HTML, CSS, JavaScript, Git e GitHub
Versão: 1.0

1. Introdução
1.1 Objetivo do documento

Este documento apresenta os requisitos do sistema Painel Digital Escolar, definindo suas funcionalidades, regras de negócio, requisitos funcionais e não funcionais.

O documento tem como objetivo orientar o desenvolvimento do sistema e estabelecer de forma clara o que a plataforma deverá oferecer aos seus usuários.

1.2 Objetivo do sistema

O Painel Digital Escolar tem como objetivo centralizar informações acadêmicas e escolares em uma plataforma digital, permitindo que alunos, professores e representantes de turma acompanhem horários, atividades, eventos, avisos e informações relacionadas ao desempenho das turmas.

A plataforma deverá proporcionar uma maneira simples, organizada e acessível de consultar e atualizar informações da rotina escolar.

2. Escopo do Sistema

O sistema deverá funcionar como um painel digital interativo para organização da rotina escolar.

O sistema deverá permitir:

Visualizar horários de aulas;

Consultar matérias e professores;

Registrar tarefas e trabalhos;

Publicar avisos importantes;

Informar eventos escolares;

Registrar alterações relacionadas às aulas;

Permitir colaboração entre professores e representantes;

Acompanhar o desempenho acadêmico das turmas;

Apresentar gráficos e indicadores de desempenho;

Centralizar informações importantes para cada turma.

3. Usuários do Sistema

O sistema terá diferentes tipos de usuários.

3.1 Professor

O professor será responsável por administrar informações relacionadas às suas aulas e turmas.

Principais permissões:

Consultar horários;

Adicionar tarefas;

Adicionar trabalhos;

Registrar avisos;

Informar avaliações;

Atualizar informações das aulas;

Informar eventos;

Consultar o desempenho das turmas.

3.2 Representante de Turma

O representante será um aluno escolhido pela própria turma para auxiliar na atualização das informações do painel.

Principais permissões:

Consultar informações da turma;

Adicionar informações importantes do dia;

Registrar comunicados destinados à turma;

Consultar atividades e eventos;

Visualizar informações de desempenho disponibilizadas pelo sistema.

3.3 Aluno

O aluno terá acesso às informações disponibilizadas para sua turma.

Principais permissões:

Visualizar horários;

Consultar professores e matérias;

Consultar tarefas;

Consultar trabalhos;

Visualizar avaliações;

Consultar eventos;

Visualizar avisos;

Acompanhar informações de desempenho disponibilizadas para a turma.

3.4 Administrador

O administrador será responsável pelo gerenciamento geral da plataforma.

Principais permissões:

Cadastrar usuários;

Editar usuários;

Remover usuários;

Cadastrar turmas;

Cadastrar matérias;

Cadastrar professores;

Configurar horários;

Gerenciar permissões;

Gerenciar informações do sistema;

Consultar relatórios.

4. Requisitos Funcionais

Os requisitos funcionais descrevem as funcionalidades que o sistema deverá disponibilizar.

RF01 — Cadastro de usuários

O sistema deverá permitir o cadastro de usuários, incluindo alunos, professores, representantes e administradores.

RF02 — Login

O sistema deverá permitir que os usuários realizem login utilizando suas credenciais.

RF03 — Controle de acesso

O sistema deverá controlar o acesso às funcionalidades de acordo com o tipo de usuário.

RF04 — Cadastro de turmas

O sistema deverá permitir o cadastro e gerenciamento das turmas escolares.

RF05 — Cadastro de disciplinas

O sistema deverá permitir cadastrar as disciplinas oferecidas pela escola.

RF06 — Cadastro de professores

O sistema deverá permitir cadastrar professores e associá-los às respectivas disciplinas e turmas.

RF07 — Cadastro de horários

O sistema deverá permitir cadastrar os horários das aulas de cada turma.

RF08 — Visualização do cronograma

O sistema deverá apresentar o cronograma de aulas organizado por dia, horário, disciplina, turma e professor.

RF09 — Registro de tarefas

O sistema deverá permitir que professores registrem tarefas destinadas às suas turmas.

Cada tarefa poderá conter:

Título;

Descrição;

Disciplina;

Data de publicação;

Prazo de entrega;

Turma responsável.

RF10 — Registro de trabalhos

O sistema deverá permitir o cadastro de trabalhos escolares.

O trabalho poderá conter:

Título;

Descrição;

Disciplina;

Data de entrega;

Turma;

Professor responsável.

RF11 — Registro de avaliações

O sistema deverá permitir o cadastro de informações sobre avaliações, incluindo data, disciplina e turma.

RF12 — Avisos escolares

O sistema deverá permitir a publicação de avisos importantes destinados a uma ou mais turmas.

RF13 — Eventos escolares

O sistema deverá permitir cadastrar e visualizar eventos, como:

Palestras;

Passeios;

Reuniões;

Atividades escolares;

Eventos comemorativos.

RF14 — Aviso de ausência de professores

O sistema deverá permitir registrar informações sobre a ausência de professores.

RF15 — Atualização pelo representante

O representante de turma poderá adicionar informações relevantes relacionadas ao cotidiano da turma, respeitando suas permissões.

RF16 — Edição de informações

Usuários autorizados deverão poder editar informações previamente cadastradas.

RF17 — Exclusão de informações

Usuários autorizados deverão poder excluir informações cadastradas, mediante confirmação da ação.

RF18 — Visualização de informações por turma

O sistema deverá permitir selecionar uma turma e visualizar suas informações específicas.

RF19 — Área de desempenho

O sistema deverá disponibilizar uma área específica para acompanhamento do desempenho acadêmico das turmas.

RF20 — Média geral da turma

O sistema deverá calcular e apresentar a média geral das notas de uma turma.

RF21 — Gráfico de desempenho

O sistema deverá apresentar gráficos para representar visualmente o desempenho acadêmico das turmas.

RF22 — Comparação entre turmas

O sistema deverá permitir visualizar informações de desempenho de diferentes turmas para fins de acompanhamento acadêmico.

RF23 — Acompanhamento da evolução

O sistema deverá permitir acompanhar a evolução do desempenho acadêmico ao longo dos períodos cadastrados.

RF24 — Indicadores acadêmicos

O sistema deverá apresentar indicadores relacionados ao rendimento das turmas, conforme os dados disponíveis.

RF25 — Relatórios

O sistema deverá permitir a geração e visualização de relatórios organizados por turma.

5. Requisitos Não Funcionais
RNF01 — Usabilidade

A interface deverá ser simples, intuitiva e de fácil utilização por alunos e professores.

RNF02 — Responsividade

O sistema deverá apresentar uma interface adaptável a diferentes tamanhos de tela, incluindo computadores, tablets e celulares.

RNF03 — Desempenho

As páginas e informações deverão ser carregadas em tempo adequado, evitando atrasos desnecessários durante a utilização.

RNF04 — Segurança

O sistema deverá proteger as informações dos usuários e restringir funcionalidades de acordo com suas permissões.

RNF05 — Autenticação

O sistema deverá utilizar mecanismos de autenticação para identificar os usuários.

RNF06 — Integridade dos dados

O sistema deverá evitar registros inconsistentes ou incompletos.

RNF07 — Disponibilidade

O sistema deverá estar disponível para consulta sempre que a infraestrutura utilizada estiver funcionando.

RNF08 — Compatibilidade

O sistema deverá funcionar nos principais navegadores modernos.

RNF09 — Manutenibilidade

O código deverá ser organizado de maneira que facilite futuras alterações e inclusões de funcionalidades.

RNF10 — Escalabilidade

A estrutura deverá permitir a inclusão futura de novos recursos, usuários, turmas e funcionalidades.

RNF11 — Acessibilidade

A interface deverá buscar boas práticas de acessibilidade, utilizando textos legíveis, contraste adequado e elementos de navegação claros.

RNF12 — Versionamento

O código-fonte deverá ser versionado utilizando Git e disponibilizado por meio do GitHub.

6. Regras de Negócio
RN01 — Identificação de usuários

Cada usuário deverá possuir uma identificação única no sistema.

RN02 — Permissões

Cada tipo de usuário deverá possuir permissões específicas.

RN03 — Representante de turma

Cada turma poderá possuir um representante escolhido pelos alunos.

RN04 — Atualização do painel

Somente usuários autorizados poderão adicionar, alterar ou remover informações.

RN05 — Associação de informações

Tarefas, trabalhos, avaliações e avisos deverão estar associados a pelo menos uma turma ou grupo de usuários.

RN06 — Associação de disciplinas

As aulas deverão estar vinculadas a uma disciplina e a um professor responsável.

RN07 — Desempenho

Os indicadores de desempenho deverão ser calculados utilizando os dados acadêmicos cadastrados no sistema.

RN08 — Exclusão

A exclusão de informações importantes deverá exigir confirmação do usuário autorizado.

RN09 — Dados por turma

O aluno deverá visualizar prioritariamente as informações relacionadas à sua turma.

RN10 — Histórico

Alterações importantes poderão futuramente ser armazenadas em um histórico de modificações.

7. Casos de Uso Principais
UC01 — Realizar Login

Ator: Aluno, Professor, Representante ou Administrador.

Fluxo principal:

O usuário acessa a tela de login.

Informa suas credenciais.

O sistema verifica os dados.

O sistema identifica o tipo de usuário.

O sistema apresenta o painel correspondente.

Resultado esperado: O usuário acessa as funcionalidades permitidas para seu perfil.

UC02 — Consultar Horário

Ator: Aluno, Professor ou Representante.

Fluxo principal:

O usuário acessa o cronograma.

Seleciona a turma ou acessa sua turma padrão.

O sistema apresenta os horários.

O usuário visualiza disciplinas e professores.

Resultado esperado: O usuário consegue consultar a programação das aulas.

UC03 — Cadastrar Tarefa

Ator: Professor.

Fluxo principal:

O professor acessa a área de atividades.

Seleciona a opção de adicionar tarefa.

Informa os dados da tarefa.

Seleciona a turma.

Confirma o cadastro.

O sistema registra a tarefa.

A tarefa passa a ser exibida para os alunos da turma.

UC04 — Publicar Aviso

Ator: Professor ou Representante autorizado.

Fluxo principal:

O usuário acessa a área de avisos.

Seleciona "Novo aviso".

Digita a mensagem.

Define a turma destinatária.

Publica o aviso.

O sistema disponibiliza o aviso no painel.

UC05 — Consultar Desempenho

Ator: Professor ou usuário autorizado.

Fluxo principal:

O usuário acessa a área de desempenho.

Seleciona uma turma.

O sistema consulta os dados acadêmicos.

O sistema calcula os indicadores necessários.

Os resultados são apresentados em gráficos e informações numéricas.

8. Estrutura das Informações

O painel principal deverá apresentar, preferencialmente, as seguintes áreas:

8.1 Horários

Dia;

Horário;

Disciplina;

Professor;

Turma.

8.2 Atividades

Tarefa;

Trabalho;

Avaliação;

Prazo;

Disciplina;

Professor.

8.3 Eventos

Nome do evento;

Data;

Horário;

Local;

Descrição;

Público-alvo.

8.4 Avisos

Título;

Mensagem;

Data;

Autor;

Turma destinatária.

8.5 Desempenho

Turma;

Disciplina;

Média;

Período;

Indicadores;

Evolução;

Gráficos.

9. Requisitos de Interface

A interface deverá possuir:

Menu de navegação;

Painel principal;

Área de cronograma;

Área de atividades;

Área de avisos;

Área de eventos;

Área de desempenho;

Filtros por turma e período;

Tabelas organizadas;

Gráficos;

Formulários para cadastro e edição;

Mensagens de confirmação e erro.

O design deverá priorizar clareza e facilidade de navegação.

10. Tecnologias

A primeira versão do projeto utilizará:

HTML: estrutura das páginas;

CSS: estilização e responsividade;

JavaScript: interatividade e funcionalidades;

Git: controle de versão;

GitHub: armazenamento e colaboração no código.

Futuramente, poderão ser incorporadas tecnologias para banco de dados, autenticação, APIs, backend e aplicativo mobile.

11. Futuras Funcionalidades

As seguintes funcionalidades poderão ser incorporadas em versões futuras:

Aplicativo mobile;

Notificações automáticas;

Integração com calendário escolar;

Envio de arquivos;

Entrega de atividades;

Dashboard interativo;

Relatórios automáticos;

Sistema de mensagens;

Integração com banco de dados;

Histórico de alterações;

Recuperação de senha;

Controle avançado de permissões.

12. Critérios Gerais de Aceitação

O sistema será considerado funcional quando:

Os usuários conseguirem acessar o sistema conforme suas permissões;

As turmas puderem ser cadastradas e consultadas;

Os horários puderem ser cadastrados e visualizados;

Professores conseguirem registrar atividades;

Avisos puderem ser publicados e consultados;

Eventos puderem ser cadastrados;

Representantes puderem realizar as ações permitidas;

Os alunos conseguirem consultar as informações da própria turma;

Os dados de desempenho puderem ser apresentados;

Os gráficos forem exibidos corretamente;

O sistema apresentar uma interface organizada e responsiva;

O código estiver versionado utilizando Git e GitHub.

13. Restrições do Projeto

A primeira versão será desenvolvida utilizando HTML, CSS e JavaScript.

O projeto deverá manter uma estrutura organizada de arquivos.

As permissões deverão ser respeitadas conforme o tipo de usuário.

As informações acadêmicas deverão ser protegidas contra alterações não autorizadas.

O sistema deverá permitir expansão futura para tecnologias de backend e banco de dados.

14. Considerações Finais

O Painel Digital Escolar tem como finalidade centralizar informações acadêmicas e facilitar a comunicação entre alunos, professores e representantes de turma.

A definição dos requisitos apresentada neste documento servirá como base para o desenvolvimento do sistema, permitindo que a equipe tenha uma visão clara das funcionalidades, regras e características esperadas.

A estrutura também foi planejada para possibilitar futuras expansões, como aplicativo mobile, notificações, integração com calendário, envio de arquivos e relatórios avançados.

Dessa forma, o sistema poderá evoluir gradualmente de um painel escolar para uma plataforma completa de organização e acompanhamento da rotina acadêmica.
