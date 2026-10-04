# Fluxo de notificação

1. O Schedule Trigger executa o workflow a cada **1 minuto**.
2. A consulta principal lê `glpi_ticketvalidations`, `glpi_tickets` e `glpi_users`. Retorna `validacao_id`, `status`, `numero_chamado`, `titulo`, `nome_validador` e `telefone_validador` para linhas com `NOTIFICADO = 0`.
3. O IF verifica se `telefone_validador` está preenchido.
4. Quando está preenchido, o Code node converte o valor em string, remove caracteres não numéricos e zeros iniciais, acrescenta o prefixo `55` quando necessário e aceita comprimento final de 12 ou 13 dígitos. Produz `telefone_formatado`, `telefone_valido` e `erro_telefone`. O exemplo fictício `(11) 99999-9999` vira `5511999999999`.
5. O HTTP Request envia uma saudação, número e título do chamado, link para o GLPI e pedido de validação. A [mensagem de exemplo](../examples/mensagem-exemplo.md) usa dados fictícios.
6. Após o HTTP Request, o nó MySQL executa o SQL atual: `update glpi_ticketvalidations set NOTIFICADO = 1 where NOTIFICADO = 0`. A condição é **global** e pode marcar outras validações pendentes. O fluxo não consulta `telefone_valido` antes do envio.
7. Quando o telefone está vazio, o outro nó MySQL executa `UPDATE glpi_ticketvalidations SET NOTIFICADO = NULL WHERE id = {{ $('MySQL').item.json.validacao_id }}`.

O workflow preserva essa lógica e o texto da mensagem, exceto pela generalização necessária de referências privadas. Os riscos e propostas de mudança estão em [melhorias futuras](melhorias-futuras.md).
