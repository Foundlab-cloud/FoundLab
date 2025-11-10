

# **Proposta de Parceria Estratégica: A Infraestrutura de Confiança Auditável para a Próxima Geração de IA do BTG Pactual**

**Subtítulo:** A Arquitetura Canônica Veritas 2.0: De Probabilístico para Determinístico

---

## **PARTE 1: O IMPERATIVO ESTRATÉGICO (O "PORQUÊ")**

Esta seção estabelece o problema central. Ela é projetada para criar um senso de urgência e alinhar-se com as preocupações primárias do C-Level e das equipes de Risco e Jurídico. O objetivo é demonstrar que a inovação em IA, uma prioridade estratégica para o BTG, está fundamentalmente bloqueada por um problema de infraestrutura que as soluções atuais não podem resolver.

### **1.1. O Paradoxo Regulatório da IA: A Inovação Bloqueada**

O setor financeiro institucional enfrenta um paradoxo. Por um lado, a Inteligência Artificial Generativa (IA Gen) representa a maior alavanca de eficiência e personalização em décadas, prometendo revolucionar desde o Private Banking até a análise de risco.1 Instituições Tier 1, como o BTG Pactual, desejam aplicar IA sobre seus dados operacionais proprietários — como posições de carteira de clientes de Private Bank — pois reconhecem que modelos genéricos não geram "alfa".1

Por outro lado, essa inovação está paralisada por uma crise de infraestrutura de confiança.1 A arquitetura de segurança legada é incapaz de suportar a adoção segura da IA. O obstáculo central é um conflito legal irreconciliável 2:

1. **O Imperativo de Retenção (SOX, BACEN Res. 4.893, CVM):** O mandato regulatório para "Nunca Excluir" registros de auditoria. A Sarbanes-Oxley (SOX) e as resoluções do Banco Central exigem a retenção de trilhas de auditoria por 7 a 10 anos, em formato WORM (Write-Once, Read-Many), para garantir a imutabilidade.2  
2. **O Imperativo de Privacidade (LGPD, GDPR):** O mandato legal para "Excluir Sob Demanda". A Lei Geral de Proteção de Dados (LGPD) impõe o "Direito ao Esquecimento", exigindo a exclusão auditável de Informações de Identificação Pessoal (PII).2

A IA Generativa agrava este conflito. A IA é inerentemente *probabilística* (uma "caixa-preta"), mas a auditoria regulatória exige prova *determinística*.1 Os bancos estão, portanto, presos: ou inovam e assumem um risco legal e de conformidade inaceitável, ou mantêm a conformidade e estagnam.2

O problema não é a falta de modelos de IA; é a ausência de uma infraestrutura que possa tornar a IA auditável e segura.1 Qualquer solução focada apenas no "modelo" de IA está, portanto, resolvendo o problema errado. A estratégia de IA do BTG Pactual depende de resolver esse problema fundamental de infraestrutura primeiro.

### **1.2. A Anatomia da Falha: Desconstruindo a Tese 1.0 e a Falha do Mercado**

Para construir credibilidade junto a uma instituição Tier 1, é imperativo endereçar proativamente as arquiteturas falhas. A solução legada da indústria, incluindo uma "Tese 1.0" anterior, baseava-se em "processamento de PII em RAM" (Zero-Persistence 1.0) e "hashing de PII" (Protocolo Veritas 1.0).5

Uma análise jurídica e técnica rigorosa conclui que esta arquitetura é "Morta à Nascença" (Dead-on-Arrival).5 Ela é uma "simbiose de falha" 6 que viola *ambos* os mandatos do paradoxo simultaneamente:

1. **Violação 1 (SOX/BACEN):** Processar PII em RAM e depois destruí-lo (ZPA 1.0) é funcionalmente "Destruição de Evidências como Serviço".5 Um auditor da CVM ou do Departamento de Justiça dos EUA (DOJ) não pode aceitar um *hash* como substituto legal para os dados brutos. É impossível para o auditor verificar independentemente a lógica de negócios (ex: "o cálculo de risco estava correto?") a partir de um hash.5  
2. **Violação 2 (FTC/LGPD):** A Federal Trade Commission (FTC) dos EUA, um análogo regulatório influente, é clara: "Hashing Não é Anonimização".2 O hashing de PII — dados com espaço de entrada finito como CPF, data de nascimento ou número de conta — é trivialmente reversível através de ataques de *rainbow table*.5 Portanto, o hash de PII *ainda é PII*, e armazená-lo viola os mandatos de privacidade.

