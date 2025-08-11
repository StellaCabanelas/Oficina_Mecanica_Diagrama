# Sistema de Controle e Gerenciamento de Ordens de Serviço - Oficina Mecânica

## 📋 Descrição do Projeto
Este projeto representa o **modelo conceitual e lógico** de um sistema para controle e gerenciamento de **execução de ordens de serviço** em uma oficina mecânica.

O sistema permite registrar clientes, veículos, ordens de serviço, peças e serviços executados, bem como controlar valores de mão de obra e o status de cada ordem.

## 🛠 Cenário
- **Clientes** levam veículos à oficina para conserto ou revisões periódicas.
- Cada veículo é atribuído a um **mecânico** ou equipe, que identifica os serviços a executar e preenche uma **Ordem de Serviço (OS)** com data de entrega prevista.
- O valor final da OS é calculado a partir de:
  - Valor de cada serviço (consultado na **tabela de referência de mão de obra**).
  - Valor das peças utilizadas.
- O cliente autoriza a execução dos serviços.
- A equipe avalia e executa os serviços, atualizando o status da OS.

## 📊 Modelo de Dados

### **Cliente**
- `idCliente` (PK)
- `Nome`
- `Identificação` (CPF/CNPJ)
- `Endereço`
- `Telefone`

### **Veículo**
- `idVeículo` (PK)
- `Modelo`
- `Ano`
- `Marca`
- `Cliente_idCliente` (FK)

### **Mecânico**
- `idMecânico` (PK)
- `Nome`
- `Endereço`
- `Especialidade`

### **Ordem de Serviço (OS)**
- `Veículo_idVeículo` (FK)
- `Mecânico_idMecânico` (FK)
- `Data de emissão`
- `Valor`
- `Data para conclusão`
- `Número`
- `Status`

### **Peças**
- `idPeças` (PK)
- `Descrição`
- `Valor`

### **Serviço**
- `idServiço` (PK)
- `Valor` *(opcional — manter somente se o valor for fixo para todos os mecânicos)*

### **Referência de Mão de Obra**
- `Mecânico_idMecânico` (FK)
- `Serviço_idServiço` (FK)
- `Valor` *(valor do serviço quando executado por determinado mecânico)*

### **Peças_has_Ordem de Serviço (OS)**
Tabela associativa para relação N:N entre **Peças** e **OS**.

### **Ordem de Serviço (OS)_has_Serviço**
Tabela associativa para relação N:N entre **OS** e **Serviços**.

## 🔗 Relacionamentos
- Um **Cliente** pode ter **vários Veículos** (1:N).
- Um **Veículo** pode ter **várias OS**, mas uma OS pertence a **um único veículo** (1:N).
- Um **Mecânico** pode estar ligado a **várias OS** (1:N).
- Uma **OS** pode conter **vários Serviços** e um Serviço pode estar em várias OS (N:N).
- Uma **OS** pode conter **várias Peças** e uma Peça pode estar em várias OS (N:N).
- Um **Serviço** pode ter valores diferentes para mecânicos diferentes, definidos em **Referência de Mão de Obra**.

## 📌 Observações
- O valor total da OS é calculado somando:
  - Valor de cada serviço na **Referência de Mão de Obra**.
  - Valor de cada peça utilizada.
- O campo `Status` da OS permite indicar se está **Aberta**, **Em execução** ou **Concluída**.
- O campo `Valor` em **Serviço** é opcional e pode ser removido caso todos os preços venham exclusivamente da tabela de referência.

## Diagrama
<img width="1578" height="926" alt="Image" src="https://github.com/user-attachments/assets/9450aa1c-2c24-49cc-9468-940ac96f584d" />
