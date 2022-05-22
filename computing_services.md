# **Computing services at AWS**

Amazon Elastic Compute Cloud~(EC2), provide computation capacity without you having to invest in hardware. The EC2 provides virtual machines where you can host 
your applications with secure and scalabe computational capacity.
São exemplos de 
uso do EC2 servidores de aplicativos, servidores web e servidores de bancos de dados. 
EC2 fornece máquinas virtuais (VMs) chamadas de **instâncias do EC2** que dão 
controle de administração total à diferentes sistemas operacionais como Windows, 
Linux Red Hat, SUSE linux, Ubuntu e Amazon Linux**.**  É possível executar qualquer 
número de instâncias de qualquer tamanho em diversos lugares do mundo em questão de 
minutos com o uso das Imagens de Máquinas Amazon (AMIs - Amazon Machine Images) .  
Podemos controlar o tráfego nestas instancias através da criação de security groups.

Ao criar um instância EC2 através do Launch Wizard é importante que você se aprofunde 
nas possíveis modificações. Em sistemas reais é comum modificar estas configurações 
para atender suas necessidades. Ao criar uma instância EC2 precisamos tomar algumas 
decisões importantes

## Selecionar uma AMI

Qual imagem AMI executar : Cria uma VM na AWS com sistema operacional Windows ou Linux.

1. **Quick Start :** Aferece AMI pré-compiladas
2. **My AMIs :** contém todas as AMIs, que você criou. É possível importar VM's de
    
    um servidor local e transformá-la em  uma AMI.
    
3. **AWS Marketplace :** Modelos pré-configurados de terceiros
4. **AMIs da comunidade :** AMIs compartilhados por terceiros

