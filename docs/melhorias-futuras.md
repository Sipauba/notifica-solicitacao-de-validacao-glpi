# Melhorias futuras

Estas ideias **não foram implementadas** nesta versão; a lógica original foi preservada.

1. **Atualizar apenas a validação atual.** O SQL atual, `UPDATE glpi_ticketvalidations SET NOTIFICADO = 1 WHERE NOTIFICADO = 0`, é global. Pode marcar como notificadas validações que não receberam mensagem. Uma futura versão poderia usar `WHERE id = <validacao_id>`, com parâmetros seguros e validação do identificador.
2. **Validar antes do HTTP Request.** O IF atual verifica apenas se `telefone_validador` não está vazio. Inserir uma condição `telefone_valido = true` após a formatação evitaria tentar enviar números inválidos.
3. **Tratar falhas da API.** Configurar retry, timeout, tratamento de erros HTTP e registro de falhas.
4. **Marcar após confirmação.** Fazer `NOTIFICADO` refletir o resultado confirmado do envio; avaliar também resposta da API e falhas parciais.
5. **Criar histórico de notificações.** Registrar `validacao_id`, data, telefone com proteção adequada, status do envio e erro.
6. **Parametrizar o agendamento.** Permitir ajuste da frequência conforme volume e limites da API.
7. **Adicionar observabilidade.** Monitorar taxas de envio, falha e filas de pendências.
8. **Usar logs estruturados.** Correlacionar execução e validação sem expor dados pessoais.
9. **Evitar envio repetido.** Considerar concorrência, reexecuções e idempotência.
10. **Parametrizar por variáveis de ambiente.** Configurar URLs e instância sem editar manualmente o workflow importado.
