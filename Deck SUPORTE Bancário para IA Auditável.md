

### **Parte 1: O Paradoxo Regulatório e a Tese da Prova Determinística**

*Esta seção estabelece o problema central (Slide 2 do deck) e a tese da solução (Slide 3), introduzindo a defensibilidade da arquitetura canônica Veritas 2.0.*

#### **I. O Problema do Banco: O Paradoxo da Inovação em IA no Brasil**

A adoção de Inteligência Artificial (IA) sobre dados sensíveis em instituições financeiras de Nível 1 está paralisada por um conflito legal e arquitetônico: o Paradoxo Regulatório.1

Este paradoxo é definido por dois conjuntos de mandatos regulatórios irreconciliáveis:

1. **O Imperativo de Retenção (SOX / BACEN / CVM):** A legislação exige a retenção absoluta e imutável de registros de auditoria por longos períodos (7-10 anos).1 A Resolução CMN n° 4.893 do BACEN (Art. 14\) e a Res. CVM 35/21 exigem "mecanismos de rastreabilidade" e acesso irrestrito do supervisor aos logs.1 A implicação legal é: **NUNCA EXCLUIR**.1  
2. **O Imperativo de Privacidade (LGPD / GDPR):** A legislação exige o controle e a exclusão de dados pessoais (PII) sob demanda, através do "Direito de Ser Esquecido".1 O Artigo 46 da LGPD codifica o *Privacy by Design* e a "minimização de dados".1 A implicação legal é: **EXCLUIR SOB DEMANDA**.

A IA Generativa agrava este conflito. Os *logs* de *prompts* e respostas de modelos (ex: Gemini) contêm PII e dados sensíveis. Reter esses *logs* para auditoria do BACEN cria um "honeypot" tóxico que viola a LGPD. Excluir esses *logs* para cumprir a LGPD viola o mandato de retenção do BACEN.2

Este conflito não é operacional; é arquitetônico. Um sistema de dados não pode, nativamente, ser "imutável" e "deletável" ao mesmo tempo.

#### **II. As Falhas Fatais das Arquiteturas Incumbentes**

As tentativas de resolver este paradoxo com arquiteturas legadas falham em dois níveis:

1. **Risco 1: SaaS Multi-Tenant (Rejeição do Slide 2):** O modelo SaaS *multi-tenant* é um não-início para dados *core* de bancos Tier-1. Ele falha em garantir a soberania do perímetro, introduz risco de *data-bleed* (vazamento entre *tenants*) e não atende aos requisitos de controle e auditoria da Res. BACEN 4.893.2  
2. **Risco 2: A Falha da "Tese 1.0" (Hashing de PII):** Uma tentativa ingênua de "anonimizar" *logs* de auditoria através do *hashing* de PII (ex: CPF) é arquitetonicamente falha e legalmente indefensável, como identificado em *due diligence* técnica e jurídica.1  
   * **Violação de Privacidade (FTC/LGPD):** O *hashing* de dados com espaço de entrada finito (como CPF, datas de nascimento ou números de conta) é trivialmente reversível através de um "ataque de *rainbow table*".1 Reguladores (incluindo a FTC dos EUA) são explícitos: "Hashing não é anonimização".1 O *hash* de PII ainda é considerado PII e um passivo tóxico.  
   * **Violação de Auditoria (SOX/BACEN):** O *hash* do *input* é inútil para um auditor. O regulador precisa do *input* original (os dados brutos) para re-executar a lógica de negócios e verificar independentemente a computação e a validade da decisão.1 O processamento de PII em RAM (Zero-Persistence) neste contexto foi corretamente avaliado como "destruição de evidências como serviço", uma violação direta dos mandatos de retenção.1

Esta arquitetura "Tese 1.0" é, portanto, "morta à nascença" (*Dead-on-Arrival*).1 Ela simultaneamente "destrói evidências (violando SOX/BACEN) e falha em proteger a privacidade (violando LGPD/FTC)".1 Este relatório apresenta exclusivamente a "Tese 2.0 Canônica", a única arquitetura defensável.

#### **III. A Tese da FoundLab: O Orquestrador de Confiança Não-Custodial (Análise do Slide 3\)**