A tabela a seguir resume essa falha arquitetônica fundamental e introduz a solução da Tese 2.0.

**Tabela 1: Matriz de Falha Regulatória (Tese 1.0 vs. Tese 2.0)** 5

| Requisito Regulatório | Paradigma Legado (Tese 1.0) | Resultado Legal/Risco | Veritas 2.0 (Canônica) |
| :---- | :---- | :---- | :---- |
| **SOX / BACEN (Retenção)** | Processamento de PII em RAM (ZPA 1.0) | **VIOLAÇÃO DIRETA.** "Destruição de Evidências". | **RESOLVIDO.** Posição Não-Custodial. O registro da *prova* é retido (Pilar 1). |
| **FTC / LGPD (Privacidade)** | Hash de PII (Protocolo Veritas 1.0) | **VIOLAÇÃO DIRETA.** "Hashing é PII". Risco de *rainbow table*. | **RESOLVIDO.** "PII Nunca Toca a Infraestrutura". Apenas a *prova* (VC) é usada (Pilar 2). |

A capacidade de identificar essa falha demonstra uma profunda vantagem de domínio. A Tese 2.0 só pôde ser criada por uma equipe com expertise convergente em Direito (compreendendo as nuances da SOX vs. FTC), Finanças (compreendendo a necessidade do banco Tier 1\) e Deep-Tech (compreendendo W3C Verifiable Credentials e Crypto-Shredding).1 Ao desconstruir a Tese 1.0, a FoundLab demonstra que já passou pela rigorosa *due diligence* jurídica e técnica que a própria equipe de Risco do BTG executaria.

### **1.3. A Nova Categoria: "Compliance-as-Infrastructure"**

A FoundLab não deve ser categorizada como uma RegTech tradicional.1 A distinção é fundamental:

* **RegTechs Tradicionais (ex: idwall, Kronoos):** São "trens".1 Elas automatizam um processo de negócios (como KYC) e operam sobre os "trilhos" da infraestrutura legada do banco.3  
* **O Problema:** Se os "trilhos" — a infraestrutura de log e auditoria — são inseguros, alteráveis ou baseados em "confiança" (logs de texto frágeis), a automação (o "trem") apenas *acelera a geração de risco*.1  
* **A Solução FoundLab:** A FoundLab "não constrói outro trem". Ela "constrói os trilhos da próxima geração".1

A FoundLab introduz uma nova categoria de mercado: "Compliance-as-Infrastructure" (Conformidade como Infraestrutura).1 Esta é uma camada fundamental que transforma a conformidade de um processo manual, reativo, caro e baseado em "confiança" em um ativo de infraestrutura programável, automatizado, matematicamente verificável e baseado em "prova".1

A plataforma não *compete* com as RegTechs que o BTG já utiliza; ela se torna a *infraestrutura habilitadora* sobre a qual elas devem operar para serem legalmente viáveis e defensáveis na era pós-IA.1 Para o BTG, a adoção da FoundLab não é uma decisão de "substituir", mas de "fundação" — é a camada de base que torna o restante da pilha de tecnologia do banco (incluindo IA e RegTechs) auditável e segura.

### **1.4. A Tese Canônica (Veritas 2.0): De Probabilístico para Determinístico**

O mercado está focado no "modelo" (a IA), que é inerentemente *probabilístico*. Modelos podem "alucinar" e são atualizados mensalmente.1 Isso cria um "pesadelo de auditoria".1 Se um regulador perguntar: "Por que essa decisão de crédito foi tomada há 5 anos?", o banco não pode simplesmente "re-executar" a consulta. O modelo original não existe mais, e um modelo mais novo (ex: Gemini 2.0) daria uma resposta diferente.1

A tese da FoundLab é que o valor não está no modelo *probabilístico*, mas na *prova determinística*.1 O silogismo de valor da IA para o setor financeiro é:

1. IA de alto valor (ex: chatbot de Private Bank) requer acesso a dados sensíveis (PII).1  
2. O uso de dados sensíveis exige prova criptográfica irrefutável para satisfazer auditores (BACEN, CVM, LGPD).1  
3. **Conclusão:** A IA de valor institucional não é apenas um modelo; é a simbiose de uma **Infraestrutura de Confiança (Umbrella) \+ uma Trilha de Prova Determinística (Veritas 2.0)**.1

