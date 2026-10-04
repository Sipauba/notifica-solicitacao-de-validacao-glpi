# Arquitetura

O **n8n** orquestra a execução e mantém as credenciais. O **Schedule Trigger** inicia o workflow a cada minuto. O **MySQL / GLPI** fornece os dados das validações, chamados e usuários. Um nó **IF** separa registros pelo preenchimento do telefone. O **Code node** normaliza o número brasileiro. O **HTTP Request** envia a mensagem à API de WhatsApp. Por fim, nós MySQL atualizam o estado da validação.

O diagrama está no [README](../README.md) e a representação visual em [assets/fluxo-workflow.svg](../assets/fluxo-workflow.svg).

A integração é direta entre n8n, banco MySQL e API HTTP. O JSON exportado contém a lógica do fluxo, mas não contém as credenciais operacionais. Após importá-lo, associe credenciais próprias no n8n e configure os endereços para o seu ambiente.
