# Notificacoes-de-Upload-Exclusao-no-S3-com-SNS-e-SQS

Este laboratório ensina como configurar notificações por e-mail (via SNS) e
registro em fila (via SQS) para uploads e exclusões de arquivos em um bucket S3.

Você trabalha em uma empresa de mídia que armazena todos os seus arquivos
de imagem e vídeo em um bucket S3 na AWS. Para fins de monitoramento, segurança e
auditoria, é necessário:

• Receber notificações por e-mail sempre que um novo arquivo for carregado (upload)
ou um arquivo existente for excluído (delete) do bucket.

• Manter um registro (log) de todos esses eventos de upload e exclusão em uma fila
SQS. Isso permitirá análises posteriores, relatórios e possíveis integrações com
outras ferramentas de monitoramento.
Seu desafio é configurar a infraestrutura necessária na AWS (usando S3, SNS e SQS) para
implementar essa solução de notificação e registro de eventos.