A plataforma FoundLab "envelopa" a chamada de IA (probabilística) com uma trilha de auditoria (determinística). Esse "envelope" de prova criptográfica é o que fornece a "licença regulatória" para operar a IA em escala sobre dados sensíveis.1

Para o auditor que pergunta sobre a decisão de 5 anos atrás, o banco não "re-executa" o modelo. Em vez disso, ele "reproduz" (replays) o **Pacote de Evidência** imutável (o envelope determinístico) gerado pelo Veritas 2.0. Esse pacote prova deterministicamente qual lógica (policy\_version) e quais dados (hash\_in) foram usados naquele momento específico.1 Esta é a única arquitetura que torna a IA, que está em constante fluxo, auditável a longo prazo.

---

## **PARTE 2: A ARQUITETURA DA CONFIANÇA (O "COMO")**

Esta seção detalha a "Linha Oficial Canônica".5 É o mergulho técnico para as equipes de Arquitetura e Risco do BTG, explicando *como* a Tese 2.0 funciona e por que ela é legalmente defensável.

### **2.1. Princípio Central da Tese 2.0: "PII Nunca Toca a Infraestrutura"**

Este é o pivô arquitetônico fundamental que anula a Tese 1.0.5 A FoundLab migra de um "Processador Efêmero de PII" para um "Orquestrador de Confiança Não-Custodial".5

A plataforma *não* ingere, processa, armazena ou faz hash de PII (nomes, CPFs), nem mesmo em memória volátil (RAM).5

A confiança é estabelecida por uma nova primitiva criptográfica: a verificação de **W3C Verifiable Credentials (VCs)**.2 Em vez de processar o PII bruto do cliente, a plataforma apenas recebe e verifica uma "Apresentação Verificável" (VP) — uma prova digital assinada que atesta um fato (ex: "KYC Aprovado pelo Emissor X").

Ao adotar uma arquitetura "Não-Custodial", a plataforma FoundLab (atuando como Verificador) se exime arquitetonicamente da responsabilidade de *reter* o PII (o mandato da SOX/BACEN). A obrigação de retenção dos dados brutos recai sobre o *Emissor* da VC (o "Rei", que neste modelo é o próprio BTG). A FoundLab retém apenas a *prova da verificação* — o "Decision Evidence Object" (DEO). Ao reter o DEO (que não contém PII) em um ledger WORM, a FoundLab cumpre o mandato de retenção (SOX/BACEN) sobre *seu próprio processo*, sem violar a LGPD (pois não há PII).

### **2.2. Componentes da Plataforma Canônica (Umbrella, Veritas 2.0, ZPA 2.0)**

A arquitetura é composta por três componentes principais que operam no modelo "Reis e Rebeldes".

**Tabela 2: Arquitetura de Componentes Canônicos (Veritas 2.0)** 5

| Componente | Persona (Modelo "Reis e Rebeldes") | Onde Roda | Função Principal (Tese 2.0) |
| :---- | :---- | :---- | :---- |
| **ACL 2.0 (Anti-Corruption Layer)** | O "Rei" (Emissor, ex: BTG) | Perímetro do BTG (VPC) | **Emissor de VCs.** Monitora o core banking e transforma "fatos" internos (ex: kyc\_status: true) em W3C VCs assinadas. |
| **ZPA 2.0 (Zero-Persistence Architecture)** | O "Rebelde" (Verificador) | Endpoint Efêmero (Cloud Run) | **Verificador Não-Custodial.** Recebe a "prova" (VP) do cliente, executa a verificação criptográfica e purga a RAM. É a implementação *legalmente defensável* de "Zero-Persistence". |
| **Veritas 2.0 Ledger** | O "Cartório" (Auditor) | GCP do BTG (BigQuery WORM) | **O "Testamento Técnico".** Armazena o **DEO** (metadado não-PII) da verificação em um ledger WORM (deletion\_protection=true), garantindo a prova de auditoria. |

O **Umbrella** é o "Orquestrador Cognitivo" ou "Fábrica de Decisão" que opera *acima* desses componentes.1 Ele atua como o gateway de governança central para o BTG:

