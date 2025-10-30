# Notificacoes-de-Upload-Exclusao-no-S3-com-SNS-e-SQS

### Este laboratório ensina como configurar notificações por e-mail (via SNS) e registro em fila (via SQS) para uploads e exclusões de arquivos em um bucket S3.
--- 
Você trabalha em uma empresa de mídia que armazena todos os seus arquivos de imagem e vídeo em um bucket S3 na AWS. Para fins de monitoramento, segurança e auditoria, é necessário:

* Receber notificações por e-mail sempre que um novo arquivo for carregado (upload) ou um arquivo existente for excluído (delete) do bucket.

* Manter um registro (log) de todos esses eventos de upload e exclusão em uma fila SQS. Isso permitirá análises posteriores, relatórios e possíveis integrações com outras ferramentas de monitoramento. Seu desafio é configurar a infraestrutura necessária na AWS (usando S3, SNS e SQS) para implementar essa solução de notificação e registro de eventos.

---

### Tarefas:

* Console S3: Acesse o console do S3.

<img width="1020" height="359" alt="Captura de tela 2025-10-29 230815" src="https://github.com/user-attachments/assets/2f8ed576-72f1-403b-8cdd-69693bc08945" />

---

* Clique em Criar bucket.

<img width="1680" height="485" alt="Captura de tela 2025-10-29 231148" src="https://github.com/user-attachments/assets/92600694-b612-48b3-b569-f3f3c32c0d81" />

---

* **Nome do bucket:** eventos-s3-seunome-data (ex: eventos-s3-robertasilva-20231028).

* **Região da AWS:** Norte da Virgínia - us-east-1 (use a mesma para todos os recursos).

* **Demais configurações:** Deixe tudo como padrão/desabilitado.

* **Concluir:** Clique em Criar bucket.

<img width="1647" height="2126" alt="screencapture-us-east-1-console-aws-amazon-s3-bucket-create-2025-10-29-18_24_02" src="https://github.com/user-attachments/assets/9e259d14-d05e-404a-bcb9-b0d6b802d49d" />

Imagem da Bucket criada:

<img width="2235" height="491" alt="Captura de tela 2025-10-29 182803" src="https://github.com/user-attachments/assets/afda967e-47e0-4042-a87d-4688cc40e164" />

---

**Copiar o ARN do Bucket (IMPORTANTE):**

* Vá para a página de detalhes do bucket.

* Aba **Propriedades** -> ``Copie o ARN do bucket.``

Arn este que será utilizado posteriormente para fazer as amarrações.

---

Agora iremos Utilizar O SNS que irá enviar as notificações.
* **Console SNS:** Acesse o console do SNS.

<img width="1011" height="355" alt="5" src="https://github.com/user-attachments/assets/ab4fe9c3-a727-49a3-8887-2b7fbf0b5ed0" />

---
**Criar Tópico:**

<img width="2238" height="464" alt="Captura de tela 2025-10-29 182905" src="https://github.com/user-attachments/assets/092624c3-ae07-43a0-bcf1-e4b40756e128" />

---

* Tópicos -> Criar tópico.
   * **Tipo:** Padrão.
   * **Nome:** notificacoes-s3-seunome-data.
   * **Política de acesso:** Básico (vamos modificar depois).
   * **Concluir:** Clique em Criar tópico.

<img width="1634" height="1261" alt="7" src="https://github.com/user-attachments/assets/b2743f8a-76e8-4d03-b08a-8363eff843fa" />

---
**Tópico Criado**

<img width="6960" height="2493" alt="8" src="https://github.com/user-attachments/assets/22f3099c-9988-4947-acc9-901b49b754d9" />

**Copiar o ARN do Tópico (IMPORTANTE):** ``Copie o ARN do tópico.`` Para ser usado posteriormente.


---

* **Criar Assinatura de E-mail:**
   * No tópico, **Assinaturas -> Criar assinatura.**
   * **Protocolo:** E-mail.
   * **Endpoint:** Seu e-mail.
   * **Criar assinatura.**
   * **Confirmação Imediata:** Abra o e-mail da AWS e clique no link de confirmação.


  
<img width="2096" height="785" alt="9" src="https://github.com/user-attachments/assets/ac3a92fa-1cb2-4758-9cf3-323aaa5f9012" />
