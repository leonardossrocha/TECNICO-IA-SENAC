#  Guia do Professor e Gabarito - Lab 18 (Tribunal dos Dados)

##  Orientações de Condução (Metodologias Ativas)
*   **Organização do Ambiente:** Como o laboratório possui estações fixas, utilize o Discord, Microsoft Teams ou Google Meet. Crie três salas/canais separados para a etapa de "Preparação" (para que os grupos não ouçam a estratégia uns dos outros). Depois, reúna todos no canal principal para o embate.
*   **O Papel do Professor (O Juiz):** Você é o mediador. Não deixe o debate virar bagunça. Controle o cronômetro rigidamente. Se os alunos começarem a desviar o assunto apenas para a medicina ou política, force-os a voltar para a tecnologia: *"Promotoria, mas qual foi o erro na chave estrangeira ou na falta de atributos do modelo relacional?"*.
*   **Marcas Formativas em Ação:** Observe e avalie a *Colaboração e comunicação* (como eles organizam as falas) e a *Visão crítica* (a capacidade de enxergar que código puro gera impacto social).

---

##  Gabaritos de Argumentação (O que esperar dos alunos)

Durante a mediação, caso os grupos fiquem travados, você pode usar as perguntas abaixo para instigá-los a encontrar os argumentos corretos.

### Para provocar a Acusação (Se estiverem fracos):
*   *"O Arquiteto de Dados não deveria ter feito um levantamento de requisitos melhor na SA 1? Eles aceitaram qualquer dado do cliente sem questionar a origem?"*
*   **Argumento de Ouro:** A modelagem foi míope. Faltou a entidade `DADOS_SOCIOECONOMICOS` ligada à entidade `PACIENTE`. Faltou perguntar ao cliente (o hospital) o que os dados realmente significavam.

### Para provocar a Defesa (Se estiverem perdendo):
*   *"O papel do DBA (Database Administrator) é garantir que o banco seja rápido, seguro e sem redundâncias (3FN). A regra de negócio não vem da diretoria do hospital?"*
*   **Argumento de Ouro:** O banco de dados apenas armazena fatos (`INSERT` de consultas). O viés não está no armazenamento, está no algoritmo de Machine Learning que correlacionou "número de visitas" com "prioridade cirúrgica". A falha é do Engenheiro de IA, não do Arquiteto de Banco de Dados.

### O Veredito Ideal do Júri (Solução Técnica)
Independentemente de votarem culpado ou inocente, o foco da sua avaliação deve ser a **solução de modelagem** que o Júri vai propor. Uma excelente resposta envolveria:
1.  Criar uma nova tabela `Postos_Saude_Bairro` para mapear a infraestrutura local.
2.  Adicionar um atributo `distancia_media_posto` na tabela de `Pacientes`.
3.  Modificar a query de extração (DQL) para que a IA não leia o número absoluto de consultas sem cruzar com a disponibilidade de médicos na região do paciente.