![https://rg6051loyag2io6oe11p1rcg-wpengine.netdna-ssl.com/wp-content/uploads/2015/04/intro-how-to-delete-unutilized-ebs.jpg](https://rg6051loyag2io6oe11p1rcg-wpengine.netdna-ssl.com/wp-content/uploads/2015/04/intro-how-to-delete-unutilized-ebs.jpg)

# 2 - Selecionar tipo de instância

Será necessário decidir o tipo de instância a ser criada. O tipo da instância é determinada por memória, processamento, disco e performance de rede.

1. Memória (RAM)
2. Capacidade de processamento (CPU)
3. Espaço e tipo de disco (Amazenamento)
4. Performance de rede

As categorias de tipo de instância podem ser :

1. Uso geral
2. Otimizadas para computação
3. Otimizadas para memória
4. Otimizadas para armazenamento
5. Otimizadas para computação acelerada.

**Nomenclatura :** As intâncias EC2 são nomeadas das seguinte forma : t3.large onde t é a família, 3 é a geração e large é o tamanho. Uma instância t3.2xlarge tem o dobro de potência de processamento e o dobro de memória de uma t3.xlarge, (t3.xlager = 4CPU e 16 GBram e t3.2xlarge = 8CPU e 32 GBram).

**Detalhes do tipo de instância :**

- a1,m4,m5,t2,t3 - uso geral - web aplications, ambiente de desenvolvimento, repositórios de código, ambientes de teste e outros
- c4,c5 - alta performance - modelagem científica, processamento em batch, jogos multiplayer, video encoding e outros
- r4,r5,x1,z1 - otimizada para memória - banco de dados de alto desempenho, mineração e análise de dados, BD em memória, processamento em tempo real, cluster apache spark
- f1,g3,g4,p2,p3 - compuatação acelerada (Machine Learning)
- d2,h1,i3 - Sistemas de arquivos distribuídos.

Instancias com recursos de rede : A largura de banda varia de acordo com o tipo de instância. Para maximizar performance de rede você pode 1 - Utilizar placement group cluster e especificar que todas as instâncias deverão estar na mesma zona de disponibilidade, 2 - Utilizar tipos de rede avançada - Elastic Network adapter (ENA) até 100 GBps e Interface Intel 82599 Virtual Function até 10 GBps.

## 3 - Configurações de Rede

Após escolher uma AMI e o tipo de instância a ser executada precisamos realizar a configuração da rede.  A escolha da região é a primeira coisa a ser feita. Isso pode ser feito verificando se você está na região desejada dentro do console do Amazon EC2 antes de iniciar a criação da instância.

Dentro da região você pode escolher se quer colocar a instância dentro de uma sub-rede existente, em qualquer VPC ou ainda criar uma nova VPC ou sub-rede. Se você não especificar nenhuma VPC ao executar uma instância, a instância será colocada na VPC padrão com um endereço IP público. Quando iniciamos uma VPC não-padrão, a sub-rede pode ainda ter um IP público.

Se desejar rodar aplicativos em uma instância EC2 que forneça, por meio de uma API, acesso a outros serviços da AWS.  Nestes casos a AWS permite que você crie um função do IAM à instância EC2. Observe que um caminho possível seria anexar as credenciais de acesso dentro da instância no entanto, isso é uma falha grave de segurança. Por esta razão anexamos uma função do IAM à instância do EC2 que concede acesso à um bucket no S3 por exemplo.

## 4 - Função do IAM

Se desejar rodar aplicativos em uma instância EC2 que forneça, por meio de uma API, acesso a outros serviços da AWS.  Nestes casos a AWS permite que vocêvincule um função do IAM à instância EC2. Observe que um caminho possível seria adicionar as credenciais de acesso dentro da instância no entanto, isso é uma falha grave de segurança. Nunca devemos armazenar credenciais da AWS em instâncias EC2. Por esta razão anexamos uma função do IAM à instância do EC2 que concede acesso à um bucket no S3 por exemplo.

## 5 -Dados de usuário

Use scripts de dados do usuário para personalizar o ambiente em tempo de execução de sua instância. O script é executado na primeira vez que a instância é iniciada. Pode ser usado para reduzir o número de AMIs que você cria

## 6 - Opções de armazenamento

É possível configurar onde o sistema operacional será instalado bem como anexar volumes de armazenamento ao executar a instância. As AMIs, por padrão, são configuradas para executar mais de um volume. É possível especificar o tamanho e o tipo dos volumes. Tipos de armazenamento significa se  o armazenamento será retido quando a instância for encerrada. É possível também especificar o tipo de criptografia a ser usada. Os tipos de armazenamento são :

           **Amazon Elastic Block Store (EBS) :** São instâncias de dados duráveis. Ao interromper o funcionamento de

uma instância e iniciá-lo novamente; os dados serão preservados.

**Armazenamento de instâncias do Amazon EC2 :** Os dados são temporários e estão vinculados ao host da instância EC2 e portanto, se a     instância for interrompida, todos os dados serão excluídos.

FAZER UM PARALELO COM INSTALAÇÂO LINUX

Outras formas de armazenamento são EFS que fornece um sistema de rede elástica, escalável e gerenciado ou ainda armazenar arquivos no próprio S3 que já possui por defult, escalabilidade, disponibilidade, segurança e desempenho.

![https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/aws-storage/choose-the-right-storage-service/images/75c6bec122ddc0a1a76b0bf99a89cae0_2-c-235-e-2-f-2448-40-c-3-8-c-7-b-e-9753-d-6-b-0-df-5.png](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/aws-storage/choose-the-right-storage-service/images/75c6bec122ddc0a1a76b0bf99a89cae0_2-c-235-e-2-f-2448-40-c-3-8-c-7-b-e-9753-d-6-b-0-df-5.png)

# 7 - TAG

Como o próprio nome sugere as TAG´s são rótulos que você atribui aos recursos AWS. TAGs são pares chave-valor definidos pelo usuário de forma a categorizar os recursos usados pelo usuário. Por exemplo uma TAG usada para uma instancia EC2 poderia ser, Servidor1, Node1 . Consiste de uma prática criar estratégias para o tagueamento dos recursos usados.

# 8 - Configuração dos grupos de segurança

Um grupo de segurança atua como firewall que controla o tráfego de rede entre as instâncias. Ao criar uma instâncias EC2 podemos especificar o security group~(SG) que será usado. Se nenhum sg for escolhido então um sg default será setado pela própria AWS. Você pode adicionar regras a cada sg que permitirão o tráfego para as instâncias que estiverem associadas a este SG, ou seja, quando uma instância é acessada todas as regras adicionadas a um SG serão verificadas para permitir o acesso as instâncias. Essas regras são definidas escolhendo a origem do acesso, regras de entrada e saída e as portas de acesso. A origem do acesso pode ser um endereço de IP, um intervalo de endereços, outro SG, ou ainda uma VPC endpoint.

ADICIONAR UM EXEMPLO de regra que permite acesso SSH pela porta TCP 22 com uma dada origem (MeuIP).

# 9 - Par de chaves

Um par de chaves consiste de uma chave privada e uma publica. Durante a criação da instância EC2 você pode escolher um par de chaves existentes ou ainda criar um novo par de chaves. Após criar a instância, faça o donwload das chaves (privada e pública). Somente no momento é possível fazer o download das chaves. Essas chaves serão usadas para fazer o acesso a instância por meio de um cliente SSH.  MOSTAR AQUI A TELA DO EC2.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e24786b0-d6bc-4883-b4c4-d24fa18b6716/Untitled.png)

