# 👨‍🏫 Guia do Professor e Gabarito - Lab 11 (DML)

## 📌 Orientações de Condução (Metodologias Ativas)
*   **Mediação Ativa:** Durante a Missão 2 e 3, circule pelo laboratório. Alguns alunos inevitavelmente vão esquecer o `WHERE`. Deixe que errem e percebam que apagaram ou alteraram a tabela toda. Ensine-os a dropar a tabela e rodar o script DDL da aula anterior para restaurá-la. Isso fixa o aprendizado do erro muito melhor do que apenas o aviso verbal.
*   **Reflexão LGPD:** Na Missão 3, chame a atenção da turma para debater o `ON DELETE CASCADE`. Faça-os perceber que apagar o dado central (paciente) sem tratar as chaves estrangeiras pode causar inconsistências ou, no nosso caso, perda de histórico de consultas.
*   **Pair Programming:** Garanta que os papéis de "Piloto" e "Copiloto" estão sendo respeitados no Desafio Final, para que nenhum aluno fique passivo na estação de trabalho.

---

## 🛑 Gabaritos Esperados

### Gabarito da Missão 1 (`INSERT`)
Os alunos têm liberdade criativa para os dados fictícios. Valide a precisão da sintaxe e a omissão correta da Chave Primária (caso esteja como auto incremento).

```sql
-- Inserindo 3 pacientes
INSERT INTO pacientes (nome, idade, cidade, doenca) 
VALUES 
('Ana Costa', 28, 'Londrina', 'Gripe'),
('Carlos Almeida', 45, 'Cambé', 'Enxaqueca'),
('Beatriz Souza', 32, 'Ibiporã', 'Dengue');

-- Inserindo 2 médicos
INSERT INTO medicos (nome, especialidade, idade) 
VALUES 
('Dr. João Silva', 'Clínico Geral', 50),
('Dra. Marta Santos', 'Pediatria', 42);
```

### Gabarito da Missão 2 (`UPDATE`)
A forma mais robusta é aplicar o filtro pela Chave Primária. Se o aluno usar o nome, alerte sobre o risco de homônimos no banco de dados.

```sql
-- Abordagem pelo Nome
UPDATE medicos 
SET especialidade = 'Cardiologia' 
WHERE nome = 'Dr. João Silva';

-- Abordagem recomendada (pela PK)
UPDATE medicos 
SET especialidade = 'Cardiologia' 
WHERE id_medico = 1; 
```

### Gabarito da Missão 3 (`DELETE`)
Validar o uso imperativo da cláusula `WHERE`.

```sql
DELETE FROM pacientes 
WHERE id_paciente = 2; 
```
*   **Gabarito da Reflexão:** O aluno deve responder (verbalmente ou nos comentários do código) que as consultas atreladas ao paciente 2 foram excluídas automaticamente da tabela `consultas` devido à restrição `ON DELETE CASCADE` implementada no esquema lógico.

### Gabarito do Desafio Final (`carga_inicial_clinica.sql`)
O script que os alunos irão submeter devem conter a seguinte estrutura lógica (os dados em si podem variar):

```sql
-- Cadastro de 5 pacientes
INSERT INTO pacientes (nome, idade, cidade) VALUES 
('Lucas Mendes', 19, 'Londrina'),
('Mariana Ribeiro', 25, 'Londrina'),
('Felipe Torres', 30, 'Rolândia'),
('Julia Farias', 22, 'Londrina'),
('Roberto Nunes', 55, 'Cambé');

-- Cadastro de 3 médicos
INSERT INTO medicos (nome, especialidade) VALUES 
('Dra. Helena', 'Dermatologia'),
('Dr. Renato', 'Ortopedia'),
('Dra. Camila', 'Neurologia');

-- Cadastro de 4 consultas (cruzando os IDs criados acima)
-- Validar se os alunos estão usando IDs que realmente existem nas tabelas fortes.
INSERT INTO consultas (data, hora, cod_p, cod_m) VALUES 
('2026-10-15', '09:00', 1, 1),
('2026-10-15', '10:30', 2, 2),
('2026-10-16', '14:00', 3, 1),
('2026-10-17', '16:00', 4, 3);
```