A tese central da FoundLab é baseada em um silogismo rigoroso: a IA é probabilística, mas a auditoria regulatória exige prova determinística.2 Portanto, toda chamada de IA que toca em dado sensível deve ser "envelopada" por uma prova criptográfica determinística.

Isto é alcançado através do pivô da "Tese 1.0" para a "Tese 2.0".1

* **O Pivô para Não-Custodial:** O princípio central da Tese 2.0 é **"PII Nunca Toca a Infraestrutura"**.1 A plataforma FoundLab migra de um "Processador Efêmero de PII" (Tese 1.0) para um **"Orquestrador de Confiança Não-Custodial" (Tese 2.0)**.1  
* **Mecanismo:** A plataforma não ingere, armazena ou faz *hash* de PII. Ela atua como um **verificador de provas criptográficas** (tecnicamente, W3C Verifiable Credentials \- VCs).1  
* **Componentes da Tese (Slide 3):**  
  * **Umbrella:** O Orquestrador Cognitivo, a "Fábrica de Decisão" que executa o RAG (Retrieval-Augmented Generation).3  
  * **Veritas 2.0:** O Cartório Técnico, a "Camada de Prova" Não-Custodial que verifica as provas e gera o registro de auditoria imutável (o *Decision Evidence Object* \- DEO).1  
* **Defensibilidade da Tese 2.0:** Esta arquitetura Não-Custodial é a única legalmente defensável, pois contorna o Paradoxo Regulatório:  
  1. **LGPD:** A FoundLab não viola a LGPD, pois não armazena PII ou *PII-hash*.  
  2. **BACEN/SOX:** A FoundLab não viola a retenção, pois a obrigação de reter o PII original permanece com o "Emissor" da prova (o próprio BTG). A FoundLab retém apenas a *prova da verificação*, que é o ativo de auditoria, no *ledger* WORM.1

---

### **Parte 2: Arquitetura da Solução e Mecânica da Prova**

*Esta seção detalha o "como" dos Slides 4, 6 e 7, focando na mecânica de engenharia da prova criptográfica.*

#### **IV. O Fluxo de Decisão Auditável (Análise do Slide 4\)**

O fluxo de 6 passos (RAG Institucionalizado) descreve como a IA pode ser usada com segurança sobre dados operacionais sensíveis.3

1. **Usuário Pede:** Um usuário interno (ex: Assessor do Private Bank) faz uma pergunta (ex: "simular carteira para cliente X").6 A plataforma gera imediatamente um **DecisionID** único para a transação, iniciando formalmente a trilha de auditoria.3  
2. **IAM (Umbrella):** O Orquestrador Umbrella intercepta a consulta, autentica o usuário e aplica as políticas de IAM (Identity and Access Management) e RBAC (Role-Based Access Control) do BTG para definir "quem pode perguntar o quê".3  
3. **RAG Interno (Umbrella):** O Umbrella executa o RAG, buscando dados *apenas* de fontes internas autorizadas e vetadas pelo BTG (ex: Core Banking, bases de clientes).3 O contexto é 100% definido e controlado pelo banco.3  
4. **IA Responde (Modelo):** O *prompt* aumentado (pergunta do usuário \+ contexto interno do RAG) é enviado ao modelo de IA (ex: Gemini ou modelo do banco). A IA gera a resposta e uma *Rationale* (justificativa em linguagem natural, para Explicabilidade \- XAI).3  
5. **Veritas Registra:** O Protocolo Veritas Logger captura a transação completa como metadados: o DecisionID, a identidade do usuário, a política aplicada, a versão do modelo usada, a *Rationale* e os *hashes* da prova.3 O evento é "selado" criptograficamente com um chainHash e encadeado ao previousChainHash, provando a integridade sequencial (Hash-chaining).3  
6. **BigQuery WORM do BTG:** O registro de auditoria final (o *Decision Evidence Object* \- DEO), que não contém PII, é persistido de forma imutável no *ledger* WORM (BigQuery) dentro do projeto GCP do próprio BTG.3

#### **V. Veritas 2.0: O Cartório Técnico e os 3 Pilares da Conformidade Defensável (Análise do Slide 6\)**

O "segredo" da solução para o Paradoxo Regulatório (Reter vs. Esquecer) é um **Desacoplamento Físico-Criptográfico**.1 A plataforma desacopla a *existência física* do registro de auditoria de sua *legibilidade criptográfica*.

