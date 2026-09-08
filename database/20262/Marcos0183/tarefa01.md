Q1. Falando de forma genérica, um banco de dados é um conjunto de dados com um significado implícito. Porém, essa definição não aborda as seguintes características de um BD, que são:

- Um banco de dados representa uma porção do mundo real, o qual chamamos de minimundo ou Universo de Discurso. Qualquer alteração que esse minimundo sofrer deve ser refletida no banco de dados.

- Um banco de dados é um conjunto lógico e ordenado de dados que possuem algum significado, e não uma coleção aleatória sem um fim ou objetivo específico.

- Um banco de dados é construído e povoado com dados que têm um determinado objetivo, com usuários e aplicações desenvolvidas para manipulá-los.

Exemplos de SGBDs: Access, Interbase, MySQL, Oracle.



Q2. 

- Ausência de controle de acesso concorrente de vários usuários;

- Impossibilidade de se executar mais de um processo ao mesmo tempo num arquivo de dados;

- A definição da estrutura do arquivo armazenada no próprio código do aplicativo, o que significa que os programas controlavam as tarefas de gravação e leitura dos dados no arquivo. Isso ocosionava uma dependência entre os bancos de dados e a aplicação, tornando muito complexo o processo de manutenção de todo o sistema.

- Inconsistência, redundância, dificuldade de acesso e isolamento de dados;

- Problemas relativos à segurança dos dados;

- Duplicidade de informações entre vários arquivos;

- Aplicação dependente dos dados;

- Imcapatibilidade dos formatos dos dados.



Q3.

- *Atomicidade*: É a garantia de que a transação será feita totalmente ou não será feita. Nesse caso, a transação não é feita "pela metadade".

Exemplo: Um cliente de um banco transferindo parte de seu saldo para outra conta do mesmo banco. Em caso dessa propriedade não ser garantida, a tranferencia poderia resultar na subtração do saldo da conta de origem, sem adicionar o valor transferido para a conta de destino.

- *Consistência*: Proteção da integridade dos dados, ou seja, é o cuidado para que processos não válidos, não possam passar pelo sistema.

Exemplo: Um cliente deseja sacar dinheiro da sua conta no banco. A ausência dessa propriedade pode causar saques maiores do que o saldo do cliente.

- *Isolamento*: Fato de uma transação não "atrapalhar" a outra e ocorrer de forma isolada, garantido que sejam feitas de forma individual. Isso não significa que não podem ocorrer mais de uma transação simulteneamente, mas que transações que ocorrem ao mesmo tempo, não podem impactar nas outras.

Exemplo: Vários clientes realizando saques simultaneamente em uma mesma conta. Para que não ocorra de um desses clientes sacar em caso...

- *Durabilidade*: Preservação dos dados após as operações terem sido realizadas. Uma vez que uma transação for efetuada, ela permanecerá dessa forma, mesmo que ocorram problemas no sistema, sem precisar de retrabalho.

Exemplo: Um cliente do banco decide realizar uma transferência da sua conta para outra, no meio da transferência, o sistema do banco fica inativo. Em caso da durabilidade não ser aplicada, os dados dessa transferência serão perdidos totalmente ou parcialmente, e o cliente terá que refazer o mesmo processo.



Q4.

a - Atomicidade: Como a situação traz a ideia de que houve um processo realizado parcialmente, dados atualizados na conta de origem e não atualizados na conta de destino da transferência, nesse caso, há a quebra da garantia de atomicidade, pois, a operação ou deveria ter creditado na conta destino, completando o processo, ou não ter debitado na conta de origem, cancelando o processo.

b - Isolamente: Se o exemplo fala de operações sendo realizadas simultaneamente, então o cuidado para que esses dois processos não influência um ao outro de maneira negativa, cabe a propriedade de isolamento garanta isso.

c - Durabilidade: Dado as perdas de informações de um processo causadas após o servidor ser reiniciado, o sistema não garantiu a durabilidade desses dados, mesmo em situações inesperadas no sistema, nesse caso, ele ter sido reiniciado.

d - Consistência: O sistema não permitiu uma transferência que passasse o limite do saldo da conta, ou seja, garantindo a integridade dos dados, aplicando o pilar de consistência, pois não permitiu a realização de operações inválidas.



Q5.

- *Recuperação*: Mecanismo responsável por garantir que o banco de dados retorne a um estado consistente e correto após a ocorrência de falhas(como quedas de energia, erros de software, falhas de hardware ou interrupções de rede). O SGBD trabalha em etapas usando arquivos(logs) que registram as modificações de dados, e antes que as informações sejam de fato gravadas no disco principal, o log deve passar pelas etapas de verificação, assim evitando perdas de dados em caso de problemas inesperados no sistema.

- *Integridade*: Refere-se à exatidão, consistência e confiabilidade dos dados armazenados, protegendo os dados contra erros de inserção, modificação ou exclusão incorreta por parte parte de usuários ou aplicações. O papel do SGBD é aplicar automaticamente as restrições definidas na DDL(PK, FK, UNIQUE, CHECK).

