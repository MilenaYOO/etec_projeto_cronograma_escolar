Informações do Projeto

Nome do Projeto:
Painel Digital Escolar (etec_projeto_cronograma_escolar)

Equipe:

Integrante 1: Milena Bispo (RA: _________)
Integrante 2: Talita Gonçalves (RA: _________)
Integrante 3: Ebert Torquato (RA: _________)

Descrição do Projeto:
O Painel Digital Escolar é uma aplicação web que centraliza o cronograma de aulas por turma, as tarefas e trabalhos, os avisos e eventos escolares e o acompanhamento do desempenho acadêmico (notas, médias e comparação entre turmas). O painel é colaborativo: professores e um representante por turma, escolhido pelos alunos, podem registrar informações do dia. Todos os dados ficam em um banco relacional centralizado, que garante consistência e permite gerar relatórios e gráficos.

1. JUSTIFICATIVA DA ARQUITETURA RELACIONAL
Tecnologia Selecionada

Sistema Gerenciador de Banco de Dados Relacional: PostgreSQL

Razão Principal para Escolha Relacional

Os dados do projeto são fortemente estruturados e interligados: turmas possuem alunos, horários ligam turma, disciplina e professor, e atividades, avisos e notas sempre pertencem a uma turma e a uma disciplina. Essa estrutura é fixa durante o ano letivo e se encaixa naturalmente em tabelas com chaves primárias e estrangeiras. A integridade referencial garante, por exemplo, que nenhuma nota exista sem aluno e avaliação válidos, e que não existam dois professores marcados na mesma aula e horário. As propriedades ACID evitam que edições simultâneas de professores e representantes corrompam o painel. Além disso, os recursos de agregação do SQL (AVG, GROUP BY, window functions) atendem diretamente aos requisitos de média geral, comparação entre turmas e evolução do desempenho.

2. MODELO DE DADOS RELACIONAL
Levantamento de Entidades
Entidade	Atributos Principais	Tipo de Dados	Restrições
Turma	ID_Turma (PK), Nome, Ano_Letivo, Turno, Sala	SERIAL, VARCHAR, INT, VARCHAR, VARCHAR	NOT NULL, UNIQUE(Nome, Ano_Letivo)
Aluno	ID_Aluno (PK), ID_Turma (FK), Matrícula, Nome, Email	SERIAL, INT, VARCHAR, VARCHAR, VARCHAR	NOT NULL, UNIQUE(Matrícula)
Professor	ID_Professor (PK), Nome, Email	SERIAL, VARCHAR, VARCHAR	NOT NULL, UNIQUE(Email)
Disciplina	ID_Disciplina (PK), Nome, Código	SERIAL, VARCHAR, VARCHAR	NOT NULL, UNIQUE(Código)
Horario_Aula	ID_Horario (PK), ID_Turma (FK), ID_Disciplina (FK), ID_Professor (FK), Dia_Semana, Hora_Inicio, Hora_Fim	SERIAL, INT, INT, INT, SMALLINT, TIME, TIME	NOT NULL, CHECK(Dia_Semana 1–7), UNIQUE(Turma, Dia, Hora_Inicio)
Representante_Turma	ID_Turma (PK, FK), ID_Aluno (FK), Data_Eleicao	INT, INT, DATE	UNIQUE: 1 representante por turma
Usuario	ID_Usuario (PK), Email, Senha_Hash, Perfil, ID_Aluno (FK), ID_Professor (FK)	SERIAL, VARCHAR, VARCHAR, VARCHAR, INT, INT	NOT NULL, UNIQUE(Email), CHECK(Perfil)
Atividade	ID_Atividade (PK), ID_Turma (FK), ID_Disciplina (FK), ID_Usuario (FK), Tipo, Titulo, Descricao, Data_Entrega	SERIAL, INT, INT, INT, VARCHAR, VARCHAR, TEXT, DATE	NOT NULL, CHECK(Tipo: TAREFA/TRABALHO/AVALIACAO)
Aviso	ID_Aviso (PK), ID_Turma (FK, nulo = geral), ID_Usuario (FK), Categoria, Titulo, Mensagem, Data_Publicacao	SERIAL, INT, INT, VARCHAR, VARCHAR, TEXT, TIMESTAMP	NOT NULL, CHECK(Categoria: FALTA_PROFESSOR/COMUNICADO/OUTRO)
Evento	ID_Evento (PK), ID_Turma (FK, nulo = toda a escola), ID_Usuario (FK), Tipo, Titulo, Data_Evento, Local	SERIAL, INT, INT, VARCHAR, VARCHAR, DATE, VARCHAR	NOT NULL, CHECK(Tipo: PALESTRA/PASSEIO/OUTRO)
Avaliacao	ID_Avaliacao (PK), ID_Turma (FK), ID_Disciplina (FK), Titulo, Bimestre, Data_Aplicacao	SERIAL, INT, INT, VARCHAR, SMALLINT, DATE	NOT NULL, CHECK(Bimestre 1–4)
Nota	ID_Nota (PK), ID_Avaliacao (FK), ID_Aluno (FK), Valor	SERIAL, INT, INT, NUMERIC(4,2)	NOT NULL, CHECK(Valor 0–10), UNIQUE(Avaliação, Aluno)
Diagrama Entidade-Relacionamento (DER)