As configurações que você escolheu durante sua a criação de sua instância poderão ser vistas na aba instances do EC2 como mostrado na imagem abaixo.

Nela você poderá ver os endereços de IP da instância, tipo da instnância, o ID da instância(selecionado pela própria AWS), o ID da VPC  e mais. Outra forma

de criar uma instância EC2, que não pela interface da AWS, é através da interface de linha de comando (CLI). Isso permite criar instâncias de forma

programática. É também possível utilizar SDKs oficiais da AWS para realizar essas tarefas de forma mais integrada ao seu código. Um exemplo de uma

SDK (Software Development Kit) largamente utilizada é a boto3 que fornece um integração entre python e AWS.

A criação de uma instância EC2 utlizando a CLI da AWS poderia ser feita por meio do comando:

aws ec2 run-instances

--image-id ami-1a3daw

--count 1

--instance-type c3.large

-- key-name MeuPardechaves

--security-groups MeuSG

--region us-east-1

ec2 - chama o serviço Elastic Compute Cloud (ec2)

image-id - representa o ID AMI

count - o número de instâncias que você vai executar.

instance-type - especifica o tipo de instância que será criada por exemplo c3.xlarge.

key-name - par de chaves (já existe)

- security-groups - SG (já existe)
- region - qual regiao da AWS será executada a sua instância. É neste região que a CLI procurará a AMI que será usada e também demais recursos necessários a execução do EC2.

Se o comando rodar com sucesso você terá como output o ID da instância e demais informações relevantes como mostrado abaixo(**COLOCAR IMAGEM**).

Uma instancia EC2 passa por diversos estados ao longo de seu ciclo de vida. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10773f06-68ea-472c-94d0-2c08afbeefb9/Untitled.png)

Depois que a instância for criada ela permanecerá em um estado pendente antes de entrar em execução e estar pronta pra ser acessada.  Analogamente ao processo de execução de uma instância, o processo de desligamento terá um processo intermediário antes de serem  completamente encerrados. Ao logo do processo de encerramento de um instância, a mesma permanece visível no console até sua exclusão permanente. Após a exclusão permanente uma a instância não pode ser recuperada. As instâncias EBS podem ser interrompidas antes de serem totalmente excluídas. Iniciar uma instância interrompida a coloca em um estado pendente e seleciona uma nova máquina host.

Quando uma instância é iniciada, ela recebe um endereço de IP público. IP já utilizados não podem ser reaproveitados. Após uma instância ser interrompida e ter seu IP desassociado, o mesmo volta para a lista de IP's disponíveis.  Se você deseja associar um endereço de IP a uma instância então deverá recorrer à um endereço de IP elástico dentro de uma região. Por default uma conta AWS tem permissão de 5 IP's elásticos por região no entanto pode-se solicitar mais caso seja necessário.

Você pode monitorar as instâncias através do Amazon CloudWatch que exibe em tempo "real" (near real time).   Essas informações podem                           ser  armazenadas pode até 15 meses.  Por default  o CloudWatch é atualizado a cada 5 minutos, para informações em intervalos menores é necessário                                     habilitar o monitoramento detalhado.

![https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/monitoring-on-aws/monitor-your-architecture-with-amazon-cloudwatch/images/522c742e37be736db2af0f8a720b1c02_f-05-f-9-a-02-2-a-81-4-fa-3-b-651-412-e-2222-bd-08.png](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/monitoring-on-aws/monitor-your-architecture-with-amazon-cloudwatch/images/522c742e37be736db2af0f8a720b1c02_f-05-f-9-a-02-2-a-81-4-fa-3-b-651-412-e-2222-bd-08.png)

[Criando uma Instância EC2](https://www.notion.so/Criando-uma-Inst-ncia-EC2-eb2ead0f33364696939fd11246d72334)