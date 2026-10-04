# Segurança

- Armazene senhas e chaves nas **Credentials do n8n**, nunca no JSON do workflow.
- Generalize domínios internos, instâncias, IDs de credenciais e metadados antes de exportar para publicação.
- Não versione dados pessoais, telefones de usuários nem resultados reais de consultas.
- Use apenas dados fictícios nos exemplos e não publique detalhes de chamados reais.
- Mantenha `.env` fora do Git; somente `.env.example` deve ser público.
- Audite **cada novo export do n8n** antes de publicar. Reatribuir uma credencial ou editar URLs pode reintroduzir dados privados.
- Execute uma busca manual por identificadores privados e, se disponível, uma varredura com **gitleaks** antes de commits.

O workflow público preserva o SQL e a estrutura atuais. Isso inclui a atualização global de `NOTIFICADO`, que exige avaliação antes de operação real.