O modelo possui os seguintes relacionamentos:

Turma 1:N Aluno: cada aluno pertence a uma turma; uma turma tem vários alunos.
Turma 1:1 Representante_Turma N:1 Aluno: cada turma tem no máximo um representante, que é um aluno da própria turma.
Turma, Disciplina e Professor se relacionam em Horario_Aula, que resolve a relação N:N ternária (uma turma tem várias disciplinas, um professor leciona em várias turmas).
Turma 1:N Atividade, Aviso e Evento: o conteúdo do painel é sempre vinculado a uma turma (ou geral, quando ID_Turma é nulo em Aviso e Evento).
Usuario 1:N Atividade, Aviso, Evento: registra quem publicou cada informação (professor ou representante).
Avaliacao 1:N Nota N:1 Aluno: base para médias, gráficos e comparação entre turmas.
                     PROFESSOR (1)
                          |
                          N
 DISCIPLINA (1) ---N--- HORARIO_AULA ---N--- (1) TURMA (1) ---- (1) REPRESENTANTE_TURMA
                                                 |  |  |                 |
                          +----------------------+  |  +-------+         N
                          |                         |          |         |
                          N                         N          N     ALUNO (1)
                   ATIVIDADE / AVISO / EVENTO    AVALIACAO   ALUNO <-----+
                          |                         |          |
                          N                         N          N
                       USUARIO                    NOTA  <-----+
3. CARACTERÍSTICAS DA ARQUITETURA RELACIONAL
Propriedades ACID Aplicadas ao Projeto
Propriedade ACID	Garantia Técnica	Aplicação no Projeto
Atomicidade	Transação completa ou não executa	O lançamento de notas de uma avaliação para toda a turma é gravado por inteiro ou nada é gravado
Consistência	Dados mantêm regras de integridade	Atividades, avisos e notas sempre vinculados a turma, disciplina e aluno válidos; nota sempre entre 0 e 10
Isolamento	Transações concorrentes não se interferem	Vários professores e o representante editando o painel ao mesmo tempo não geram conflito
Durabilidade	Dados persistem após commit	Cronograma, notas e histórico de avisos permanecem após falha ou reinício do servidor
4. NORMALIZAÇÃO E ESTRUTURA DE DADOS
Nível de Normalização Aplicado

Forma Normal: 3NF

Justificativa:

O modelo está na 3ª Forma Normal. Não há atributos multivalorados nem grupos repetitivos (1NF): os horários de uma turma ficam em linhas de Horario_Aula, e não em colunas como "segunda", "terça" etc. Todos os atributos não-chave dependem da chave primária completa (2NF). Não há dependências transitivas (3NF): o nome do professor e o nome da disciplina ficam em suas próprias tabelas e não são repetidos em horários ou atividades. A média das turmas não é armazenada, e sim calculada por consultas e views a partir de Nota, evitando redundância e valores desatualizados.

Integridade Referencial

Todas as tabelas dependentes possuem chaves estrangeiras. O banco impede excluir uma turma, disciplina ou professor enquanto houver horários, atividades ou notas vinculados (ON DELETE RESTRICT). Já os dados puramente dependentes, como as notas de uma avaliação, são removidos em cascata quando a avaliação é excluída (ON DELETE CASCADE). A regra "uma turma só tem um representante" é garantida pela chave primária de Representante_Turma, e a de que "o professor não pode estar em duas turmas no mesmo horário" por uma restrição UNIQUE ou EXCLUDE. Essas regras valem em nível de banco, independentemente da aplicação.