Isso é implementado através dos Três Pilares da Conformidade Defensável do Veritas 2.0 1:

* **Pilar 1: Imutabilidade Física (Resolvendo SOX/BACEN).**  
  * **Mecanismo:** O *ledger* de auditoria (os metadados DEO) é escrito no **Google BigQuery**.3  
  * **Defensibilidade:** O *dataset* do BigQuery é configurado em modo **WORM (Write-Once, Read-Many)**. Isso é aplicado no nível da infraestrutura através de permissões **IAM Append-Only** (somente inserção) e deletion\_protection=true, proibindo explicitamente UPDATE ou DELETE.1  
  * **Arquitetura Hot/Cold Path:** Para uma defensibilidade de nível SEC/SOX, a arquitetura é híbrida. O BigQuery serve como o "Hot Path" para análise em tempo real. O "Cold Path" (a prova WORM de nível regulatório) é alcançado pela exportação periódica dos *logs* para um **GCS Bucket Lock**, que é a solução WORM do Google validada por auditores independentes (Cohasset Associates) para a Regra 17a-4 da SEC.4 Isso garante a retenção física imutável por 7-10 anos.  
* **Pilar 2: Veracidade Criptográfica (Resolvendo FTC/LGPD Hashing).**  
  * **Mecanismo:** O *ledger* WORM (Pilar 1\) **não armazena PII ou PII-hash**.  
  * **Defensibilidade:** Ele armazena o **PresentationHash** (o *hash* da *prova* criptográfica que foi verificada) e o issuer\_did (o identificador criptográfico do emissor, ex: did:web:btg.com).1  
  * **Resultado:** O *ledger* contém uma prova irrefutável da transação de verificação, eliminando o passivo de privacidade (PII) e resolvendo a falha fatal da Tese 1.0.1  
* **Pilar 3: Desacoplamento Criptográfico (Resolvendo LGPD Direito de Esquecer).**  
  * **Mecanismo:** A arquitetura utiliza **Customer-Managed Encryption Keys (CMEK)**, controladas 100% pelo BTG no Google Cloud KMS ou Cloud HSM (com certificação FIPS 140-2 Nível 3).1  
  * **Defensibilidade (O "Kill Switch"):** Quando o BTG recebe uma solicitação de exclusão (Direito de Ser Esquecido da LGPD), ele não tenta deletar o dado do WORM (o que é impossível e ilegal sob SOX). Em vez disso, o BTG executa o **"Crypto-Shredding"**: a **destruição da chave CMEK** associada àquele dado.1  
  * **Resultado:** O *blob* de dados cifrado permanece fisicamente no *ledger* WORM (cumprindo SOX/BACEN), mas torna-se "lixo" criptográfico permanentemente ilegível e irrecuperável (cumprindo LGPD).1 Esta é a única arquitetura de engenharia que resolve o conflito jurídico.

A tabela a seguir resume a resolução do Paradoxo Regulatório:

| Mandato Legal | Requisito Contraditório | Solução Veritas 2.0 | Mecanismo Técnico |
| :---- | :---- | :---- | :---- |
| **SOX / BACEN 4.893** | Nunca Excluir Registros (Retenção WORM) | Imutabilidade Física (**Pilar 1**) | BigQuery WORM (com IAM Append-Only) \+ GCS Bucket Lock (Cold Path) |
| **FTC / LGPD (Hashing)** | Hashing Não é Anonimização (Risco de Rainbow Table) | Veracidade Criptográfica (**Pilar 2**) | Armazena PresentationHash (hash da prova), **não** PII-hash. |
| **LGPD (Exclusão)** | Excluir PII Sob Demanda (Direito de Ser Esquecido) | Desacoplamento Criptográfico (**Pilar 3**) | **Crypto-Shredding** (Destruição da chave CMEK/HSM pelo BTG). |

---

### **Parte 3: Arquitetura de Segurança e Soberania de Dados (BTG Perímetro)**

*Esta seção detalha a arquitetura de deployment (Slide 5\) e a segurança de dados (Slide 7), respondendo diretamente à objeção "SaaS multi-tenant \= não".*

