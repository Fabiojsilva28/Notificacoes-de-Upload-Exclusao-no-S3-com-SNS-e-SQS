# Notificacoes-de-Upload-Exclusao-no-S3-com-SNS-e-SQS

### Este laboratório ensina como configurar notificações por e-mail (via SNS) e registro em fila (via SQS) para uploads e exclusões de arquivos em um bucket S3.
--- 
Você trabalha em uma empresa de mídia que armazena todos os seus arquivos de imagem e vídeo em um bucket S3 na AWS. Para fins de monitoramento, segurança e
auditoria, é necessário:

• Receber notificações por e-mail sempre que um novo arquivo for carregado (upload) ou um arquivo existente for excluído (delete) do bucket.

• Manter um registro (log) de todos esses eventos de upload e exclusão em uma fila SQS. Isso permitirá análises posteriores, relatórios e possíveis integrações com outras ferramentas de monitoramento. Seu desafio é configurar a infraestrutura necessária na AWS (usando S3, SNS e SQS) para implementar essa solução de notificação e registro de eventos.


---

### Tarefas:

Console S3: Acesse o console do S3.

<img width="1034" height="405" alt="Captura de tela 2025-10-28 225638" src="https://github.com/user-attachments/assets/485a7dd4-06ad-414a-a872-7aa322bab308" />

---

Clique em Criar bucket.

<img width="1684" height="498" alt="Captura de tela 2025-10-29 182056" src="https://github.com/user-attachments/assets/bacd4961-b291-4d6e-86ae-81f44d30a8a4" />

---

**Nome do bucket:** eventos-s3-seunome-data (ex: eventos-s3-robertasilva-20231028).

**Região da AWS:** Norte da Virgínia - us-east-1 (use a mesma para todos os recursos).

**Demais configurações:** Deixe tudo como padrão/desabilitado.

**Concluir:** Clique em Criar bucket.



<img width="1647" height="2126" alt="screencapture-us-east-1-console-aws-amazon-s3-bucket-create-2025-10-29-18_24_02" src="https://github.com/user-attachments/assets/34576fd8-d23d-46a4-accd-82e480b9318a" />