5. JUSTIFICATIVA TÉCNICA: POR QUE NÃO ALTERNATIVAS
Por que não NoSQL para este projeto?

NoSQL é indicado para dados semi-estruturados e de crescimento imprevisível. Aqui os dados são estruturados e muito relacionados: o desempenho das turmas exige junções entre Nota, Avaliacao, Aluno, Disciplina e Turma, e cálculos de média e comparação, tarefas em que o SQL é mais simples e eficiente. Bancos NoSQL tendem a duplicar dados e oferecer consistência eventual, o que arriscaria exibir notas ou horários divergentes. Para o escopo do projeto, NoSQL acrescentaria complexidade sem benefício.

Por que não arquitetura em camadas com múltiplos bancos?

O objetivo da disciplina é aprender modelagem, normalização, SQL, integridade referencial e procedures. Um único banco PostgreSQL bem projetado permite focar nesses conceitos sem gastar tempo orquestrando várias infraestruturas. Para o volume de uma escola (centenas de alunos), um banco só atende com folga.

6. MODELAGEM SQL
Scripts de Criação
sql
CREATE TABLE turma (
    id_turma     SERIAL PRIMARY KEY,
    nome         VARCHAR(50) NOT NULL,
    ano_letivo   INT NOT NULL,
    turno        VARCHAR(20) NOT NULL,
    sala         VARCHAR(10),
    UNIQUE (nome, ano_letivo)
);

CREATE TABLE aluno (
    id_aluno   SERIAL PRIMARY KEY,
    id_turma   INT NOT NULL REFERENCES turma(id_turma) ON DELETE RESTRICT,
    matricula  VARCHAR(20) UNIQUE NOT NULL,
    nome       VARCHAR(100) NOT NULL,
    email      VARCHAR(100)
);

