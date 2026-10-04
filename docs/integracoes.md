# Integrações

## MySQL / GLPI

Três nós MySQL usam uma credencial armazenada no n8n: um consulta validações pendentes; outro altera `NOTIFICADO` após o envio; o terceiro trata a ausência de telefone. A cópia pública contém somente uma referência de credencial mascarada. Associe a credencial correta após a importação.

## API de WhatsApp

O nó HTTP Request envia `POST` a `https://xxxxxxxxxxxxxxxxxxxx/message/sendText/xxxxxxxxxxxxxxxxxxxx`, com autenticação `httpHeaderAuth`. O corpo contém `number`, vindo de `telefone_formatado`, e `text`, com dados do chamado e link para o GLPI. Configure a URL da API, o nome da instância e a credencial de cabeçalho apenas na sua instância do n8n.

## Endereço do chamado

A mensagem usa o formato `https://xxxxxxxxxxxxxxxxxxxx/front/ticket.form.php?id={{ $json.numero_chamado }}`. Substitua o domínio mascarado pelo endereço base correto do GLPI na configuração privada do workflow. O [.env.example](../.env.example) é uma referência de configuração; o JSON atual não faz leitura automática desse arquivo.
