# 👨‍🏫 Guia do Professor e Gabarito - Lab 19 (Blindagem e LGPD)

## 📌 Orientações de Condução (Metodologias Ativas)
*   **Contextualização:** Inicie a aula perguntando: *"O que aconteceria se um hacker invadisse o banco de dados da clínica hoje? Ele saberia quem tem qual doença?"*. Isso ativa a *Atitude Sustentável* e a *Visão Crítica*.
*   **Mediação na Missão 1:** O uso do `LEFT` e do `CONCAT` costuma gerar erros de sintaxe (parênteses faltando). Encoraje o "Copiloto" (na dinâmica de duplas) a revisar a sintaxe antes de pedir ajuda.
*   **O Conceito de VIEW:** O Desafio Final introduz a `VIEW`. Explique aos alunos do Ensino Médio que uma VIEW é como uma "lente de óculos": ela muda a forma como enxergamos os dados da tabela, mas não altera a tabela física que está guardada no disco rígido.

---

## 🛑 Gabaritos Esperados

### Gabarito da Preparação (Adicionando Dados)
Apenas valide se todos rodaram os comandos fornecidos no roteiro para que a coluna `telefone` exista antes de começarem as missões.

### Gabarito da Missão 1 (Mascarando os Telefones)
O `LEFT` deve pegar os primeiros 9 caracteres (contando com o espaço) do telefone.

```sql
SELECT 
    nome, 
    CONCAT(LEFT(telefone, 9), '****') AS telefone_mascarado
FROM pacientes
WHERE telefone IS NOT NULL;
```
*Se algum aluno usar a função `REPLACE`, valide a criatividade, mas alerte que o `CONCAT + LEFT` é mais padronizado para mascaramento de pontas.*

### Gabarito da Missão 2 (Anonimização Definitiva)
Este comando destruirá os nomes originais e substituirá pela concatenação. É importante que eles vejam o impacto de um `UPDATE` massivo (sem WHERE), mas desta vez, intencional.

```sql
UPDATE pacientes 
SET nome = CONCAT('Paciente ', id_paciente);

-- Para testar:
SELECT * FROM pacientes;
```

### Gabarito do Desafio Final (`vw_dados_seguros_ia`)
Criação da tabela virtual. Este é o suprassumo da governança de dados para IA.

```sql
CREATE VIEW vw_dados_seguros_ia AS
SELECT 
    id_paciente,
    CONCAT(LEFT(telefone, 9), '****') AS telefone_seguro,
    idade,
    doenca
FROM pacientes;

-- Chamando a View para confirmar:
SELECT * FROM vw_dados_seguros_ia;
```