1. **Definir Acesso:** Intercepta a consulta do usuário e aplica as políticas de IAM (Identity and Access Management) do banco.1  
2. **Montar Comando (RAG Institucionalizado):** Executa o Pilar 1 (Relevância). Garante que a IA seja "ancorada" em fontes de dados *internas e vetadas* pelo BTG (ex: "dossiê do cliente X", "política de onboarding Y"), mitigando "alucinações" e prevenindo a exfiltração de dados.1  
3. **Encaminhar e Monitorar:** Encaminha o prompt seguro para o modelo de IA (ex: Gemini) e força o resultado a passar pelo **Veritas 2.0** para a geração do "envelope de prova" determinístico.3

O desacoplamento do "Umbrella" (Fábrica de Decisão) do "Veritas" (Cartório Técnico) é a chave para a escala *organizacional*.1 O Private Bank do BTG pode usar o Umbrella para orquestrar o Gemini 1.5 Pro, enquanto a área de Compliance usa um modelo de risco interno. Embora funcionalmente distintos, ambos os fluxos são *forçados a passar pelo mesmo framework de prova do Veritas 2.0*. Isso permite "execução descentralizada com governança e auditoria centralizadas".1

### **2.3. Resolvendo o Paradoxo: Os Três Pilares da Conformidade Defensável**

Esta é a solução de engenharia para o paradoxo legal, alcançada através do "Desacoplamento Físico-Criptográfico".4 A arquitetura permite ao BTG Pactual, pela primeira vez, cumprir os mandatos conflitantes de Retenção (SOX/BACEN) e Exclusão (LGPD) simultaneamente.

**Tabela 3: Os Três Pilares da Conformidade Defensável (Veritas 2.0)** 5

| Pilar | Mandato Resolvido | Objetivo | Mecanismo Técnico (Tese 2.0) |
| :---- | :---- | :---- | :---- |
| **1\. Imutabilidade Física** | **SOX / BACEN (Retenção)** | Garantir que o registro de auditoria *nunca* seja fisicamente excluído. | **BigQuery WORM.** Ledger com deletion\_protection=true (Nível de Infra) \+ IAM Append-Only (Nível de App).2 |
| **2\. Veracidade Criptográfica** | **FTC (Hashing Inseguro)** | Armazenar uma prova auditável *sem* armazenar PII ou PII-hash. | **W3C VCs / DEO.** O Ledger (Pilar 1\) armazena o PresentationHash (hash da *prova*), não o hash do *PII*.5 |
| **3\. Desacoplamento Criptográfico** | **LGPD (Exclusão)** | Permitir a exclusão *lógica* do PII sem violar a retenção *física* do Pilar 1\. | **Cloud KMS (CMEK) com "Crypto-Shredding"**.1 |

O Pilar 3, **"Crypto-Shredding"**, é a solução técnica para o Paradoxo Regulatório. O processo é o seguinte 2:

1. **O Problema:** Como "esquecer" (LGPD) um dado que reside em um ledger WORM (SOX)?  
2. **A Arquitetura:** O PII (que reside em outros sistemas do BTG, *não* no ledger Veritas) é criptografado usando uma Chave de Criptografia Gerenciada pelo Cliente (**CMEK**) no Google Cloud KMS. O controle dessa chave pertence *exclusivamente* ao BTG.  
3. **A Ação (LGPD):** Para atender a uma solicitação de "Direito de Ser Esquecido", o oficial de compliance do BTG *não* tenta deletar o registro do WORM (o que é impossível e ilegal sob a SOX). Em vez disso, o oficial *destrói a chave CMEK* associada àquele PII.  
4. **O Resultado:** O registro físico (o *ciphertext*) permanece no ledger WORM, **satisfazendo a SOX/BACEN**. No entanto, ele se torna "lixo criptográfico" — permanentemente ilegível e irrecuperável — **satisfazendo a LGPD**.

A FoundLab transformou um problema jurídico insolúvel em um problema de engenharia de gerenciamento de chaves. Esta é uma solução técnica e defensável que as equipes de arquitetura e risco podem implementar.

### **2.4. O Runbook de Auditoria Determinístico (A Prova para o Regulador)**

Este é o processo exato que um auditor do BACEN ou da CVM executaria, usando apenas o decision\_id de uma transação e ferramentas públicas.5

**Cenário:** Auditor do BACEN possui decision\_id \= 'dec\_12345'.

1. **Passo 1: Consulta Soberana (Acesso Read-Only):**  
   * **Ação:** O auditor, usando o acesso de leitura concedido *pelo BTG*, consulta *diretamente* o ledger BigQuery WORM na conta GCP *do BTG*.5  
   * **Comando:** SELECT \* FROM veritas\_audit\_ledger\_v2 WHERE decision\_id \= 'dec\_12345'.9  
   * **Resultado:** O auditor obtém o registro DEO (não-PII).5  
