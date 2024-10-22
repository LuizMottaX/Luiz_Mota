# REPOSITÓRIO - ENGENHARIA DE SOFTWARE


- [REPOSITORIO ENG. SE SW.](#repositorio-eng-se-sw)
- [1. Introdução](#1-introdução)
- [2. Problema e descrição do negócio.](#2-problema-e-descrição-do-negócio)
- [3. Visão geral do sistema](#3-visão-geral-do-sistema)
- [4. Diagrama ER](#4-diagrama-er)
- [5. Diagrama de classe](#5-diagrama-de-classe)
- [6. Casos de uso](#6-casos-de-uso)
  - [6.1 Histórias de Usuário](#61-histórias-de-usuário)
- [7. Diagrama de componente](#7-diagrama-de-componente)
- [8. Diagrama de implantação](#8-diagrama-de-implantação)
- [9. Protótipo de telas](#9-prototipo-de-telas)
- [10 Diagrama de navegação de telas](#10-diagrama-de-navegação-de-telas)
- [11. Pilha tecnológica](#11-pilha-tecnológica)
- [12. Requisitos do sistema](#12-requisitos-do-sistema)
- [13. Considerações sobre segurança](#13-considerações-sobre-segurança)
- [14. manutenção e instalação](#14-manutenção-e-instalação)
- [15. Glossário](#15-glossario)


# 1. Introdução
O projeto a seguir apresenta um sistema desenvolvido para um pet shop. A empresa é considerada  micro e iniciou as atividades recentemente. Ao possuir serviços exclusivos, os sistemas presentes no mercado não se enquadram, desta forma, os proprietários decidiram desenvolver uma solução própria. Esta solução é detalhada.

# 2. Problema e descrição do negócio.

Descrição do cenário onde o sistema deverá funcionar:
                                                                                

 1  ->  A clínica veterinária atende apenas os animais: gatos e cachorros.                         
 2  -> Os clientes devem fazer um cadastro de si e dos animais.                                   
 3  ->  Os clientes devem informar as condições nas quais os animais chegam.                       
 4  ->  Os clientes devem informar o tipo de ração que o animal come.                              
 5  ->  O cliente deve informar hábitos do animal.                                                 
 6  ->  Para cada animal é possível que mais de um veterinário o atenda.                           
 7  ->  Os animais podem chegar e serem atendidos de acordo com uma agenda do dia.                 
 8  ->  Cada animal atendido receberá uma ficha e um prontuário.                                   
 9  ->  Outros donos podem querer marcar horários de atendimento futuro.                           
 10 ->  O atendimento gera uma receita para o animal.                                              
 11 ->  Quando um cliente chega na clínica veterinária ele é atendido por um atendente.            
 12 ->  O atendente deve verificar se existe agenda disponível com um veterinário.                 
 13 ->  O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso.          
 14 ->  O atendente deve levar o cliente e o animal até o veterinário.                             
 15 ->  O veterinário deve realizar uma entrevista com o dono do animal.                           
 16 ->  O resultado da entrevista deve ir para um formulário.                                      
 17 ->  O veterinário deverá examinar o animal e anotar em prontuário (ficha) suas observações.    
 18 ->  Dependendo da situação do animal, este receberá uma receita.   
 19 ->  O dono do animal deve informar se o mesmo possui alergia a alguma medicação.  
 20 ->  Registrar o diagnóstico e criar um plano de tratamento, incluindo prescrições e recomendações.                           
 21 ->  Registrar os medicamentos prescritos e o plano de administração.                                      
 22 ->  Programar e registrar consultas de acompanhamento para monitorar a evolução do tratamento.    
 23 ->  Criar faturas detalhadas para os serviços prestados, incluindo consultas, exames e tratamentos.   
 24 ->  Registrar pagamentos e atualizar o status financeiro no sistema.


# 3. Visão geral do sistema

# 4. Diagrama ER

```mermaid
erDiagram
    CLIENTS {
        string id PK "ID do Cliente"
        string name "Nome do Cliente"
        string contact "Contato do Cliente"
    }
    ANIMALS {
        string id PK "ID do Animal"
        string name "Nome do Animal"
        string type "Tipo (Gato/Cachorro)"
        string condition "Condição ao Chegar"
        string foodType "Tipo de Ração"
        string habits "Hábitos"
    }
    VETERINARIANS {
        string id PK "ID do Veterinário"
        string name "Nome do Veterinário"
        string specialty "Especialidade"
    }
    APPOINTMENTS {
        string id PK "ID do Atendimento"
        date date "Data do Atendimento"
        string time "Hora do Atendimento"
        string status "Status (Agendado/Realizado)"
    }
    RECORDS {
        string id PK "ID do Prontuário"
        string animalId FK "ID do Animal"
        string vetId FK "ID do Veterinário"
        string observations "Observações"
        string diagnosis "Diagnóstico"
        string treatmentPlan "Plano de Tratamento"
        string prescription "Prescrições"
        string followUp "Consultas de Acompanhamento"
    }
    BILLS {
        string id PK "ID da Fatura"
        string appointmentId FK "ID do Atendimento"
        float amount "Valor"
        string status "Status do Pagamento"
    }
    ATTENDANTS {
        string id PK "ID do Atendente"
        string name "Nome do Atendente"
    }
    
    CLIENTS ||--o{ ANIMALS : owns
    ANIMALS ||--o{ APPOINTMENTS : "receives"
    VETERINARIANS ||--o{ APPOINTMENTS : "conducts"
    APPOINTMENTS ||--o{ RECORDS : "generates"
    RECORDS ||--o{ BILLS : "bills"
    ATTENDANTS ||--o{ APPOINTMENTS : "manages"
```


# 5. Diagrama de classe

```mermaid
classDiagram
    %% Definições de classe

    class Cliente {
        +int id
        +string nome
        +string contato
    }

    class Animal {
        +int id
        +string nome
        +string tipo
        +string condicaoChegada
        +string tipoRacao
        +string habitos
    }

    class Veterinario {
        +int id
        +string nome
        +string especialidade
    }

    class Atendimento {
        +int id
        +date data
        +time hora
        +string status
    }

    class Registro {
        +int id
        +string observacoes
        +string diagnostico
        +string planoTratamento
        +string prescricoes
        +string acompanhamento
    }

    class Fatura {
        +int id
        +decimal valor
        +string status
    }

    class Atendente {
        +int id
        +string nome
    }

    class Medicamento {
        +int id
        +string nome
        +string descricao
    }

    class Prescricao {
        +int id
        +string dosagem
    }

    class ConsultaAcompanhamento {
        +int id
        +date data
    }

    %% Relacionamentos

    Cliente "1" -- "0..*" Animal : possui
    Animal "1" -- "0..*" Atendimento : recebe
    Veterinario "1" -- "0..*" Atendimento : realiza
    Atendimento "1" -- "0..1" Registro : gera
    Registro "1" -- "0..*" Fatura : gera
    Atendente "1" -- "0..*" Atendimento : gerencia
    Registro "1" -- "0..*" Prescricao : inclui
    Medicamento "1" -- "0..*" Prescricao : prescrito
    Registro "1" -- "0..*" ConsultaAcompanhamento : inclui
```

# 6. Casos de uso

   ![Diagrama de casos de uso](https://github.com/LuizMottaX/Luiz_Mota/blob/main/Figura1.png?raw=true) 

## 6.1 Histórias de Usuário

 ```

    1 - Cadastro de Cliente e Animal
        Como um cliente, quero me cadastrar e registrar meus animais (gato ou cachorro) no sistema, para que eu possa agendar consultas e receber atendimento adequado.

    2 - Informação sobre a Condição do Animal
        Como cliente, quero informar a condição em que meu animal chega à clínica, para que o veterinário tenha uma visão clara do estado de saúde inicial dele.

    2- Registro de Alimentação e Hábitos
        Como cliente, quero informar o tipo de ração que meu animal consome e seus hábitos (alimentação, comportamento), para que o veterinário possa ajustar recomendações conforme as necessidades do animal.

    3 - Marcar Consulta
        Como cliente, quero poder marcar horários de atendimento para meu animal, para garantir que ele seja atendido no momento mais conveniente e adequado.

    4 - Recebimento de Receita
        Como dono de animal, quero receber uma receita com as medicações e tratamentos recomendados após a consulta, para seguir o plano de tratamento do veterinário.

    5 - Fila de Espera e Acompanhamento
        Como atendente, quero verificar se há disponibilidade na agenda e, se não houver, colocar o cliente e seu animal na fila de espera para otimizar o fluxo de atendimentos.

    6 - Entrevista Inicial pelo Veterinário
        Como veterinário, quero realizar uma entrevista com o dono do animal antes do exame físico, para coletar informações essenciais sobre a saúde e os hábitos do animal.

    7 - Prontuário Completo
        Como veterinário, quero criar um prontuário completo para cada animal atendido, registrando todas as observações, diagnósticos e prescrições, para manter um histórico detalhado da saúde do animal.

    8 - Registro de Alergias e Medicações
        Como cliente, quero informar se meu animal tem alguma alergia a medicações, para que o veterinário possa evitar prescrever remédios que possam causar reações adversas.

    9 - Pagamento e Fatura
        Como cliente, quero receber uma fatura detalhada dos serviços prestados (consultas, exames e tratamentos) e efetuar o pagamento na clínica, garantindo que o status financeiro seja atualizado no sistema.

```

# 7. Diagrama de componente  

![Diagrama de Compenente](https://github.com/LuizMottaX/Luiz_Mota/blob/main/diagrama_compenente.png?raw=true) 

# 8. Diagrama de implantação

![Diagrama de Implatação](https://github.com/LuizMottaX/Luiz_Mota/blob/main/Diagrama_implatacao.png?raw=true)

# 9. Protótipo de telas

## 9.1. Tela de Login

![Tela de login SC](https://github.com/LuizMottaX/Luiz_Mota/blob/main/tela_login.png?raw=true)

## 9.2. Tela de Cadastro

![Tela de cadastro](https://github.com/LuizMottaX/Luiz_Mota/blob/main/cadastros.png?raw=true)

## 9.3. Tela de Grafico

![Tela de Grafico](https://github.com/LuizMottaX/Luiz_Mota/blob/main/graficos.png?raw=true)

## 9.4. Tela de Dashboard

![Tela de Dashboard](https://github.com/LuizMottaX/Luiz_Mota/blob/main/dashboard.png)

# 10 Diagrama de navegação de telas

# 11. Pilha tecnológica

# 12. Requisitos do sistema

# 13. Considerações sobre segurança

# 14. manutenção e instalação

# 15. Glossário

# 16. Script SQL

  ## 16.1 crie um scrit sql para MYSQL para gerar as tabelas para as regras de negócio.

  ```SQL
  -- Tabela de Clientes
CREATE TABLE Clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    contato VARCHAR(255) NOT NULL
);

-- Tabela de Animais
CREATE TABLE Animais (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    tipo ENUM('Gato', 'Cachorro') NOT NULL,
    condicao_chegada TEXT,
    tipo_racao VARCHAR(255),
    habitos TEXT,
    cliente_id INT,
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

-- Tabela de Veterinários
CREATE TABLE Veterinarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    especialidade VARCHAR(255)
);

-- Tabela de Atendimentos
CREATE TABLE Atendimentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    data DATE NOT NULL,
    hora TIME NOT NULL,
    status ENUM('Agendado', 'Realizado') NOT NULL,
    animal_id INT,
    atendente_id INT,
    FOREIGN KEY (animal_id) REFERENCES Animais(id)
);

-- Tabela de Registros (Prontuário)
CREATE TABLE Registros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    animal_id INT,
    veterinario_id INT,
    observacoes TEXT,
    diagnostico TEXT,
    plano_tratamento TEXT,
    prescricoes TEXT,
    acompanhamento TEXT,
    FOREIGN KEY (animal_id) REFERENCES Animais(id),
    FOREIGN KEY (veterinario_id) REFERENCES Veterinarios(id)
);

-- Tabela de Faturas
CREATE TABLE Faturas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    atendimento_id INT,
    valor DECIMAL(10, 2) NOT NULL,
    status ENUM('Pendente', 'Pago') NOT NULL,
    FOREIGN KEY (atendimento_id) REFERENCES Atendimentos(id)
);

-- Tabela de Atendentes
CREATE TABLE Atendentes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL
);

-- Tabela de Medicamentos
CREATE TABLE Medicamentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    descricao TEXT
);

-- Tabela de Prescrições
CREATE TABLE Prescricoes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    registro_id INT,
    medicamento_id INT,
    dosagem VARCHAR(255),
    FOREIGN KEY (registro_id) REFERENCES Registros(id),
    FOREIGN KEY (medicamento_id) REFERENCES Medicamentos(id)
);

-- Tabela de Consultas de Acompanhamento
CREATE TABLE ConsultasAcompanhamento (
    id INT AUTO_INCREMENT PRIMARY KEY,
    registro_id INT,
    data DATE NOT NULL,
    FOREIGN KEY (registro_id) REFERENCES Registros(id)
);
```

  ## 16.2 gere em SQL comandos INSERT com dados fictícios para as tabelas.

  ```SQL
-- Inserir dados na tabela Clientes
INSERT INTO Clientes (nome, contato) VALUES
('Maria Silva', 'maria.silva@example.com'),
('João Santos', 'joao.santos@example.com'),
('Ana Oliveira', 'ana.oliveira@example.com');

-- Inserir dados na tabela Animais
INSERT INTO Animais (nome, tipo, condicao_chegada, tipo_racao, habitos, cliente_id) VALUES
('Felix', 'Gato', 'Fraco, desidratado', 'Ração seca', 'Dormir muito', 1),
('Rex', 'Cachorro', 'Lesão na pata', 'Ração úmida', 'Brincar com bolas', 2),
('Luna', 'Gato', 'Saudável', 'Ração seca', 'Caçar brinquedos', 3);

-- Inserir dados na tabela Veterinarios
INSERT INTO Veterinarios (nome, especialidade) VALUES
('Dr. Carlos Almeida', 'Dermatologia'),
('Dra. Fernanda Costa', 'Cardiologia'),
('Dr. Paulo Mendes', 'Ortopedia');

-- Inserir dados na tabela Atendimentos
INSERT INTO Atendimentos (data, hora, status, animal_id, atendente_id) VALUES
('2024-09-20', '09:00:00', 'Agendado', 1, 1),
('2024-09-20', '10:00:00', 'Agendado', 2, 2),
('2024-09-21', '11:00:00', 'Realizado', 3, 3);

-- Inserir dados na tabela Registros
INSERT INTO Registros (animal_id, veterinario_id, observacoes, diagnostico, plano_tratamento, prescricoes, acompanhamento) VALUES
(1, 1, 'Pelagem opaca, sinais de desidratação.', 'Desidratação', 'Hidratação intravenosa, dieta equilibrada.', 'Solução salina', 'Reavaliação em 1 semana.'),
(2, 3, 'Lesão visível na pata direita.', 'Fratura na pata', 'Imobilização com gesso, analgésicos.', 'Analgesia e anti-inflamatório', 'Revisão em 10 dias.'),
(3, 2, 'Animais saudáveis, sem sinais de doença.', 'Saudável', 'Manutenção dos cuidados gerais.', NULL, 'Reavaliação anual.');

-- Inserir dados na tabela Faturas
INSERT INTO Faturas (atendimento_id, valor, status) VALUES
(1, 150.00, 'Pendente'),
(2, 200.00, 'Pago'),
(3, 100.00, 'Pendente');

-- Inserir dados na tabela Atendentes
INSERT INTO Atendentes (nome) VALUES
('Joana Pereira'),
('Ricardo Lima'),
('Patrícia Souza');

```