- *Redudância*: A redundância acontece quando um mesmo dado é armazenado em mais de um local dentro do banco de dados. Portanto, o SGBD deve ser capaz de controlar essas redundâncias, impedindo o que esses dados duplicados se espalhem pelo banco de dados de forma descontrolada, já que também é de responsabilidade do SGBD  gerenciar as redundâncias intencionais. Esse processo é feit com técnicas específicas de arquitetura e lógica interna para gerenciar dados duplicados sem comprometer a integridade.

- *Inconsistência*: Quando duas ou mais informações dentro do banco de dados entram em contradição direta, representando estados diferentes para uma mesma realidade. O SGBD possui formas de tratar esse problema como a rejeição automatica de comandos da própria linguagem do banco de dados que gerariam inconsistências, arquivos de logs que desfazem alterações de processos no caso de serem mal sucedidos ou o protocolo Two-Phase Commmit, que antes de salvar um dado, verifica se todos os bancos estão prontos para essa operação.



Q6.

a - Entidades Principais e b - Atributos
Cliente: ID_Cliente (identificador único), Nome_Empresa, CNPJ, Email_Contato, Telefone, Data_Inicio_Contrato.

Squad: ID_Squad, Nome_Squad, Data_Criacao, Especialidade_Principal.

Membro: ID_Membro, Nome, CPF, Email_Corporativo, Cargo (Desenvolvedor, Testador, Líder Técnico, Supervisor, Gerente de Produto), ID_Squad (Squad à qual pertence).

Projeto: ID_Projeto, Nome_Projeto, Descricao, Data_Inicio, Data_Previsao_Fim, Status, ID_Cliente (Cliente proprietário), ID_Squad (Squad responsável).

Sprint (Iteração): ID_Sprint, Numero_Sprint, Data_Inicio, Data_Fim, Objetivo, ID_Projeto.

Tarefa (Issue): ID_Tarefa, Titulo, Descricao, Tipo, Prioridade, Status (A Fazer, Em Andamento, Em Teste, Concluído), Pontos_Estimativa, ID_Projeto (Projeto pai), ID_Sprint (Sprint alocada - opcional), ID_Membro_Atribuido (Responsável), ID_Release (Release inclusa - opcional).

Release: ID_Release, Versao (v1.0.0), Data_Lancamento, Descricao_Alteracoes, ID_Projeto (Projeto correspondente).

c - Relacionamentos e Cardinalidades
Cliente e Projeto: 1 : N (Um Cliente pode ter vários Projetos, mas cada Projeto pertence a apenas um Cliente).

Squad e Projeto: 1 : N (Uma Squad pode ser responsável por múltiplos Projetos, mas cada Projeto é atribuído a apenas uma Squad principal).

Squad e Membro: 1 : N (Uma Squad possui múltiplos Membros, mas cada Membro pertence a apenas uma Squad por vez).

Projeto e Sprint: 1 : N (Um Projeto é composto por várias Sprints, mas uma Sprint pertence a um único Projeto).

Projeto e Release: 1 : N (Um Projeto pode ter várias Releases lançadas, mas uma Release pertence a apenas um Projeto).

Projeto e Tarefa: 1 : N (Um Projeto contém várias Tarefas, e toda Tarefa obrigatoriamente pertence a um Projeto).

Sprint e Tarefa: 0..1 : N (Uma Sprint agrupa várias Tarefas; uma Tarefa pode ou não estar alocada em uma Sprint em um dado momento).

Membro e Tarefa: 0..1 : N (Um Membro pode estar atribuído a várias Tarefas, mas cada Tarefa pode ter no máximo um Membro responsável atribuído por vez).

Release e Tarefa: 0..1 : N (Uma Release pode empacotar várias Tarefas concluídas; uma Tarefa pode ou não estar associada a uma Release específica).

d - Regras de Integridade (Restrições)
Integridade de Liderança (Líder Técnico por Squad): Cada Squad deve ter exatamente um Membro associado cujo cargo seja "Líder Técnico".

Obrigatoriedade de Projeto para Tarefa: Nenhuma Tarefa pode existir no banco de dados sem estar vinculada a um Projeto válido.

Restrição Temporal de Sprints: A Data_Fim de uma Sprint deve ser estritamente posterior à sua Data_Inicio.

Coerência de Alocação de Tarefas: Uma Tarefa só pode ser atribuída a um Membro que pertença à mesma Squad responsável pelo Projeto daquela tarefa.

Apenas Tarefas Concluídas em Releases: Uma Tarefa só pode ser vinculada a uma Release se o seu Status for "Concluído".

Unicidade de Identificação do Cliente: O CNPJ de um Cliente e o Email_Corporativo e CPF de um Membro devem ser únicos no sistema.

Consistência do Escopo da Sprint: Uma Tarefa só pode ser vinculada a uma Sprint se essa Sprint pertencer ao mesmo Projeto da Tarefa.