#### **VI. A Trindade da Confiança: Soberania Absoluta no Perímetro do BTG (Análise do Slide 5\)**

A plataforma não é um SaaS. É um software entregue como uma instância *single-tenant* (Dedicada) implantada diretamente no perímetro do banco.

* **O Modelo "Dedicated (VPC do Cliente)":** A plataforma é entregue como **Infrastructure as Code (IaC)** (usando Terraform/Terragrunt) e implantada inteiramente dentro da VPC e do projeto Google Cloud (GCP) do BTG.1 O BTG retém 100% de soberania sobre a infraestrutura e os dados.  
* A "Trindade da Confiança" 2 garante esta soberania:  
  1. **Pilar 1: Soberania de Perímetro (VPC Service Controls \- VPC-SC).**  
     * **Mecanismo:** O BTG aplica o VPC-SC 1 em torno do projeto.  
     * **Função:** Atua como o "muro do castelo" ou "firewall para as APIs do Google". Ele **bloqueia arquitetonicamente todo o egresso de dados** para fora do perímetro aprovado, mitigando o risco de exfiltração de dados, mesmo em caso de credenciais comprometidas.1  
  2. **Pilar 2: Soberania de Chaves (CMEK / Cloud HSM).**  
     * **Mecanismo:** O BTG mantém 100% de custódia das chaves de criptografia no Cloud KMS.2  
     * **Função:** Habilita o **Pilar 3 do Veritas (Crypto-Shredding)**.1 O "kill switch" regulatório está na mão do BTG, não da FoundLab.  
  3. **Pilar 3: Soberania de Auditoria (Logs no Projeto do Banco).**  
     * **Mecanismo:** O *ledger* WORM (BigQuery/GCS) reside fisicamente no projeto GCP de propriedade do BTG.1  
     * **Função:** Atende diretamente ao **Art. 14 da Res. BACEN 4.893**.1 O BTG pode conceder acesso de auditoria ao BACEN *diretamente* ao seu próprio *ledger*, eliminando a FoundLab como um intermediário de acesso.1

#### **VII. O Princípio da Minimização de Dados: Zero-Persistence (Análise do Slide 7\)**

"Zero-Persistence" (ZPA) não é um produto, mas o princípio de segurança fundamental que rege os componentes da Tese 2.0.6 É a implementação técnica rigorosa do princípio de "minimização de dados" exigido pelo Art. 46 da LGPD.3

* **Mecanismo:** Dados sensíveis (PII, dados financeiros) existem **apenas em memória volátil (RAM)** de contêineres efêmeros e *stateless* (ex: Google Cloud Run).2 No instante em que a transação é concluída (milissegundos), a instância e sua RAM são destruídas.3  
* Fluxo de Dados Volátil vs. Prova Persistente 6: A arquitetura impõe uma separação rigorosa de fluxos:  
  * **Fluxo Volátil (PII):** Ingestão \-\> Processamento em RAM \-\> Descarte. O PII nunca toca o disco (*data-at-rest*), eliminando o risco de vazamento de banco de dados.2  
  * **Fluxo Persistente (Prova):** Decisão Gerada \-\> Metadados (DEO, sem PII) \-\> Veritas Registra \-\> BigQuery WORM.  
* **Defensibilidade (Tese 2.0):** Na Tese 2.0, o ZPA *não* é "destruição de evidência" (a falha da Tese 1.0).1 Isso porque o *ativo de prova* (o DEO ou a VC) *é* persistido no WORM.1 O ZPA aplica-se apenas ao PII bruto, que a arquitetura Não-Custodial Tese 2.0 foi projetada para *nunca* ter como custódia.1 Esta arquitetura satisfaz a LGPD (minimizando PII) e o BACEN (retendo a prova) simultaneamente.4

---

### **Parte 4: Aplicação, Conformidade e Aceleração**

*Esta seção finaliza o due diligence conectando a arquitetura aos resultados de negócios (Slides 8, 9, 10).*

#### **VIII. Mapeamento de Conformidade Regulatória Explícita (Análise do Slide 9\)**

A arquitetura "Dedicated/VPC" (Trindade da Confiança) e a "Camada de Prova" (3 Pilares do Veritas) fornecem conformidade "por design":

