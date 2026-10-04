# Configuração do GLPI

A credencial MySQL do n8n precisa acessar `glpi_ticketvalidations`, `glpi_tickets` e `glpi_users`. A consulta usa `glpi_ticketvalidations.tickets_id` para localizar o chamado e `users_id_validate` para localizar o validador. O telefone é escolhido entre `mobile`, `phone` e `phone2`.

O workflow depende de `glpi_ticketvalidations.NOTIFICADO`. **Verifique se esse campo existe na sua instalação.** Ele pode ser uma customização local, não um campo nativo garantido do GLPI. Os estados usados são:

| Valor | Uso no workflow |
| --- | --- |
| `0` | Validação aguardando notificação |
| `1` | Validação marcada como notificada |
| `NULL` | Tratamento de validação sem telefone |

A credencial também precisa de permissão para atualizar `NOTIFICADO`. Antes de ativar o fluxo, valide a consulta, as permissões e o significado desses estados no seu ambiente. Observe o risco da atualização global descrito em [melhorias futuras](melhorias-futuras.md).
