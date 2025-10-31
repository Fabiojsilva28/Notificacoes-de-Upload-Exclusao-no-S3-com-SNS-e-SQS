# Notificacoes-de-Upload-Exclusao-no-S3-com-SNS-e-SQS

### Este laboratório ensina como configurar notificações por e-mail (via SNS) e registro em fila (via SQS) para uploads e exclusões de arquivos em um bucket S3.

--- 

Você trabalha em uma empresa de mídia que armazena todos os seus arquivos de imagem e vídeo em um bucket S3 na AWS. Para fins de monitoramento, segurança e auditoria, é necessário:

* Receber notificações por e-mail sempre que um novo arquivo for carregado (upload) ou um arquivo existente for excluído (delete) do bucket.

* Manter um registro (log) de todos esses eventos de upload e exclusão em uma fila SQS. Isso permitirá análises posteriores, relatórios e possíveis integrações com outras ferramentas de monitoramento. Seu desafio é configurar a infraestrutura necessária na AWS (usando S3, SNS e SQS) para implementar essa solução de notificação e registro de eventos.

---

### Tarefas:

* **Console S3:** Acesse o console do S3.

<img width="1020" height="359" alt="Captura de tela 2025-10-29 230815" src="https://github.com/user-attachments/assets/2f8ed576-72f1-403b-8cdd-69693bc08945" />

---

* **Clique em Criar bucket.**

<img width="1680" height="485" alt="Captura de tela 2025-10-29 231148" src="https://github.com/user-attachments/assets/92600694-b612-48b3-b569-f3f3c32c0d81" />

---

* **Nome do bucket:** eventos-s3-seunome-data (ex: eventos-s3-fabiosilva-20231028).

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

**Agora iremos Utilizar O SNS que irá enviar as notificações.**
* **Console SNS:** Acesse o console do SNS.

<img width="1011" height="355" alt="5" src="https://github.com/user-attachments/assets/ab4fe9c3-a727-49a3-8887-2b7fbf0b5ed0" />

---

**Criar Tópico:**

<img width="2238" height="464" alt="Captura de tela 2025-10-29 182905" src="https://github.com/user-attachments/assets/092624c3-ae07-43a0-bcf1-e4b40756e128" />

---

* **Tópicos -> Criar tópico.**
   * **Tipo:** Padrão.
   * **Nome:** notificacoes-s3-seunome-data.
   * **Política de acesso:** Básico (vamos modificar depois).
   * **Concluir:** Clique em Criar tópico.

<img width="1634" height="1261" alt="7" src="https://github.com/user-attachments/assets/b2743f8a-76e8-4d03-b08a-8363eff843fa" />

---

**Tópico Criado/Depois criando a assinatura no SNS**

* **Criar Assinatura de E-mail:**
   * No tópico, **Assinaturas -> Criar assinatura.**

<img width="6960" height="2493" alt="8" src="https://github.com/user-attachments/assets/22f3099c-9988-4947-acc9-901b49b754d9" />

**Copiar o ARN do Tópico (IMPORTANTE):** ``Copie o ARN do tópico.`` Para ser usado posteriormente.


---

   * **Protocolo:** E-mail.
   * **Endpoint:** Seu e-mail.
   * **Criar assinatura.**
   * **Confirmação Imediata:** Abra o e-mail da AWS e clique no link de confirmação.

<img width="2096" height="785" alt="9" src="https://github.com/user-attachments/assets/ac3a92fa-1cb2-4758-9cf3-323aaa5f9012" />

---

**Agora partiremos para a criação das filas que receberão os logs dos uploas e exclusões do bucket S3.** 

**Console SQS:** Acesse o console do SQS.

<img width="1013" height="365" alt="10" src="https://github.com/user-attachments/assets/6af76266-cd2e-429a-a7ab-334b572816d7" />

---

**Criar Fila:**
* **Criar fila.**

<img width="2090" height="557" alt="11" src="https://github.com/user-attachments/assets/58c292ad-6012-4502-957c-9da8ab15f39f" />

---

* **Tipo:** Fila padrão.

* **Nome:** fila-eventos-s3-seunome-data.

* **Política de acesso:** Básico (vamos modificar depois).

* **Concluir:** Clique em Criar fila.

<img width="1228" height="2427" alt="12" src="https://github.com/user-attachments/assets/86a00abb-5ab6-4482-87c7-003fb81fa68f" />

**Copiar o ARN da Fila (IMPORTANTE):** ``Copie o ARN da fila.``

---

## Agora, a parte crucial com os ARNs e a politica do SQS e habilitando que o S3 notifique uploads/exclusões no bucket.