* Resolução BACEN CMN nº 4.893/2021 1:  
  * **Art. 11, 12, 13 (Controle e Supervisão):** Atendidos pelo modelo "Dedicated (VPC do Cliente)", onde o BTG mantém controle soberano sobre a infraestrutura (IaC) e os *logs*.1  
  * **Art. 14 (Acesso do Supervisor):** Atendido pela "Soberania de Auditoria". O BTG concede acesso ao BACEN diretamente ao seu próprio BigQuery WORM.1  
* CVM Res. 35/21 (Controles Internos e Rastreabilidade) 3:  
  * **Rastreabilidade:** Atendida pelo Protocolo Veritas, que fornece o *ledger* imutável (WORM) e o *hash-chaining* para a reconstrução determinística de qualquer decisão.3  
  * **Não-Repúdio:** Atendido pela entrega do artefato de decisão final como uma JSON Web Signature (JWS) assinada, garantindo autenticidade e integridade.3  
* LGPD 1:  
  * **Art. 46 (Minimização de Dados):** Atendido pelo princípio "Zero-Persistence" (PII apenas em RAM).3  
  * **Direito de Ser Esquecido:** Atendido pelo "Pilar 3: Desacoplamento Criptográfico" (Crypto-Shredding via CMEK).1

#### **IX. Casos de Uso Imediatos para o BTG (Análise do Slide 8\)**

A arquitetura desbloqueia imediatamente dois casos de uso de alto valor:

* **Caso de Uso 1: Onboarding/KYC Automatizado ("Alfa Operacional").**  
  * **Demonstra:** Umbrella (RAG) \+ Veritas (Prova).  
  * **Mecânica:** O Umbrella orquestra a IA (ex: Google Document AI) para fazer o *parsing* de documentos complexos de Onboarding PJ (contratos sociais, balanços, etc.).2  
  * **Resultado (Métrica de ROI\_E):** A automação de processos manuais de alta latência reduz o tempo de ciclo de **21 horas para 16 minutos**.1 O Veritas gera um DEO/VC imutável (ex: "Score Risco KYC: 85, Decisão: APROVADO, Base: Docs A, B, C") 2, fornecendo a prova de diligência para o BACEN.  
* **Caso de Uso 2: "BTG GPT" Interno Auditável (IA Generativa Segura).**  
  * **Demonstra:** Zero-Persistence \+ Veritas (Prova de Ação).  
  * **Mecânica:** Um assessor do Private Bank usa um "BTG GPT" interno (ancorado pelo RAG do Umbrella) para perguntar sobre a carteira de um cliente.2  
  * **Arquitetura de Segurança Dupla:**  
    * **LGPD (Zero-Persistence):** A consulta (PII) e a resposta (PII) existem *apenas* em memória volátil (RAM) e são purgadam.2 O PII *não* é registrado pelo provedor de modelo nem no *ledger* WORM. O risco de vazamento de PII para o provedor de IA é eliminado.  
    * **CVM/BACEN (Veritas):** O Veritas *não* registra o PII (a conversa). Ele registra o *metadado da ação*: "Assessor solicitou simulação para Cliente às, usando Política \[Versão\]".2  
  * **Resultado:** O BTG obtém o "Alfa de Inovação" da IA generativa sobre dados de clientes, sem o risco de vazamento de PII, e mantendo uma trilha de auditoria completa da *ação* do assessor, em conformidade com a CVM/BACEN.

#### **X. Plano de Aceleração: A Prova de Conceito (PoC) de 15 Dias (Análise do Slide 10\)**

O objetivo do PoC é tático e focado: gerar o primeiro DecisionID no BigQuery WORM do BTG, provando a viabilidade da arquitetura e o cumprimento da conformidade em três *sprints* de 5 dias.

* **Dias 1-2: Arquitetura e Provisionamento.**  
  * **Ação:** Sessão de Arquitetura de Nuvem (BTG+FoundLab).  
  * **Pedido (CTA):** Liberação pelo BTG de um **projeto GCP *sandbox*** com IAM mínimo e permissões para provisionar BigQuery, GCS, Cloud Run e KMS.  
* **Dias 3-5: Deploy da Infra (IaC).**  
  * **Ação:** FoundLab (via pipeline de CI/CD do banco) executa o **IaC (Terraform)** para implantar as instâncias *single-tenant* do Umbrella e do Veritas 2.0 Ledger, incluindo as políticas WORM/IAM no BigQuery/GCS.  
