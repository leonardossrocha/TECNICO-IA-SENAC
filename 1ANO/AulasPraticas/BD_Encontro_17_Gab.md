# 👨‍🏫 Guia do Professor e Gabarito - Lab 17 (Ponte para a IA)

## 📌 Orientações de Condução (Metodologias Ativas)
*   **Ideathon Direcionado (Missão 1):** O grande objetivo aqui é desenvolver a **Visão Crítica**. Provoque os alunos: *"Se a IA aprender que o paciente 'Lucas' teve Dengue, ela pode achar que todo mundo chamado Lucas tem mais chance de ter Dengue. Isso é viés algorítmico!"*. Faça-os entender a diferença entre dados identificadores (ruído) e dados preditivos (features).
*   **Mediação na Missão 2:** Eles já aprenderam JOINs nas aulas anteriores, mas podem ter dificuldade em agrupar as três tabelas ao mesmo tempo. Deixe que tentem estruturar a lógica das chaves estrangeiras.
*   **Restrições de Laboratório (Missão 3):** Exportar usando a interface gráfica é a melhor opção em laboratórios de Ensino Médio. O comando nativo do MariaDB `INTO OUTFILE` exige permissões de segurança de pasta no sistema operacional que geralmente estão bloqueadas para alunos em redes institucionais. Foque no uso do botão "Exportar" da IDE visual que estão utilizando.

---

## 🛑 Gabaritos Esperados

### Gabarito da Missão 1 (Seleção de Features)
Os alunos devem concluir que:
*   **Colunas a Ignorar (Ruído/Identificadores):** `id_paciente`, `nome` (do paciente e do médico), `data` da consulta (a menos que fosse extraído apenas o mês para sazonalidade).
*   **Colunas a Extrair (Features Úteis):** `idade` (paciente), `cidade` (paciente), `doenca` (paciente/diagnóstico), `especialidade` (médico).

### Gabarito da Missão 2 (A Query de Extração)
Espera-se uma query limpa, focada e sem a presença do famigerado `SELECT *`.

```sql
SELECT 
    p.idade, 
    p.cidade, 
    p.doenca, 
    m.especialidade 
FROM consultas c
INNER JOIN pacientes p ON c.cod_p = p.id_paciente
INNER JOIN medicos m ON c.cod_m = m.id_medico
WHERE p.doenca IS NOT NULL;
```
*Observação:* Dependendo de como os alunos nomearam as chaves primárias e estrangeiras nas aulas anteriores, os nomes dos campos (`cod_p`, `id_paciente`) podem variar levemente. Avalie a lógica do `JOIN` e o uso correto do `IS NOT NULL`.

### Avaliação Final
Verifique as telas ou os arquivos entregues. O arquivo `.csv` gerado na Missão 3 deve conter a primeira linha como cabeçalho (Idade, Cidade, Doença, Especialidade) e as demais linhas com os dados limpos, separados por vírgulas ou ponto-e-vírgula.