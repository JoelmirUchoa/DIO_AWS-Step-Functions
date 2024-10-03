**Pré-requisitos**:  
Antes de iniciar, é necessário ter uma conta AWS ativa e as permissões suficientes, além de um entendimento básico de AWS. Familiaridade com linguagens como JSON ou YAML para definição de fluxos de trabalho também será útil.

**Situação Problema**:
 As empresas de entrega enfrentam desafios na coordenação eficiente de pedidos, rastreamento e comunicação entre clientes, entregadores e lojas. Esse processo manual frequentemente leva a erros, atrasos e falta de transparência.

**Step Functions - Página Oficial**:  
O AWS Step Functions é um serviço que facilita a coordenação de componentes distribuídos, sendo ideal para automatizar fluxos de trabalho complexos. A página oficial fornece uma visão geral, tutoriais e melhores práticas.

**Documentação Oficial**:  
A documentação da AWS Step Functions oferece informações detalhadas sobre o uso de linguagens de definição de fluxo de trabalho, integração com outros serviços AWS, exemplos práticos e APIs para gerenciar tarefas.

**Localizando o Serviço**:  
Acesse o AWS Console e faça login.
No AWS Management Console, use a barra de serviços e digite Step Functions.
Clique no serviço Step Functions para começar a criar e gerenciar fluxos de trabalho.

**Começando com um Projeto Template**:  
 Inicia na máquina de estado a AWS oferece templates prontos para Step Functions , permitindo que você crie projetos iniciais rapidamente. Esses templates cobrem diversos casos de uso, como automação de processos, pipelines de dados e orquestração de microserviços.

**Workflow Studio & ASL**:  
É uma ferramenta visual que permite criar, editar e visualizar fluxos de trabalho de maneira simples, arrastando e soltando componentes(Ações, Fluxo, Padrões). Ele facilita o design de workflows complexos, ajudando a montar o fluxo de estados e interações com outros serviços AWS de maneira visual.
ASL (Amazon States Language) é a linguagem baseada em JSON usada para definir os estados e transições dos workflows no Step Functions. Ela descreve como os estados de um fluxo de trabalho se conectam e as ações que cada estado executa.
Opções:
1.	Ações:
o	Tarefas: Realiza uma tarefa específica, como executar uma função Lambda, chamar uma API ou invocar um serviço externo.
o	Escolhas: Define condições lógicas (if/else) para decidir qual estado seguir baseado em variáveis.
o	Espera: Pausa o fluxo de trabalho por um tempo determinado.
o	Sucesso/Falha (Succeed/Fail): Define um estado como sucesso ou falha e encerra o workflow.
2.	Fluxo:
o	Sequência: Organiza as ações para que ocorram em ordem específica.
o	Mapeamento: Executa uma ação repetidamente para cada item de uma lista.
o	Paralelo: Executa múltiplas ações ao mesmo tempo e espera até que todas sejam concluídas.
3.	Padrões:
o	Orquestração sequencial: Ações são executadas em sequência, passando de um estado para o outro conforme os resultados.
o	Orquestração paralela: Várias ações são executadas simultaneamente, e o fluxo só avança quando todas são concluídas.
o	Branching (ramificação): Com a ajuda de estados de escolha, o fluxo segue por diferentes caminhos com base nas condições definidas. 
**Criando um Hello World**:  
Esse exemplo inicial é um fluxo simples de Step Functions, que executa as funçoes dos blocos que podemos atera os nomes, tipo de estado o proximo estado e o comentario desse bloco, retornando uma mensagem de sucesso. Ele demonstra os conceitos fundamentais de estados, transições e como Step Functions interage com outros serviços AWS.

**Precificação e Custos**:  
A AWS Step Functions é cobrada com base no número de transições de estado no fluxo de trabalho. O custo depende do volume de execuções e da complexidade dos fluxos. Também é importante considerar os custos dos serviços AWS integrados ao fluxo.
OBS: A dica seria excluído o serviço(Máquina de estado)depois do estudo para não ver cobrança.

**Nível 1 de Configuração - Permissão de Perfil**:  
Aqui é necessário configurar as permissões corretas para o usuário e para os serviços envolvidos. Isso geralmente envolve criar papéis (roles) no IAM para que Step Functions tenha as permissões adequadas para invocar outros serviços AWS.

**Nível 2 de Configuração - Disponibilidade de Serviço**:  
Este nível lida com a disponibilidade dos serviços integrados ao Step Functions, garantindo que os recursos estejam corretamente distribuídos e com alta disponibilidade para evitar falhas em seus fluxos.

**Criando um Assistente de Delivery na Prática**:  
Aqui, você implementa um fluxo de trabalho completo para um assistente de delivery, utilizando Step Functions para coordenar serviços como gerenciamento de pedidos.

Passos: 

1. Criar a Máquina de Estados
No console do AWS Step Functions, clique em Criar máquina de estados.
Escolha o modelo que deseja usar. Selecione Implantar e Executar.
Clique em Cancelar e depois em Editar para ajustar o workflow.

2. Configurar Permissões - Nível 1
Na tela de design, vá para Configurações.
Clique em Visualizar no IAM e adicione as permissões necessárias.
Volte para a tela de Design.

# Exemplo de comando para adicionar permissões via CLI:
aws iam attach-role-policy --role-name StepFunctionsRole --policy-arn arn:aws:iam::aws:policy/service-role/AWSStepFunctionsFullAccess

3. Selecionar os Modelos
Selecione os blocos ou estados apropriados para o workflow (Task, Pass, etc.).
Ajuste conforme necessário.

4. Configurar o Bloco de Entrada
Acesse Configurações do bloco de entrada.
Aumente o número de tokens se necessário.

{
  "Type": "Task",
  "Resource": "arn:aws:lambda:us-east-1:123456789012:function:MyFunction",
  "ResultPath": "$.content[0]",
  "Next": "NextState"
}

5. Configurar o Bloco 'Pass State'
O Pass State vai armazenar o resultado de uma etapa.
Configure a entrada como $.input_one e a saída como $.result_one.

{
  "Type": "Pass",
  "InputPath": "$.input_one",
  "ResultPath": "$.result_one",
  "Next": "FinalState"
}

6. Salvar e Executar
Após todas as configurações, clique em Salvar e depois em Executar.
Verifique os logs e os resultados no console.

Tecnologias Utilizadas
AWS Step Functions
IAM (Gerenciamento de Identidade e Acessos)
Lambda (Exemplo de integração)