2. **Passo 2: Verificação do Emissor (Resolução de DID):**  
   * **Ação:** O auditor extrai o issuer\_did do DEO (ex: did:web:btg.com). Em seu *próprio navegador*, ele resolve este Identificador Descentralizado (DID) acessando o endpoint público .well-known do banco.5  
   * **Comando:** curl https://btg.com/.well-known/did.json.9  
   * **Resultado:** O auditor obtém a chave pública oficial do BTG, confirmando criptograficamente que o BTG foi o Emissor.5  
3. **Passo 3: Verificação de Revogação (Confirmação de Validade):**  
   * **Ação:** O auditor extrai o revocation\_check.list\_checked (ex: https://btg.com/credentials/status/list) do DEO e confirma que a VC não estava listada como revogada no timestamp\_verified.6

**A Conclusão Forçada do Auditor:** O auditor é forçado a concluir: "Houve uma verificação criptográfica válida (Passo 3), por um emissor confiável (Passo 2), em um horário exato, e o registro da prova é imutável (Passo 1).".5

O auditor *nunca* precisou ver o PII do cliente e *nunca* precisou confiar no software da FoundLab. Ele usou apenas criptografia de chave pública e o ledger soberano do BTG. Esta arquitetura *elimina a FoundLab como um intermediário de auditoria* 5 e fornece a resposta técnica direta ao **Artigo 14 da Resolução 4.893 do BACEN**, que exige acesso direto do regulador aos dados.5

---

## **PARTE 3: SOBERANIA E VALOR (O "PARA QUEM" \- BTG)**

Esta seção foca na implementação específica para o BTG, traduzindo a arquitetura em soberania de dados e valor de negócio.

### **3.1. Modelo Recomendado para BTG: A Soberania do "Dedicated/VPC"**

Para uma instituição Tier 1, o modelo SaaS multi-tenant é um "não-início" (non-starter) para dados bancários core.1 A proposta para o BTG Pactual é, inequivocamente, o **Modelo Dedicated / On-Prem / VPC**.1

Neste modelo, a plataforma FoundLab é entregue como **Infraestrutura-como-Código (IaC)** (ex: Terraform/Terragrunt) e implantada *inteiramente dentro da VPC e do projeto de nuvem do BTG*.1

Isso estabelece a "Linha de Base da Soberania" 1, onde o BTG ganha o melhor dos dois mundos: a soberania de dados do on-premise com a escalabilidade dos serviços gerenciados (KMS, BigQuery) da nuvem. A FoundLab fornece o *software* e os *runbooks*; o BTG retém *100% de soberania* sobre a infraestrutura, os dados e as chaves.1

### **3.2. A "Trindade da Confiança": Alinhamento Técnico com a Res. 4.893 do BACEN**

A arquitetura de rede que implementa o modelo "Dedicated" é construída sobre três pilares de segurança que formam a "Trindade da Confiança" 1:

1. **Perímetro Soberano (VPC Service Controls \- VPC-SC):** Atua como o "muro do castelo".1 É um "firewall para as APIs do Google" que bloqueia *arquitetonicamente* a exfiltração de dados (ex: logs do BigQuery) para fora do perímetro de segurança definido pelo BTG.1  
2. **Chaves Soberanas (CMEK/HSM):** O "kill switch" regulatório.1 O BTG mantém controle total sobre suas próprias chaves de criptografia no Google Cloud KMS (ou Cloud HSM).1 Isso habilita o Pilar 3 (Crypto-Shredding).  
3. **Logs Soberanos (WORM no Projeto do Banco):** A trilha de auditoria (o ledger Veritas 2.0) reside no projeto BigQuery *do BTG*.1

Esta arquitetura não apenas "alega conformidade"; ela entrega uma propriedade inerente ao sistema que satisfaz o CISO, o Diretor de Risco e o Regulador.1

**Tabela 4: Mapeamento de Conformidade (BACEN Res. 4.893 vs. Trindade da Confiança)** 5

| Requisito Regulatório | Artigo (BACEN Res. 4.893) | Resposta Técnica FoundLab (Trindade da Confiança) | Benefício para o BTG (Soberania) |
| :---- | :---- | :---- | :---- |
| **Controle e Supervisão** | Art. 11, 12, 13 | A infra (IaC) é implantada na conta GCP do cliente. | Controle e Supervisão Diretos. O BTG gerencia a infra. |
| **Acesso do BACEN** | **Art. 14** | **Logs Soberanos:** O cliente (BTG) concede acesso direto ao BACEN em seu próprio BigQuery WORM. | **Soberania de Auditoria.** FoundLab é eliminada como intermediário. |
| **Proteção de Dados** | LGPD Art. 46 / BACEN | **Perímetro Soberano (VPC-SC).** | Prevenção de Exfiltração. Os metadados não podem sair do perímetro. |
| **Custódia de Chaves** | LGPD / BACEN | **Chaves Soberanas (CMEK/HSM).** | **"Kill Switch" Criptográfico.** O BTG detém o controle criptográfico final. |

### **3.3. O "Alfa Operacional" (ROI\_E): O Valor de Negócio Quantificável**

O valor da plataforma não é apenas defensivo (risco); é ofensivo (eficiência).

O ROI Explícito ("Alfa Operacional"):  
A plataforma foi validada em produção em um caso de uso análogo no ecossistema de um Banco Tier 1 (Elite Capital).4 Os resultados demonstram ganhos de eficiência massivos:

* **Redução de Tempo:** **98,7%** de redução no Tempo de Processamento de compliance. Um processo manual que consumia **21 horas** foi reduzido para **16 minutos**.4  
* **Redução de Erro:** **94%** de redução na Taxa de Erros manuais, substituindo a análise humana falível por um motor de IA determinístico.4

Essa aceleração de aproximadamente 80x 4 traduz o "compliance" (um centro de custo) em "alfa operacional" (um gerador de eficiência).

O ROI Estratégico (O "ROI Oculto"):  
O valor mais significativo reside na eliminação de classes inteiras de risco de exfiltração de dados e, o mais importante, na obtenção da "licença regulatória" para finalmente usar IA Generativa em dados sensíveis, desbloqueando novos produtos e serviços.1

### **3.4. Desbloqueando a IA: Casos de Uso Imediatos no BTG**

A plataforma FoundLab torna o uso de IA em PII tangível e seguro:

* **Caso de Uso 1: Onboarding e Compliance Automatizado** 1  
  * **Descrição:** Automatizar o processo de onboarding de clientes (ex: PJ complexo), que hoje consome horas de trabalho manual.5  
  * **Solução FoundLab:** O Umbrella (IA) processa os documentos (em memória volátil \- ZPA 2.0), e o Veritas 2.0 registra imutavelmente cada passo, consentimento LGPD e decisão como um Pacote de Evidência criptográfico, gerando o "Alfa Operacional" de 98,7%.1  
* **Caso de Uso 2: Chat Interno Auditável (A "Joia da Coroa")** 1  
  * **Descrição:** O "santo graal" — usar IA Generativa sobre PII de clientes.1 Por exemplo, um chatbot de Private Bank que responde a um analista: "Qual a exposição do Cliente X a títulos de tecnologia?".1  
  * **O Problema Legado:** Impossível de auditar e alto risco de vazamento de PII em logs de prompt.  
  * **Solução FoundLab:**  
    1. **Umbrella (RAG):** Garante que o chatbot use *apenas* dados internos vetados (o dossiê do cliente, as políticas de risco do banco).1  
    2. **Veritas 2.0:** Registra um Pacote de Evidência (DEO) *determinístico* da consulta e da resposta (ex: model\_version, policy\_version, hash\_in), *sem* registrar o PII do cliente no log, fornecendo a "prova de replay".1

A plataforma é projetada para ser "Antifrágil" — ela melhora com as falhas.1 Através do "AI Flywheel", quando um analista de risco (Human-in-the-Loop) discorda e corrige uma decisão da IA, o Veritas 2.0 registra essa correção (HUMAN\_OVERRIDE) como um evento criptográfico imutável. Esse registro se torna um "ground truth" de alta qualidade para re-treinar o modelo de IA. A cada correção humana, o "fosso de dados" (data moat) proprietário do BTG (seu capital intelectual de risco) se aprofunda, tornando sua IA progressivamente mais inteligente e defensável.1

---

## **PARTE 4: A VISÃO E ATIVAÇÃO**

Esta seção consolida a parceria de longo prazo e define um próximo passo tático e imediato.

### **4.1. Visão de Longo Prazo: O Modelo "Reis e Rebeldes" (VaaS)**

A visão de longo prazo é uma parceria B2B2B que transforma o BTG de cliente em parceiro de ecossistema.1

* **Horizonte 1: O "Rei" se Equipa (Uso Interno):**  
  * **Ação:** O BTG (o "Rei") implanta o modelo "Dedicated/VPC" internamente.5  
  * **Valor:** Ganha "Alfa Operacional" e defesa regulatória.  
* **Horizonte 2: O "Rei" Habilita o Ecossistema (Emissão de VCs):**  
  * **Ação:** O BTG, agora equipado com o componente ACL 2.0 (Emissor), começa a *emitir* W3C Verifiable Credentials para seus clientes.5  
  * **Exemplo:** BtgKycApprovedCredential ou BtgSuitabilityVerifiedCredential.5  
* **Horizonte 3: "Veritas-as-a-Service" (VaaS) (Monetização):**  
  * **Ação:** Os "Rebeldes" (Fintechs, Gestoras, Family Offices no ecossistema do Private Bank do BTG) 5 agora podem verificar instantaneamente as VCs dos clientes.  
  * **O Fluxo:** O cliente (Titular) apresenta sua VC (emitida pelo BTG) ao "Rebelde". O "Rebelde" usa o componente ZPA 2.0 (Verificador) para validar a prova contra o ledger do BTG.5

O resultado é um "fosso de rede" (network moat).6 O onboarding de um cliente BTG em uma gestora "Rebelde" cai de *dias para segundos*.7 Isso cria um poderoso incentivo para que clientes e gestoras operem *dentro* do ecossistema de confiança do BTG. O BTG transforma seu *custo* de compliance em um *fluxo de receita* (VaaS) e uma *vantagem competitiva* estratégica.

### **4.2. Chamado à Ação: A Prova de Conceito (PoC) de 15 Dias**

O engajamento não começa com uma demo, mas com uma Prova de Conceito (PoC) de 15 dias focada em validar a infraestrutura.1

O objetivo desta PoC (re-contextualizada para a Tese 2.0) não é testar "PII-em-RAM". O objetivo é *validar a infraestrutura de conformidade defensável*.5

**Objetivo Principal da PoC:** Implantar a infraestrutura canônica (Ledger WORM) no ambiente sandbox do BTG e **gerar o primeiro "Pacote de Evidência" (DEO) criptograficamente verificável**.1

**O Plano de 15 Dias:** 1

| Dias | Fase | Atividade Chave | Objetivo |
| :---- | :---- | :---- | :---- |
| **D1–D2** | Alinhamento e Arquitetura | Sessão de deep dive técnico. | Definir escopo da PoC, requisitos de VPC, IAM e CMEK. |
| **D3–D5** | Deploy de Infra (IaC) | Provisionar a infra sandbox via IaC. | Validar o deploy automatizado no projeto do banco. |
| **D6–D12** | Configuração (Umbrella & Veritas) | Conectar 1-2 fontes de dados (RAG); Configurar o Ledger WORM (BigQuery). | Validar a geração do decision\_id e a escrita imutável. |
| **D13–D15** | Demonstração de Valor | Executar o fluxo ponta-a-ponta. | Gerar o primeiro Pacote de Evidência e **executar o "Runbook de Auditoria Determinístico"**. |

**Próximos Passos Imediatos:** 1

1. Agendar a sessão de deep-dive de arquitetura (Dias 1-2).  
2. Provisionar um projeto sandbox dedicado no Google Cloud do BTG.  
3. Conceder à equipe da FoundLab as permissões de IAM necessárias para executar o deploy da infraestrutura (IaC).

---

## **ANEXOS**

* **Anexo A:** Relatório de Due Diligence: A Falha da Tese 1.0 vs. A Defensibilidade da Tese 2.0 1  
* **Anexo B:** Especificação Profunda do Protocolo Veritas 2.0 e Esquema do DEO (Decision Evidence Object) 1  
* **Anexo C:** Mapeamento de Conformidade Detalhado (Artigo-por-Artigo): BACEN Res. 4.893 1  
* **Anexo D:** Plano de Implantação da PoC de 15 Dias (Requisitos de IaC e IAM) 1  
* **Anexo E:** O "Fosso" da FoundLab: A Vantagem de Domínio (Jurídico, Financeiro, Técnico) 