* **Dias 6-9: Conexão da Fonte.**  
  * **Ação:** Conectar o Orquestrador Umbrella a **uma (1)** fonte de dados interna (ex: API de *mock* de Onboarding ou Suitability). Configurar o RAG para esta única fonte.  
* **Dias 10-12: Geração da Primeira Prova.**  
  * **Ação:** Executar a primeira transação *end-to-end*. (Ex: Submeter um documento de Onboarding).  
  * **Resultado:** O **primeiro DecisionID (DEO)** é gerado e escrito com sucesso no *dataset* BigQuery WORM, dentro do projeto *sandbox* do BTG.  
* **Dias 13-15: Demo de Auditoria (O Momento de Validação).**  
  * **Ação:** Sessão de demonstração para os times de Risco e Compliance do BTG.  
  * **Demonstração:**  
    1. Mostrar a transação no sistema de origem (ex: "Onboarding Submetido").  
    2. Mostrar o DecisionID correspondente no *dataset* BigQuery WORM *dentro do projeto GCP do BTG*.  
    3. *Teste de Imutabilidade:* Tentar executar um DELETE ou UPDATE no registro e demonstrar a falha (provando o WORM).  
    4. *Teste de Exclusão (Opcional):* Executar o "Crypto-Shredding" (destruir a chave CMEK) e demonstrar o registro tornando-se "lixo" criptográfico ilegível.

O *Call to Action* (CTA) para a reunião executiva (Slide 12\) é a solicitação direta para iniciar este plano de 15 dias: **"Liberar projeto sandbox \+ IAM mínimo hoje → entregamos primeira prova em até 15 dias."**

#### **Referências citadas**

1. FoundLab Veritas 2.0: Infraestrutura Bancária, [https://drive.google.com/open?id=1HQyXZF3gxJ-x7ywJ4XGfWtwZvJdwqfhfBXgNBhjpHk0](https://drive.google.com/open?id=1HQyXZF3gxJ-x7ywJ4XGfWtwZvJdwqfhfBXgNBhjpHk0)  
2. FoundLab: Infraestrutura de Confiança para IA, [https://drive.google.com/open?id=1N7oSZaKYHEZGmRFD4ucA1GVKH9nNvfwjZEBy9G7IG2w](https://drive.google.com/open?id=1N7oSZaKYHEZGmRFD4ucA1GVKH9nNvfwjZEBy9G7IG2w)  
3. doc, [https://drive.google.com/open?id=1Hx\_O4CgDQDBOdWOyjimbVbiExq1XxLhBLTl4TDFvS0Y](https://drive.google.com/open?id=1Hx_O4CgDQDBOdWOyjimbVbiExq1XxLhBLTl4TDFvS0Y)  
4. Whitepaper Veritas 2.0: Arquitetura de Confiança, [https://drive.google.com/open?id=1BYRIHQ7L1MIGRGnlIg8M7jR2B6eQHnQBph3KMqyQH8o](https://drive.google.com/open?id=1BYRIHQ7L1MIGRGnlIg8M7jR2B6eQHnQBph3KMqyQH8o)  
5. Whitepaper Veritas 2.0: Arquitetura de Confiança, [https://drive.google.com/open?id=1IHFpY5Lw\_Yn95AgftxUoOSbL1zDX3xUw9S8BHusogOY](https://drive.google.com/open?id=1IHFpY5Lw_Yn95AgftxUoOSbL1zDX3xUw9S8BHusogOY)  
6. Estrutura de Confiança para IA Bancária, [https://drive.google.com/open?id=1CnzPQ8zXVTveO-skkJP1xuiK9cmitoSkLeLpfuNpZR4](https://drive.google.com/open?id=1CnzPQ8zXVTveO-skkJP1xuiK9cmitoSkLeLpfuNpZR4)  
7. Whitepaper Veritas 2.0: Arquitetura de Confiança, [https://drive.google.com/open?id=12SoYOGzGcgS102ixFVoQkbi6tQEB3-exyFap3eJu37M](https://drive.google.com/open?id=12SoYOGzGcgS102ixFVoQkbi6tQEB3-exyFap3eJu37M)