CREATE TABLE professor (
    id_professor SERIAL PRIMARY KEY,
    nome         VARCHAR(100) NOT NULL,
    email        VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE disciplina (
    id_disciplina SERIAL PRIMARY KEY,
    nome          VARCHAR(80) NOT NULL,
    codigo        VARCHAR(20) UNIQUE NOT NULL
);

CREATE TABLE horario_aula (
    id_horario    SERIAL PRIMARY KEY,
    id_turma      INT NOT NULL REFERENCES turma(id_turma) ON DELETE RESTRICT,
    id_disciplina INT NOT NULL REFERENCES disciplina(id_disciplina) ON DELETE RESTRICT,
    id_professor  INT NOT NULL REFERENCES professor(id_professor) ON DELETE RESTRICT,
    dia_semana    SMALLINT NOT NULL CHECK (dia_semana BETWEEN 1 AND 7),
    hora_inicio   TIME NOT NULL,
    hora_fim      TIME NOT NULL CHECK (hora_fim > hora_inicio),
    UNIQUE (id_turma, dia_semana, hora_inicio),
    UNIQUE (id_professor, dia_semana, hora_inicio)
);

CREATE TABLE representante_turma (
    id_turma     INT PRIMARY KEY REFERENCES turma(id_turma) ON DELETE CASCADE,
    id_aluno     INT NOT NULL REFERENCES aluno(id_aluno) ON DELETE RESTRICT,
    data_eleicao DATE NOT NULL DEFAULT CURRENT_DATE
);

CREATE TABLE usuario (
    id_usuario   SERIAL PRIMARY KEY,
    email        VARCHAR(100) UNIQUE NOT NULL,
    senha_hash   VARCHAR(255) NOT NULL,
    perfil       VARCHAR(20) NOT NULL CHECK (perfil IN ('PROFESSOR','REPRESENTANTE','ALUNO')),
    id_aluno     INT REFERENCES aluno(id_aluno),
    id_professor INT REFERENCES professor(id_professor)
);

CREATE TABLE atividade (
    id_atividade  SERIAL PRIMARY KEY,
    id_turma      INT NOT NULL REFERENCES turma(id_turma) ON DELETE RESTRICT,
    id_disciplina INT NOT NULL REFERENCES disciplina(id_disciplina) ON DELETE RESTRICT,
    id_usuario    INT NOT NULL REFERENCES usuario(id_usuario),
    tipo          VARCHAR(15) NOT NULL CHECK (tipo IN ('TAREFA','TRABALHO','AVALIACAO')),
    titulo        VARCHAR(120) NOT NULL,
    descricao     TEXT,
    data_entrega  DATE NOT NULL
);

CREATE TABLE aviso (
    id_aviso         SERIAL PRIMARY KEY,
    id_turma         INT REFERENCES turma(id_turma) ON DELETE CASCADE, -- NULL = aviso geral
    id_usuario       INT NOT NULL REFERENCES usuario(id_usuario),
    categoria        VARCHAR(20) NOT NULL CHECK (categoria IN ('FALTA_PROFESSOR','COMUNICADO','OUTRO')),
    titulo           VARCHAR(120) NOT NULL,
    mensagem         TEXT NOT NULL,
    data_publicacao  TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE evento (
    id_evento    SERIAL PRIMARY KEY,
    id_turma     INT REFERENCES turma(id_turma) ON DELETE CASCADE, -- NULL = toda a escola
    id_usuario   INT NOT NULL REFERENCES usuario(id_usuario),
    tipo         VARCHAR(15) NOT NULL CHECK (tipo IN ('PALESTRA','PASSEIO','OUTRO')),
    titulo       VARCHAR(120) NOT NULL,
    data_evento  DATE NOT NULL,
    local        VARCHAR(100)
);

CREATE TABLE avaliacao (
    id_avaliacao   SERIAL PRIMARY KEY,
    id_turma       INT NOT NULL REFERENCES turma(id_turma) ON DELETE RESTRICT,
    id_disciplina  INT NOT NULL REFERENCES disciplina(id_disciplina) ON DELETE RESTRICT,
    titulo         VARCHAR(100) NOT NULL,
    bimestre       SMALLINT NOT NULL CHECK (bimestre BETWEEN 1 AND 4),
    data_aplicacao DATE NOT NULL
);

CREATE TABLE nota (
    id_nota      SERIAL PRIMARY KEY,
    id_avaliacao INT NOT NULL REFERENCES avaliacao(id_avaliacao) ON DELETE CASCADE,
    id_aluno     INT NOT NULL REFERENCES aluno(id_aluno) ON DELETE RESTRICT,
    valor        NUMERIC(4,2) NOT NULL CHECK (valor BETWEEN 0 AND 10),
    UNIQUE (id_avaliacao, id_aluno)
);
Índices para Performance
aluno(id_turma): listar alunos de uma turma.
horario_aula(id_turma, dia_semana): montar o cronograma diário de cada turma.
atividade(id_turma, data_entrega): atividades do dia e próximos prazos.
aviso(id_turma, data_publicacao DESC): avisos mais recentes por turma.
evento(data_evento): calendário de eventos.
nota(id_aluno) e avaliacao(id_turma, bimestre): cálculo de médias e evolução por bimestre.
sql
CREATE INDEX idx_aluno_turma       ON aluno(id_turma);
CREATE INDEX idx_horario_turma_dia ON horario_aula(id_turma, dia_semana);
CREATE INDEX idx_atividade_turma   ON atividade(id_turma, data_entrega);
CREATE INDEX idx_aviso_turma_data  ON aviso(id_turma, data_publicacao DESC);
CREATE INDEX idx_evento_data       ON evento(data_evento);
CREATE INDEX idx_nota_aluno        ON nota(id_aluno);
CREATE INDEX idx_avaliacao_turma   ON avaliacao(id_turma, bimestre);
7. OPERAÇÕES PRINCIPAIS: DML e DQL
Consultas Principais (SELECT)

1. Cronograma do dia de uma turma

sql
SELECT h.hora_inicio, h.hora_fim, d.nome AS disciplina, p.nome AS professor
FROM horario_aula h
JOIN disciplina d ON d.id_disciplina = h.id_disciplina
JOIN professor p  ON p.id_professor  = h.id_professor
WHERE h.id_turma = :id_turma
  AND h.dia_semana = EXTRACT(ISODOW FROM CURRENT_DATE)
ORDER BY h.hora_inicio;

2. Atividades e avisos do dia / próximos prazos

sql
SELECT a.tipo, a.titulo, d.nome AS disciplina, a.data_entrega
FROM atividade a
JOIN disciplina d ON d.id_disciplina = a.id_disciplina
WHERE a.id_turma = :id_turma
  AND a.data_entrega >= CURRENT_DATE
ORDER BY a.data_entrega;

3. Média geral de cada turma (gráfico e comparação entre turmas)

sql
SELECT t.nome AS turma, ROUND(AVG(n.valor), 2) AS media_geral
FROM turma t
JOIN avaliacao av ON av.id_turma = t.id_turma
JOIN nota n       ON n.id_avaliacao = av.id_avaliacao
WHERE t.ano_letivo = EXTRACT(YEAR FROM CURRENT_DATE)
GROUP BY t.id_turma, t.nome
ORDER BY media_geral DESC;

4. Evolução da turma por bimestre

sql
SELECT av.bimestre, ROUND(AVG(n.valor), 2) AS media
FROM avaliacao av
JOIN nota n ON n.id_avaliacao = av.id_avaliacao
WHERE av.id_turma = :id_turma
GROUP BY av.bimestre
ORDER BY av.bimestre;

5. Média por disciplina em cada turma (identificar dificuldades)

sql
SELECT t.nome AS turma, d.nome AS disciplina, ROUND(AVG(n.valor), 2) AS media
FROM nota n
JOIN avaliacao av ON av.id_avaliacao = n.id_avaliacao
JOIN turma t      ON t.id_turma = av.id_turma
JOIN disciplina d ON d.id_disciplina = av.id_disciplina
GROUP BY t.nome, d.nome
HAVING AVG(n.valor) < 6
ORDER BY media;

6. Ranking das turmas (window function)

sql
SELECT turma, media_geral, RANK() OVER (ORDER BY media_geral DESC) AS posicao
FROM (
    SELECT t.nome AS turma, AVG(n.valor) AS media_geral
    FROM turma t
    JOIN avaliacao av ON av.id_turma = t.id_turma
    JOIN nota n       ON n.id_avaliacao = av.id_avaliacao
    GROUP BY t.id_turma, t.nome
) x;

View para o painel de desempenho

sql
CREATE VIEW vw_desempenho_turma AS
SELECT t.id_turma, t.nome AS turma, av.bimestre,
       ROUND(AVG(n.valor), 2) AS media
FROM turma t
JOIN avaliacao av ON av.id_turma = t.id_turma
JOIN nota n       ON n.id_avaliacao = av.id_avaliacao
GROUP BY t.id_turma, t.nome, av.bimestre;
Procedures e Funções
sp_registrar_atividade: insere uma atividade, validando se o usuário é professor ou representante da turma informada e se a disciplina faz parte do horário dessa turma.
sp_lancar_notas: grava, em uma única transação, as notas de uma avaliação para todos os alunos da turma (tudo ou nada).
fn_media_turma(id_turma, bimestre): retorna a média da turma, reaproveitada em relatórios e gráficos.
Trigger trg_valida_representante: impede que um aluno de outra turma seja cadastrado como representante.
sql
CREATE OR REPLACE FUNCTION fn_media_turma(p_turma INT, p_bimestre INT DEFAULT NULL)
RETURNS NUMERIC AS $$
    SELECT ROUND(AVG(n.valor), 2)
    FROM avaliacao av
    JOIN nota n ON n.id_avaliacao = av.id_avaliacao
    WHERE av.id_turma = p_turma
      AND (p_bimestre IS NULL OR av.bimestre = p_bimestre);
$$ LANGUAGE sql STABLE;

CREATE OR REPLACE FUNCTION fn_valida_representante() RETURNS TRIGGER AS $$
BEGIN
    IF (SELECT id_turma FROM aluno WHERE id_aluno = NEW.id_aluno) <> NEW.id_turma THEN
        RAISE EXCEPTION 'O representante deve ser aluno da própria turma';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_valida_representante
BEFORE INSERT OR UPDATE ON representante_turma
FOR EACH ROW EXECUTE FUNCTION fn_valida_representante();
8. BENEFÍCIOS DA ARQUITETURA RELACIONAL PARA PROJETO EDUCACIONAL
Benefício	Impacto no Projeto
Estrutura Clara e Documentada	O MER mostra como turmas, professores, horários, atividades e notas se conectam
Garantia de Integridade	Impede conflito de horários de professor, nota fora de 0–10 e conteúdo sem turma válida
Colaboração Segura	Vários professores e representantes editam o painel ao mesmo tempo com isolamento transacional
Relatórios e Gráficos Nativos	Médias, comparação entre turmas e evolução por bimestre saem direto de consultas SQL
SQL Padronizado e Aprendizado	Habilidades transferíveis para qualquer SGBD relacional
Escalabilidade Adequada	Volume de uma escola (centenas de alunos) é bem atendido por um único PostgreSQL
9. FERRAMENTAS E TECNOLOGIAS
Stack Tecnológico
Camada	Tecnologia	Justificativa
Banco de Dados	PostgreSQL	Gratuito e de código aberto, com funções de janela, views, triggers e restrições avançadas (CHECK, EXCLUDE) úteis para o cronograma e o desempenho
Backend	Quarkus (Java)	Integração com JDBC/JPA e API REST para entregar os dados ao painel
Frontend	HTML, CSS e JavaScript	Tecnologias do projeto; consome a API REST e exibe tabelas e gráficos (ex.: Chart.js)
ORM	JPA/Hibernate	Abstração de SQL; facilita manutenção
Versionamento	Git e GitHub	Controle de versão dos scripts SQL e do código
10. CRONOGRAMA DE IMPLEMENTAÇÃO
Semana	Atividade	Entregável
12-19/10	Finalizar MER; criar scripts SQL; criar índices	Scripts SQL validados + MER documento
19-26/10	Implementar procedures, funções e trigger; testes de integridade	Procedures funcionais; testes executados
26-02/11	Desenvolver views e consultas de desempenho (médias, comparação de turmas)	Queries complexas otimizadas
09-16/11	Integração completa com o painel; apresentação final	Sistema funcionando; testes de carga
11. QUESTÕES TÉCNICAS

Pergunta: Esta arquitetura é suficiente para um projeto que pode crescer no futuro?

Resposta:

"Sim. O modelo já prevê as melhorias planejadas: a tabela Usuario sustenta o login de alunos e professores; notificações automáticas podem usar uma tabela de notificações ligada a Aviso e Evento; o envio de arquivos pode guardar o arquivo em storage externo e o link no banco; e relatórios automáticos saem das views de desempenho. O PostgreSQL escala verticalmente com índices e particionamento."

Pergunta: Por que usar Banco de Dados e não apenas arquivo JSON/CSV?

Resposta:

"Arquivos JSON/CSV não oferecem integridade referencial, controle de acesso por perfil nem segurança em edições simultâneas. Como o painel é colaborativo (professores e representantes editando ao mesmo tempo), o banco evita sobrescritas e perda de dados, além de calcular médias e comparações sem carregar tudo na memória."

Pergunta: Como o controle de quem pode editar o painel é feito?

Resposta:

"Pela tabela Usuario (campo perfil) e pela tabela Representante_Turma. Professores podem editar qualquer turma; o representante só pode publicar na própria turma. Essa validação é feita na procedure sp_registrar_atividade e reforçada na camada de API."

12. CONCLUSÃO

Resumo Executivo:

"O Painel Digital Escolar adota arquitetura relacional com PostgreSQL como SGBD. A escolha é apropriada porque: (1) cronograma, turmas, professores e notas são dados estruturados e estáveis; (2) a integridade referencial é crítica para evitar conflitos de horário e notas inválidas; (3) o SQL permite gerar as médias, comparações entre turmas e indicadores de desempenho; (4) o ACID garante consistência nas edições simultâneas de professores e representantes; (5) o projeto proporciona prática real de modelagem, normalização, procedures e otimização. A implementação será realizada em 4 semanas utilizando Quarkus e JPA no backend e HTML, CSS e JavaScript no frontend."

Checklist de Entregáveis
 Modelo Entidade-Relacionamento finalizado
 Scripts SQL criados e testados
 Integridade referencial implementada
 Índices criados e otimizados
 Procedures principais documentadas
 Queries principais validadas
 Plano de backup documentado
 Integração com aplicação testada
Assinaturas

Elaborado por: Milena Bispo, Talita Gonçalves e Ebert Torquato
Data: ________________
Revisado pelo Professor: ___________________________

Referências Consultadas:

Aulas de Programação e Administração de Banco de Dados
Documentação PostgreSQL
Normalização de Dados (Codd)
ANSI SQL Standards
