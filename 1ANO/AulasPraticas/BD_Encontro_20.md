# 🚀 Guia de Laboratório 20: Code Review e Entrega Final

## 🎯 Objetivo da Missão
Chegamos ao último encontro da nossa Unidade Curricular! Vocês projetaram modelos, criaram tabelas, garantiram a integridade dos dados e até aplicaram regras de LGPD focadas em Inteligência Artificial.

No mercado de tecnologia real (em empresas como Google, Nubank ou TCS), nenhum código vai para o sistema principal sem antes passar por um **Code Review (Revisão de Código)**. Hoje, vocês atuarão como Engenheiros de Dados Sêniores, avaliando o trabalho de outra equipe.

---

## 🔄 1. A Troca de Repositórios
A revisão de código serve para encontrar bugs que o autor original não viu e para garantir que o código está limpo e legível. O foco não é criticar o colega, mas sim melhorar o projeto em equipe!

### 🚩 Missão 1: Preparando o Terreno
1. O professor indicará com qual dupla vocês farão a troca.
2. Enviem o script final de vocês (`carga_inicial_clinica.sql` ou o script completo de criação do banco) para a dupla parceira via Microsoft Teams ou Discord.
3. Baixem o script que a outra dupla enviou para vocês.

---

## 🕵️‍♂️ 2. Execução e Validação (Testes)
Vocês não podem apenas "ler" o código, precisam testá-lo na prática.

### 🚩 Missão 2: Rodando o Código Alheio
1. Abram o MariaDB.
2. Criem um banco de dados de teste temporário (Ex: `CREATE DATABASE teste_revisao; USE teste_revisao;`).
3. Abram o arquivo `.sql` da outra dupla e executem o código completo.
4. Anotem: Rodou de primeira? Deu algum erro de sintaxe? Faltou criar alguma tabela antes de inserir os dados?

---

## 📋 3. O Checklist de Qualidade (Feedback)
Avaliador bom é aquele que documenta o que encontrou.

### 🚩 Missão 3: Preenchendo o Parecer Técnico
Copiem o checklist abaixo, preencham com "Sim", "Não" ou "Parcialmente", e enviem de volta para a dupla avaliada (com cópia para o professor).

**Checklist de Code Review:**
* [ ] **Execução:** O script rodou do início ao fim sem erros vermelhos no console?
* [ ] **Estrutura (DDL):** As tabelas possuem Chave Primária (`PRIMARY KEY`) configuradas corretamente?
* [ ] **Integridade (Constraints):** Existem Chaves Estrangeiras (`FOREIGN KEY`) conectando as tabelas?
* [ ] **Povoamento (DML):** Os `INSERTs` funcionaram e os dados fazem sentido?
* [ ] **Segurança/LGPD:** Existe alguma técnica de mascaramento ou o uso de `VIEW` para proteger dados sensíveis?
* [ ] **Organização:** O código está legível? Tem comentários (`--`) explicando as etapas?

**Comentário Final da Revisão:**
*(Escrevam aqui um elogio sobre algo legal que a dupla fez e uma sugestão construtiva de melhoria).*

---

## 🏆 Encerramento
Parabéns! Vocês concluíram a base fundamental para qualquer projeto de Inteligência Artificial: **um banco de dados bem estruturado, íntegro e seguro.** O mercado de tecnologia espera por vocês!