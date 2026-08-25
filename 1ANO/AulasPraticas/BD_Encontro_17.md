# 🤖 Guia de Laboratório 17: A Ponte para a IA (Extraindo Datasets)

## 🎯 Objetivo da Missão
Até agora, nós modelamos, criamos e povoamos o nosso banco de dados relacional. Mas como uma Inteligência Artificial consome isso? 

Modelos de Machine Learning (Aprendizado de Máquina) geralmente não se conectam diretamente a dezenas de tabelas espalhadas. Eles precisam de um **Dataset** (Conjunto de Dados) consolidado, limpo e focado, geralmente exportado em formatos como `.csv` ou `.json`. Nossa missão hoje é extrair a inteligência do banco de dados e prepará-la para a IA.

---

## 🧠 1. Ideathon de Dados: O que importa para a máquina?
Na Inteligência Artificial, chamamos as colunas do nosso banco de dados de **Features** (Características). Se você entregar dados inúteis para a IA, ela vai encontrar padrões falsos. 

Por exemplo, o "Nome" ou o "CPF" do paciente ajuda a prever qual doença ele vai ter? **Não.** Mas a "Idade", a "Cidade" e a "Especialidade" do médico que o atendeu podem revelar padrões fortíssimos de saúde pública!

### 🚩 Missão 1: Seleção de Features (Trabalho em Dupla)
1. Analisem as tabelas `pacientes`, `medicos` e `consultas` do nosso banco de dados.
2. Discutam e anotem: Se fôssemos treinar uma IA para prever a **probabilidade de surtos de doenças**, quais colunas nós deveríamos extrair? Quais deveríamos ignorar?

---

## 🧹 2. Higienização e Cruzamento (SQL para ML)
Agora precisamos unir os dados que escolhemos e garantir que não haja "sujeira" (valores nulos). Algoritmos de IA odeiam campos vazios. Para isso, usaremos o filtro `IS NOT NULL`.

### 🚩 Missão 2: A Query Perfeita
Construam um comando `SELECT` que atenda aos seguintes requisitos:
1. Utilize `INNER JOIN` para unir as tabelas de consultas, pacientes e médicos.
2. Traga **apenas** as colunas úteis para a nossa IA (ex: idade, cidade, doenca, especialidade). Não tragam nomes, IDs internos ou datas de nascimento completas.
3. Adicione uma cláusula `WHERE` para garantir que a coluna `doenca` não seja nula (`IS NOT NULL`), filtrando apenas pacientes já diagnosticados.

**Sintaxe de Ajuda (Filtro Anti-Nulo):**
```sql
WHERE coluna_importante IS NOT NULL;
```

---

## 📦 3. O Pote de Ouro: Exportando o Dataset
Com a consulta rodando perfeitamente e os dados limpos aparecendo na tela, precisamos tirar isso do MariaDB e transformar em um arquivo físico que um Cientista de Dados possa carregar no Python.

### 🚩 Missão 3: Gerando o CSV
1. Execute a sua query da Missão 2 na sua ferramenta visual (DBeaver, phpMyAdmin, HeidiSQL, etc.).
2. Procure o botão de **Exportação** (geralmente "Export Resultset" ou "Exportar").
3. Escolha o formato **CSV** (Comma-Separated Values).
4. Salve o arquivo na sua máquina com o nome `dataset_clinica_ML.csv`.
5. Abra o arquivo no Bloco de Notas ou no Excel para verificar se os dados estão separados por vírgula e prontos para a Inteligência Artificial.