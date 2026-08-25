# Guia de Laboratório 18: O Tribunal dos Dados (Ética e Viés)

## Objetivo da Missão
Até agora, aprendemos que os dados alimentam a Inteligência Artificial. Mas o que acontece se esses dados contiverem preconceitos históricos ou erros de modelagem? A IA se torna racista, elitista ou injusta. Chamamos isso de **Viés Algorítmico**.

Hoje, os computadores ficam de lado. Nosso laboratório será um tribunal. Vocês debaterão a responsabilidade de quem projeta o banco de dados quando a IA toma uma decisão que prejudica a sociedade.

---

## O Caso: O Escândalo do "Triage.AI"
Imagine que a Secretaria de Saúde implantou um novo sistema de Inteligência Artificial chamado **Triage.AI** em um grande hospital de Londrina. O objetivo da IA era analisar o banco de dados de pacientes e definir a prioridade na fila de espera por cirurgias.

**O Problema:** 
Após seis meses, uma reportagem investigativa descobriu que pacientes de bairros nobres (ex: Gleba Palhano) estavam sendo operados em semanas, enquanto pacientes de regiões periféricas (ex: Cinco Conjuntos) esperavam meses, mesmo com a mesma gravidade médica.

**A Causa no Banco de Dados:**
A IA foi treinada usando a tabela `historico_consultas`. O algoritmo aprendeu que os pacientes da Gleba Palhano tinham um histórico de 10 visitas anuais ao médico, enquanto os dos Cinco Conjuntos tinham apenas 1 ou 2. 
A IA cruzou os dados e deduziu, de forma errada: *"Quem vai mais ao médico se importa mais com a saúde e tem mais chance de sucesso na cirurgia. Logo, devem ter prioridade"*. 
O banco de dados falhou em registrar um detalhe crucial: os pacientes da periferia iam menos ao médico porque faltavam postos de saúde na região deles, e não porque eram menos graves. O modelo de dados era cego para a realidade social.

---

## A Dinâmica: Júri Simulado Online
A turma será dividida em três grupos nos canais de voz/texto.

### Grupo 1: A Acusação (Promotoria)
Vocês representam os pacientes prejudicados. O objetivo de vocês é **culpar a equipe de desenvolvedores e arquitetos de banco de dados**.
*   **Argumento Central:** Os desenvolvedores são responsáveis. Eles modelaram as tabelas sem visão crítica. Faltaram colunas no banco de dados que explicassem o contexto social (como "distância do posto de saúde" ou "renda"), o que envenenou a IA.

### Grupo 2: A Defesa (Advogados dos Desenvolvedores)
Vocês representam os profissionais de TI que criaram o banco de dados. O objetivo é **inocentar a equipe técnica**.
*   **Argumento Central:** O banco de dados reflete a realidade fornecida pela direção do hospital. Desenvolvedor não é médico nem sociólogo. A tabela `historico_consultas` estava tecnicamente perfeita e normalizada (em 3FN). A culpa é de quem usou os dados cegamente para treinar a IA.

### Grupo 3: O Conselho de Sentença (Júri)
Vocês são os juízes. Durante o debate, vocês devem ouvir em silêncio e fazer anotações.
*   **A Missão:** Ao final, vocês devem votar se os desenvolvedores são **Culpados** ou **Inocentes** por negligência na modelagem de dados. Além do veredito, vocês devem propor uma solução técnica (Quais novas tabelas ou colunas deveriam ser criadas no MER para evitar que a IA seja injusta no futuro?).

---

##  Regras do Tribunal
1. **Preparação (15 min):** Os grupos de Acusação e Defesa se reúnem em seus canais para montar seus argumentos e escolher 2 oradores. O Júri discute os critérios de avaliação.
2. **Acusação (5 min):** Apresenta por que a modelagem de dados foi negligente.
3. **Defesa (5 min):** Apresenta por que a culpa foge do escopo técnico do banco de dados.
4. **Réplica e Tréplica (3 min cada):** Respostas diretas aos ataques.
5. **Veredito (10 min):** O Júri delibera, anuncia a sentença e apresenta a proposta de correção do Diagrama ER.