---

## Política do Tópico SNS (S3 -> SNS):

* Console SNS -> Seu tópico -> **Política de acesso -> Editar.**
* **Substitua** a política pelo JSON abaixo:

 <img width="2226" height="937" alt="13" src="https://github.com/user-attachments/assets/cdde583d-9b2e-41e8-8fe9-ae6e7763c6b2" />

 ---
 
<img width="1639" height="1439" alt="14" src="https://github.com/user-attachments/assets/33fa7d71-6b10-48f4-9769-6164a25145f2" />

No campo Política de acesso substitua a politica JSON padrão por esta politica de acesso abaixo:

<img width="474" height="866" alt="Captura de tela 2025-10-31 182923" src="https://github.com/user-attachments/assets/75e1d625-45ae-402d-8278-97cf07d7336e" />

[Link do Código acima](https://docs.google.com/document/d/1XscPnvRc9z8_JK_TSPx7fQ-8aMm4Gk4Vj5xrfeay3BA/edit?usp=sharing)

**Onde Colar os ARNs (e o ID da Conta):**
* **"Resource":** "COLE AQUI O ARN DO SEU TÓPICO SNS": **Em ambos os lugares onde esta linha aparece, cole o ARN completo do seu tópico SNS.** 

* **"aws:SourceArn":** "COLE AQUI O ARN DO SEU BUCKET S3": **Cole o ARN completo do seu bucket S3.**

* **"AWS:SourceOwner":** "SEU ID DE CONTA DA AWS (12 DÍGITOS)": **Cole o seu ID de conta da AWS (12 dígitos). Você encontra o ID no canto superior direito do console.**

* Clique em **Salvar alterações.**

---

## Política da Fila SQS (SNS -> SQS)

Console SQS -> Sua fila -> **Política de acesso** -> **Editar.**

<img width="2244" height="1061" alt="15" src="https://github.com/user-attachments/assets/e0a8118b-5733-4820-a70e-e06811c0c951" />

* **Substitua** a política pelo JSON abaixo:

<img width="447" height="709" alt="Captura de tela 2025-10-31 183221" src="https://github.com/user-attachments/assets/1e3e5906-b9b9-4c01-901f-1a1b6761771c" />

[Link do Código acima](https://docs.google.com/document/d/1p9Duh_wXL3imZFsG6IGDyCjAvmPhhw3xGJEfYf70wvM/edit?usp=sharing)

* **Onde Colar os ARNs:**
   * **"Resource":** "COLE AQUI O ARN DA SUA FILA SQS": **Cole o ARN da sua fila SQS.**
   * **"aws:SourceArn":** "COLE AQUI O ARN DO SEU TÓPICO SNS": **Cole o ARN do seu tópico SNS.**
* Clique em **Salvar alterações.**

---

* Console S3 -> Seu bucket -> Propriedades -> Notificações de eventos -> Criar notificação de evento.
<img width="2336" height="612" alt="16 0" src="https://github.com/user-attachments/assets/eacabd17-dacc-41c1-baf9-42ef473adc30" />

<img width="2224" height="738" alt="16 1" src="https://github.com/user-attachments/assets/085f02fc-bb31-4319-9688-3af724ac1b50" />


* **Configuração:**
   * **Nome:** NotificarPutDelete.
   * **Tipos de eventos:** Marque as caixinhas:
      * Todos os eventos de criação de objeto (s3:ObjectCreated:*)
      * Todos os eventos de remoção de objetos (s3:ObjectRemoved:*)
   * **Destino:** **Tópico do SNS** -> **Tópico do SNS, na sua lista...** -> Selecione o seu tópico.

* **Salvar.**

---

**Console SNS** -> **Seu tópico** -> **Assinaturas** -> **Criar assinatura.**
* **Configuração:**
   * **Protocolo:** Amazon SQS.
   * **Endpoint:** ARN completo da sua fila SQS.
   * **Habilitar conteúdo de mensagem bruta:** Marque.
* **Criar**

---

### Nesse campo algumas etapas precisarão ser seguidas para testar a funcionalidade do projeto:

* **Upload:** No S3, carregue um arquivo.
* **Email:** Verifique o e-mail.
* **Fila SQS:** Pesquise mensagens na fila (deve ter o JSON).
* **Exclusão:** No S3, exclua o arquivo.
* **Email e Fila:** Verifique novamente.
* **Sem E-mail:** Confirmação, spam, filtros, provedor, raw message delivery (SQS), política do SNS, região.
* **Sem Mensagem na Fila:** Raw message delivery, política da fila, política do tópico, eventos no S3, região.


