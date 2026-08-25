# 🛡️ Guia de Laboratório 19: Blindagem e LGPD (Mascaramento de Dados)

## 🎯 Objetivo da Missão
A Lei Geral de Proteção de Dados (LGPD) exige que informações sensíveis (PII - *Personally Identifiable Information*) sejam protegidas. 

Cientistas de Dados precisam da idade, da doença e da cidade do paciente para treinar uma Inteligência Artificial, mas eles **não precisam** saber o nome completo ou o telefone da pessoa. 

Hoje, nosso laboratório se transforma em um bunker de **Cybersecurity**. Vocês aprenderão a utilizar funções de texto do SQL para "mascarar" e "anonimizar" os dados antes de exportá-los para a equipe de IA.

---

## 🏗️ Preparação: Adicionando Dados Sensíveis
Para testarmos o mascaramento, precisamos de dados realmente sigilosos. Vamos adicionar uma coluna de telefone na nossa tabela de pacientes.

Execute os comandos abaixo no MariaDB para preparar nosso cenário:
```sql
-- 1. Criando a coluna de telefone
ALTER TABLE pacientes ADD COLUMN telefone VARCHAR(15);

-- 2. Populando os telefones (DML)
UPDATE pacientes SET telefone = '43 99123-4567' WHERE id_paciente = 1;
UPDATE pacientes SET telefone = '43 98855-1234' WHERE id_paciente = 3;
UPDATE pacientes SET telefone = '43 99777-8899' WHERE id_paciente = 4;
```

---

## 🕵️‍♂️ 1. A Arte do Mascaramento (Funções de String)
No SQL, podemos manipular textos ("strings") usando funções nativas. As mais úteis para segurança são:
*   `LEFT(coluna, numero)`: Pega os primeiros "X" caracteres da esquerda.
*   `RIGHT(coluna, numero)`: Pega os últimos "X" caracteres da direita.
*   `CONCAT(texto1, texto2)`: Junta (concatena) dois ou mais textos.

**Exemplo de como esconder o final de um CPF:**
```sql
SELECT CONCAT(LEFT('123.456.789-00', 3), '.***.***-**');
-- Resultado: 123.***.***-**
```

### 🚩 Missão 1: Mascarando os Telefones
Um atendente de telemarketing precisa ligar para os pacientes, mas não queremos que ele exporte a lista com os números inteiros por segurança (ele só deve ver no sistema). 
*   Construa um comando `SELECT` que mostre o `nome` do paciente e o `telefone` mascarado. 
*   O telefone deve mostrar apenas o DDD e os 5 primeiros dígitos, e o resto deve ser substituído por asteriscos. **Exemplo esperado:** `43 99123-****`.

---

## 👻 2. Anonimização para a Inteligência Artificial
Diferente do mascaramento (que apenas esconde um pedaço do dado), a **Anonimização** altera o dado de forma que seja impossível rastrear quem é a pessoa original. 

### 🚩 Missão 2: Protegendo a Identidade (`UPDATE`)
A diretoria ordenou que a base de dados seja enviada para a equipe de Inteligência Artificial amanhã. 
*   Escreva um comando `UPDATE` que altere definitivamente a coluna `nome` de todos os pacientes.
*   A regra é: O nome do paciente deve ser substituído pela palavra "Paciente " concatenada com o seu próprio ID (ex: O paciente de ID 1 passará a se chamar "Paciente 1", o ID 3 será "Paciente 3").

**Sintaxe de Ajuda:**
```sql
UPDATE nome_da_tabela 
SET coluna = CONCAT('Texto Fixo ', id_da_linha);
```

---

## 🤝 Desafio Final: A View Segura (Pair Programming)
Alterar o dado original com `UPDATE` destrói a informação real (o que pode ser um problema se a recepção da clínica precisar do nome verdadeiro). 

A solução mais profissional no mercado é criar uma **VIEW** (uma tabela virtual) que já entrega os dados mascarados, sem alterar a tabela original.

1. **Em duplas:** Escrevam um comando para criar uma View chamada `vw_dados_seguros_ia`.
2. Essa View deve fazer um `SELECT` trazendo:
   * O ID do paciente.
   * O telefone mascarado (da Missão 1).
   * A idade.
   * A doença.
3. Testem executando `SELECT * FROM vw_dados_seguros_ia;`.
4. Salvem o script SQL e enviem para avaliação do professor.