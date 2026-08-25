# 🛠️ Guia de Laboratório 11: Povoando e Higienizando o Banco (DML)

## 🎯 Objetivo da Missão
Neste laboratório, vamos aprender como inserir, modificar e apagar os dados do nosso banco de dados utilizando a Linguagem de Manipulação de Dados (DML). 

Para quem trabalha com Inteligência Artificial, existe uma regra de ouro: **"Garbage In, Garbage Out"** (Lixo entra, Lixo sai). Se os dados inseridos no banco estiverem errados, incompletos ou forem apagados acidentalmente, qualquer modelo de Machine Learning que formos treinar no futuro aprenderá padrões errados e será inútil. A qualidade da IA começa aqui.

---

## ⚠️ O Paradoxo do Estagiário (Atenção!)
Existe uma lenda clássica na área de tecnologia sobre o "estagiário" que rodou um comando de atualização (`UPDATE`) ou exclusão (`DELETE`) e esqueceu de usar a cláusula de filtro (`WHERE`). O resultado? Ele alterou o nome de todos os clientes para o mesmo nome ou apagou o banco de dados inteiro da empresa em milissegundos! 

Hoje, vocês aprenderão a **NUNCA** cometer esse erro. O comando `WHERE` é o seu maior aliado.

---

## 1. Injetando Conhecimento (`INSERT`)
O comando `INSERT` é utilizado para adicionar novas linhas (registros) em uma tabela. Sem dados, nosso sistema é apenas uma casca vazia.

**Sintaxe Básica:**
```sql
INSERT INTO nome_da_tabela (coluna1, coluna2, coluna3) 
VALUES ('Valor 1', 'Valor 2', 'Valor 3');
```

> **Dica de Ouro:** Se a sua Chave Primária (ex: id_paciente) foi configurada como AUTO_INCREMENT na criação da tabela, você não precisa digitá-la aqui. O próprio banco de dados vai gerar o próximo número sozinho!

### 🚩 Missão 1: Os Primeiros Registros
* Abra o seu ambiente do MariaDB.
* Escreva e execute comandos INSERT para cadastrar 3 novos pacientes na tabela pacientes.
* Escreva e execute comandos para cadastrar 2 novos médicos na tabela medicos.

---

## 2. Higienização de Dados (`UPDATE`)
No mundo real, os dados chegam com muitos erros de digitação (ex: cidade "Sãão Pualo" ou idades incorretas). A etapa de higienização corrige essas falhas usando o UPDATE para alterar registros que já existem.

**Sintaxe Segura (Sempre use o WHERE!):**
```sql
UPDATE nome_da_tabela 
SET coluna_para_mudar = 'Novo Valor Corrigido' 
WHERE id_da_linha = 1;
```

### 🚩 Missão 2: Correção de Rota
O médico "Dr. João Silva" concluiu uma nova especialização e agora atende exclusivamente pela "Cardiologia".

* Escreva e execute o código SQL para atualizar a especialidade apenas do Dr. João Silva.

> **Atenção:** Se você esquecer o WHERE, todos os médicos da clínica vão virar cardiologistas!

---

## 3. O Direito ao Esquecimento e a LGPD (`DELETE`)
A Lei Geral de Proteção de Dados (LGPD) garante que um cliente pode solicitar a exclusão total de seus dados pessoais da base de uma empresa. Para isso, utilizamos o DELETE.

**Sintaxe Extremamente Perigosa (Sempre use o WHERE!):**
```sql
DELETE FROM nome_da_tabela 
WHERE id_da_linha = 5;
```

### 🚩 Missão 3: Exclusão Segura
O paciente de ID número 2 solicitou a exclusão de seus dados do sistema da clínica.

* Escreva o comando SQL para apagar este paciente.
* Reflexão para a dupla: O que aconteceu com as consultas que ele já tinha agendado na tabela consultas? (Lembrem-se da restrição ON DELETE CASCADE que configuramos na nossa infraestrutura. Verifiquem a tabela de consultas para ver o efeito cascata em ação).

---

## 🤝 Desafio Final: Pair Programming (Entrega da Aula)
Agora que vocês dominaram os comandos de manipulação, é hora do desafio final da aula.

* **Formem duplas:** Trabalhem lado a lado nas estações ou usem ferramentas de compartilhamento. Um de vocês será o "Piloto" (quem digita) e o outro o "Copiloto" (quem revisa a lógica e procura erros). Alternem os papéis a cada 10 minutos.
* **Criem o Script:** Abram um arquivo em branco no editor de código e salvem com o nome carga_inicial_clinica.sql.
* **O Escopo:** Escrevam neste arquivo todos os comandos SQL necessários para simular o cadastro completo do sistema:
    * Cadastrar 5 novos pacientes.
    * Cadastrar 3 novos médicos.
    * Cadastrar 4 consultas cruzando os IDs dos médicos e pacientes recém-criados.
* **Entrega:** Testem se o script roda do início ao fim sem erros no MariaDB e enviem o arquivo .sql no Microsoft Teams para avaliação do professor.