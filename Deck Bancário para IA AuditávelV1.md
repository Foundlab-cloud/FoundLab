

# **Infraestrutura de Confiança Auditável para IA no Perímetro TIER 1 BANCÁRIO: Uma Análise de Due Diligence Técnico e Regulatório**

**Subtítulo: A Implementação da Tese FoundLab (Umbrella · Veritas 2.0 · Zero-Persistência) para Soberania de Dados e Conformidade BACEN**

---

## **Seção 1: O Paradoxo do Banco: IA Travada por Risco Regulatório**

O imperativo estratégico para instituições financeiras Tier 1, como o BTG PACTUAL/SANTANDER/BRADESCO/ITAÚ, é a aplicação de Inteligência Artificial Generativa (IA Gen) sobre seus dados operacionais e sensíveis. O objetivo é gerar "alfa" competitivo, otimizar a eficiência e criar novas experiências de cliente, como no Private Banking, por exemplo, através da análise de posições de carteira.1

No entanto, esta inovação encontra-se universalmente bloqueada por um obstáculo regulatório e de infraestrutura. A natureza da IA Generativa é *probabilística* — seus resultados são inerentemente não determinísticos.1 Isso entra em conflito direto com o mandato de conformidade (BACEN, CVM), que exige prova *determinística* e uma trilha de auditoria irrefutável para qualquer decisão que toque dados sensíveis de clientes.1 Este é o "Paradoxo Regulatório".1

A arquitetura de segurança legada, frequentemente descrita como uma "fortaleza com mil portas", é um *patchwork* de sistemas incapaz de suportar esta nova carga de trabalho.1 A auditoria atual é um processo manual, reativo e caro, baseado em "confiança" em logs de texto, planilhas e capturas de tela.1 Logs de texto são frágeis, alteráveis e, portanto, "indefensáveis" em um litígio ou investigação regulatória.3

Modelos de software como serviço (SaaS) *multi-tenant* agravam o problema e são considerados um "não-início" (non-starter) para dados bancários *core*. O risco de *data-bleed* (vazamento de dados entre *tenants*) ou uma simples falha de configuração de isolamento apresenta um risco existencial.1 Instituições Tier 1 exigem soberania e controle de perímetro absolutos.1

O problema central que a FoundLab resolve não é a *falta de IA* — o banco já tem acesso a modelos poderosos. O problema é a *ausência de uma licença regulatória para usar a IA* em escala. A plataforma FoundLab é projetada para fornecer essa licença, substituindo a "confiança" frágil em processos por "prova matemática" irrefutável.1

## **Seção 2: A Tese da FoundLab: De Probabilístico para Determinístico**

A tese da FoundLab é articulada através de um silogismo rigoroso que redefine o valor da IA para o setor financeiro 1:

1. A IA de alto valor (ex: um *chatbot* de Private Bank) requer acesso a **dados operacionais e sensíveis** do banco.  
2. O uso de dados sensíveis em um processo decisório exige uma **prova criptográfica irrefutável** para satisfazer auditores e reguladores (BACEN, CVM, LGPD).  
3. **Portanto:** A IA de valor institucional não é apenas um modelo inteligente; é a simbiose de uma **Infraestrutura de Confiança (Umbrella) \+ uma Trilha de Prova Determinística (Veritas 2.0)**.

A plataforma FoundLab, portanto, "envelopa" a chamada de IA, que é inerentemente *probabilística*, com uma trilha de auditoria *determinística*.1 O mercado está focado no *modelo*; a FoundLab está focada na *prova*.1 Este "envelope" de prova criptográfica é a "licença regulatória" para operar.

Os dois componentes centrais que executam esta tese são:

* **Umbrella (O Orquestrador):** Definido como a "Fábrica de Decisão".1 Atua como o *gateway* de governança que se posiciona entre os usuários internos e os modelos de IA. Ele intercepta consultas, aplica as políticas de IAM (Identity and Access Management) do banco e utiliza RAG (Retrieval-Augmented Generation) para "ancorar" a IA em fontes de dados internas autorizadas.1  
* **Veritas 2.0 (A Camada de Prova):** Definido como o "Cartório Técnico".1 Para cada decisão orquestrada pelo Umbrella, o Veritas 2.0 gera um registro criptográfico imutável — a "prova" — que é armazenado de forma soberana pelo banco.1

Esta abordagem introduz uma nova categoria de mercado: **"Compliance-as-Infrastructure"** (Conformidade como Infraestrutura).1 A FoundLab não compete com *RegTechs* existentes (os "trens" que automatizam processos quebrados); ela constrói os "trilhos da próxima geração".1 Não é um "aplicativo", mas uma camada de fundação que habilita todas as outras aplicações de IA e RegTechs a se tornarem legalmente viáveis e defensáveis.1

## **Seção 3: O Fluxo Operacional: Da Consulta à Prova Imutável**

O fluxo de 6 passos a seguir detalha como a plataforma opera na prática, desde a consulta do usuário até a geração da prova imutável 1:

1. **Consulta do Usuário:** Um usuário interno (ex: Assessor de Private Bank) faz uma pergunta que envolve dados sensíveis em uma aplicação interna.1  
2. **Interceptação e IAM:** O **Umbrella** intercepta a consulta, autentica o usuário e aplica as políticas de IAM do Banco para determinar *quem* pode perguntar *o quê*.1  
3. **RAG Institucional:** O Umbrella executa um RAG (Retrieval-Augmented Generation), buscando dados *apenas* de fontes internas autorizadas (ex: "dossiê do cliente X") para "ancorar" a consulta da IA.1  
4. **Resposta da IA:** O *prompt* aumentado e seguro é enviado ao modelo de IA (ex: Gemini) para gerar uma resposta.1  
5. **Geração da Prova:** O **Veritas 2.0** *simultaneamente* gera um "Pacote de Evidência" (ou DecisionID) contendo os metadados da decisão (política usada, versão do modelo, timestamp, etc.).1  
6. **Armazenamento Soberano:** O registro da prova (sem PII) é salvo de forma imutável no *ledger* **WORM (Write-Once, Read-Many) do Banco**, tipicamente em seu próprio projeto BigQuery.1

Esta arquitetura é definida por um **"Fluxo Duplo"** que separa o tratamento de dados voláteis (PII) do de provas persistentes (metadados), resolvendo o conflito regulatório central.1

**Tabela 1: A Arquitetura de Fluxo Duplo**

| Característica | Fluxo de Dados (Volátil) | Fluxo de Prova (Persistente) |
| :---- | :---- | :---- |
| **Dado** | PII do Cliente, consulta, resposta da IA | Metadados: DecisionID, *hashes*, policy\_version, timestamp, actor\_id |
| **Estado** | Volátil (existe apenas em RAM) | Persistente e Imutável |
| **Princípio** | Zero-Persistência (ZPA) 1 | Veritas 2.0 1 |
| **Ação Final** | *Purge* (Descarte da RAM) 1 | Escrita em WORM (BigQuery do Banco) 1 |
| **Cumprimento** | **LGPD** (Minimização de Dados) | **CVM/BACEN** (Retenção de Auditoria) |

Neste modelo, o RAG (Passo 3\) funciona como um mecanismo de segurança de dados crítico. Ele não apenas melhora a precisão da IA, mas *reforça* o IAM (Passo 2), garantindo que a IA generativa opere estritamente dentro das permissões de dados já estabelecidas para o usuário, impedindo que ela contorne as políticas de acesso.1

## **Seção 4: A Arquitetura de Soberania: A "Trindade da Confiança" no Perímetro do Banco**

Para um banco Tier 1, a segurança não é negociável. O modelo de implantação proposto é inequivocamente o **Dedicated/VPC**.1 Nesta "Linha de Base da Soberania" 1, a plataforma é entregue como Infraestrutura como Código (IaC) e implantada *inteiramente dentro* do projeto Google Cloud (GCP) e da Virtual Private Cloud (VPC) do Banco.1 A FoundLab entrega o software; o Banco retém 100% de soberania sobre a infraestrutura, os dados e as chaves.

Esta arquitetura de soberania é mantida pela **"Trindade da Confiança"** 1:

1. **Pilar 1: O Perímetro de Rede (VPC Service Controls \- VPC-SC)**  
   * **Função:** O "muro do castelo".1 O VPC-SC atua como um "firewall para as APIs do Google".7  
   * **Mecanismo:** Ele cria um perímetro de segurança em nível de nuvem que bloqueia *qualquer* tentativa de exfiltração de dados (ex: uma cópia do BigQuery para um *bucket* público) no nível da infraestrutura do Google. Esta proteção se aplica independentemente das permissões de IAM, mitigando o risco de *insiders* ou credenciais comprometidas.1  
2. **Pilar 2: O Perímetro de Chaves (CMEK/HSM)**  
   * **Função:** O "kill switch" regulatório.1  
   * **Mecanismo:** O Banco utiliza e controla 100% de suas próprias Chaves de Criptografia Gerenciadas pelo Cliente (CMEK) ou Hardware Security Module (HSM). A aplicação FoundLab recebe apenas a permissão para *usar* a chave para criptografar o *ledger*, mas o Banco retém a *propriedade* da chave, incluindo o controle sobre rotação e destruição.1  
3. **Pilar 3: O Perímetro de Prova (Logs Soberanos e PSC)**  
   * **Função:** O "caminho seguro" e o "cofre do cartório".1  
   * **Mecanismo (PSC):** O Private Service Connect garante que toda a comunicação entre os microsserviços da plataforma e os serviços de dados (como o BigQuery WORM) ocorra *inteiramente* dentro da rede de *backbone* privada do Google, nunca atravessando a internet pública.1  
   * **Mecanismo (Logs WORM):** A trilha de auditoria do Veritas 2.0 é escrita *diretamente* no projeto BigQuery WORM *do próprio banco*.1

A "Trindade da Confiança" mitiga riscos em três níveis distintos: (1) o dado não pode sair (VPC-SC), (2) o dado não pode ser lido sem a chave soberana (CMEK), e (3) a prova não pode ser alterada (WORM). Isso transforma a narrativa de "Por favor, confie no nosso SaaS" para "Nós lhe damos as ferramentas para *você* controlar e provar sua própria infraestrutura".7

## **Seção 5: Veritas 2.0: O Cartório Técnico Não-Custodial**

O Veritas 2.0 é o componente que gera o artefato central de auditoria: o "Pacote de Evidência" ou "Registro de Decisão" (DecisionID).1 Este é o registro imutável que um auditor do BACEN ou da CVM analisará.1

O design mais crítico é que este registro armazena **metadados, não PII (Informações de Identificação Pessoal)**.1

**Tabela 2: Anatomia do Registro de Decisão (DecisionID)**

| Campo | Descrição | Propósito |
| :---- | :---- | :---- |
| **decision\_id** | Identificador único (UUID) da decisão 3 | Rastreabilidade 1 |
| **actor\_id** | Quem (usuário/serviço) solicitou a decisão | Responsabilidade (Accountability) |
| **timestamp\_verified** | O *timestamp* exato da decisão 1 | Ordem cronológica 1 |
| **policy\_version** | O hash/versão da política de risco usada (ex: "KYC\_Onboarding@2.3.1") 1 | Replay Determinístico 1 |
| **model\_version** | O hash/versão do modelo de IA usado (ex: "gemini-1.5-pro-2025-10") 1 | Replay Determinístico 1 |
| **input\_hash** | O *hash* (impressão digital) dos dados de entrada (NÃO o PII) 1 | Integridade dos dados 3 |
| **output\_hash / decision\_status** | O *hash* da resposta ou a decisão final (ex: "APPROVED") 1 | Prova do resultado |
| **jws / proof\_signature** | A assinatura criptográfica que sela este registro 1 | Imutabilidade e Não-Repúdio |

A garantia de imutabilidade (WORM) é aplicada tecnicamente em duas camadas: (1) O IaC (Terraform) define a tabela do BigQuery com deletion\_protection \= true, e (2) é usada uma função IAM personalizada (Veritas-WORM-Ingestor) que *nega* explicitamente as permissões bigquery.tables.updateData e bigquery.tables.deleteData, permitindo apenas bigquery.tables.insertData.9

Esta arquitetura permite o "Replay Determinístico".1 Se um auditor questionar uma decisão de 5 anos atrás, o Banco não "re-executa" a consulta (o modelo de IA já mudou). Em vez disso, o Banco "reproduz" (replays) o DecisionID.1 Este registro prova deterministicamente qual policy\_version e model\_version foram usados, tornando a IA, que está em constante fluxo, auditável a longo prazo.1

## **Seção 6: A Solução para o Paradoxo Legal: LGPD vs. BACEN**

A plataforma resolve o conflito legal que atualmente paralisa as instituições financeiras, conhecido como o "Paradoxo Reter vs. Esquecer".1

* **O Mandato de Reter (CVM/SOX/BACEN):** Exige que as trilhas de auditoria sejam retidas em formato WORM (imutável) por 5 a 10 anos.1  
* **O Mandato de Esquecer (LGPD):** Concede ao titular dos dados o "Direito de Ser Esquecido", exigindo a exclusão de PII sob demanda.1

A arquitetura FoundLab resolve isso com uma solução de duas partes:

1. Princípio de Zero-Persistência (ZPA)  
   Esta é a implementação técnica do princípio de "minimização de dados" da LGPD.1 Dados PII (ex: a consulta do cliente, dados da carteira) existem apenas em memória volátil (RAM) durante os milissegundos da transação de IA. Os dados nunca tocam o disco (data-at-rest) na camada de computação.1 Isso elimina arquitetonicamente o risco de violação de banco de dados de PII.  
2. Mecanismo de Crypto-Shredding  
   Esta é a solução para o paradoxo, alcançada através do "Desacoplamento Físico-Criptográfico".1  
   * **Para satisfazer o CVM/BACEN:** O *blob* de dados criptografado (o DecisionID) é escrito no Ledger WORM e **nunca é excluído fisicamente**, cumprindo o mandato de retenção.1  
   * **Para satisfazer a LGPD:** Os dados são criptografados usando a chave CMEK soberana do Banco (Pilar 2 da Trindade). Quando o "Direito de Ser Esquecido" é exercido, o Banco **destrói a chave CMEK**.1  
   * **Resultado:** O *blob* físico permanece no WORM (cumprindo CVM), mas se torna "lixo criptográfico" permanentemente ilegível e irrecuperável (cumprindo LGPD).1

Esta arquitetura troca um problema jurídico insolúvel por uma solução de engenharia de chaves, onde o controle do "kill switch" (CMEK) está 100% nas mãos do Banco.1

## **Seção 7: Casos de Uso Imediatos e ROI para o BANCOS TIER 1**

A plataforma não é apenas uma infraestrutura de *compliance*, mas um habilitador de *valor de negócio*, entregando dois tipos de "alfa":

### **Caso de Uso 1: Onboarding/KYC Automatizado (Alpha de Eficiência)**

* **Dor:** Processos de Onboarding e KYC são manuais, lentos, caros e propensos a erros humanos, além de gerarem trilhas de auditoria frágeis.1  
* **Solução:** O Umbrella (IA) automatiza a análise de documentos e validações; o Veritas 2.0 gera a prova de *compliance* imutável para cada etapa.1  
* **ROI (Dados de Implementação):** A validação em processos análogos de *compliance* de ponta-a-ponta demonstrou um "Alfa Operacional" mensurável.1

**Tabela 3: ROI do Caso de Uso de Onboarding/Compliance**

| Métrica | Antes (Processo Manual) | Depois (Plataforma FoundLab) | Impacto |
| :---- | :---- | :---- | :---- |
| **Tempo de Ciclo** | 21 Horas 1 | 16 Minutos 1 | **Redução de 98.7%** 1 |
| **Taxa de Erro (Manual)** | 42% 1 | 2.5% 1 | **Redução de 94%** 1 |
| **Prova de Auditoria** | Logs de texto, planilhas 1 | Registro DecisionID imutável no BigQuery do Banco | Defensibilidade Determinística |

### **Caso de Uso 2: "BANK GPT" Interno Auditável (Alpha de Inovação)**

* **Dor:** O Banco deseja habilitar seus assessores e equipes internas com IA Generativa (ex: Gemini) para analisar dados de clientes (ex: "simule uma alocação de carteira para o cliente X"). Isso é bloqueado pelo risco de vazar PII para o provedor do modelo.1  
* **Solução (A "Tríade" de IA Segura):**  
  1. **Umbrella (RAG):** Busca os dados do cliente (PII) *internamente* e os injeta no *prompt*.1  
  2. **ZPA (Zero-Persistência):** A consulta \+ dados PII existem *apenas em RAM* durante a chamada à API do modelo.1 O PII nunca é logado pelo provedor.  
  3. **Veritas 2.0:** O sistema *não* registra a conversa (o PII). Ele registra a *ação* (metadados): "Assessor executou simulação para cliente \[hash\] às \[timestamp\]".1

Este caso de uso demonstra como a plataforma *desbloqueia* inovação que hoje está parada nas mesas de Risco e Jurídico, permitindo que o Banco use IA Gen com segurança sobre seus dados mais sensíveis.

## **Seção 8: Conformidade Regulatória Direta (Res. 4.893/2021)**

A narrativa central para a conformidade é: "Não é um SaaS que pede para você confiar, é uma infraestrutura que você controla." A arquitetura da plataforma é uma resposta técnica direta aos requisitos da regulação brasileira, notadamente a Resolução CMN nº 4.893/2021.

**Tabela 4: Matriz de Conformidade (BACEN/CVM)**

| Requisito Regulatório | Recurso Chave da FoundLab | Prova de Conformidade |
| :---- | :---- | :---- |
| **Res. CMN 4.893/2021** (Contratação de Nuvem) 1 | **Deploy Dedicated/VPC** 1 | A infraestrutura opera na conta GCP *do Banco*, não da FoundLab. O Banco mantém soberania. |
| **Art. 14, Res. 4.893** (Acesso do Supervisor) 1 | **Logs Soberanos** no BigQuery 1 | O Banco concede ao BACEN acesso de auditoria *diretamente* ao seu próprio projeto BigQuery. A FoundLab é eliminada como intermediário.1 |
| **Retenção de 5-10 Anos** (CVM/BCB) 1 | **Ledger WORM** (BigQuery Imutável) 1 | A prova (DecisionID) é escrita de forma "Write-Once, Read-Many", garantindo integridade pelo período exigido, conforme validado pelo design técnico do IAM (Veritas-WORM-Ingestor).9 |
| **LGPD** (Direito de Esquecimento) 1 | **CMEK \+ Crypto-Shredding** 1 | O Banco destrói a chave (CMEK) para tornar o dado ilegível, cumprindo a LGPD sem violar o mandato de retenção WORM (CVM).1 |
| **Prevenção de Exfiltração de Dados** | **VPC Service Controls** 1 | O "muro do castelo" 1 bloqueia o egresso de dados no nível da infraestrutura da nuvem, independentemente das permissões de IAM.7 |

## **Seção 9: O Plano de Ativação: Prova de Conceito em 15 Dias**

O engajamento proposto não é uma demo de vendas, mas uma Prova de Conceito (PoC) de 15 dias focada em validação técnica e de risco. O objetivo é gerar o primeiro "Pacote de Evidência" verificável *dentro* do ambiente sandbox do Banco.1

**Tabela 5: Cronograma da Prova de Conceito (15 Dias)**

| Dias | Fase | Atividade Chave |
| :---- | :---- | :---- |
| **Dias 1–2** | **Alinhamento e Arquitetura** | Sessão de *deep dive* técnico; definir escopo da PoC (1 caso de uso), requisitos de VPC, IAM e CMEK.1 |
| **Dias 3–5** | **Deploy de Infra (IaC)** | Provisionar a infraestrutura *sandbox* (Umbrella \+ Veritas) via Terraform/IaC no projeto GCP do Banco.1 |
| **Dias 6–9** | **Configuração e Conexão** | Conectar 1 fonte de dados interna (ex: dados simulados de Onboarding).1 |
| **Dias 10–12** | **Geração da Prova** | Executar o fluxo de decisão; gerar o primeiro DecisionID e validar a escrita imutável no BigQuery WORM do Banco.1 |
| **Dias 13–15** | **Demonstração de Valor** | Demo para Risco/Compliance, mostrando o "Pacote de Evidência" real e o "Software Verificador".1 |

Os entregáveis-chave desta PoC são tangíveis e direcionados à equipe de risco:

1. **O "Pacote de Evidência" (formato JWT/JSON):** Residindo de forma imutável no BigQuery WORM *do Banco*.2  
2. **O "Software Verificador" (script):** Uma ferramenta simples para o time de Risco do Banco validar criptograficamente a prova.2  
3. **Relatório de Métricas:** Latência da prova, *throughput*, etc..2

Esta PoC é projetada para obter a aprovação do *stakeholder* mais crítico (Risco/Compliance) primeiro, o que, por sua vez, desbloqueia a adoção pela área de Inovação.

## **Seção 10: Modelo de Deploy, Custo e Governança**

O modelo de engajamento é construído sobre a mesma premissa de soberania.

* **Modelo de Deploy:** A proposta é exclusivamente o **Dedicated/VPC (Single-Tenant)**, estabelecendo a "Linha de Base da Soberania".1  
* **Governança:** A implantação e as atualizações são gerenciadas via Infraestrutura como Código (IaC) (Terraform/Terragrunt), integrando-se aos *pipelines* de governança de mudança do banco.1  
* **Estrutura de Custo:** O modelo é projetado para alinhar incentivos e reforçar a soberania 1:  
  1. **Custo de Setup/Licença:** Um custo inicial (CAPEX-like) para o *deploy* do IaC e provisionamento da instância *single-tenant*.  
  2. **Custo de Consumo (Variável):** Um custo transacional (OPEX-like) cobrado por "Pacote de Evidência" / DecisionID gerado.  
  3. **Custo de Infra (Direto):** O Banco paga *diretamente ao GCP* pelo consumo de recursos em seu próprio projeto (ex: armazenamento do BigQuery WORM, computação do Cloud Run).

O terceiro item é uma característica da soberania: ao pagar diretamente pela infraestrutura de armazenamento de logs, o Banco reforça contratualmente e tecnicamente que o *ledger* de auditoria é 100% seu.

## **Seção 11: Call to Action (CTA) / Próximos Passos**

A solicitação formal e tática para iniciar a PoC de 15 dias é o próximo passo imediato 1:

1. **Liberar** o provisionamento de um projeto *sandbox* dedicado no Google Cloud.1  
2. **Conceder** à equipe da FoundLab as permissões de IAM mínimas necessárias para executar o *deploy* do IaC no referido projeto.1

A promessa é a entrega da primeira prova de auditoria determinística, operando dentro do perímetro de segurança do Banco, em até 15 dias.

## **Seção 12: Anexos Técnicos e Visão Futura**

(Materiais de suporte para *deep dive* técnico, disponíveis mediante solicitação)

* **Anexo A: O "AI Flywheel" (IA Antifrágil)**  
  * Detalha como a plataforma utiliza correções humanas (Human-in-the-Loop) como um sinal de treinamento. O Veritas 2.0 registra o *override* do analista como um novo evento criptográfico, que é usado como "verdade fundamental" (ground truth) para re-treinar e melhorar o modelo de IA de forma auditável.1  
* **Anexo B: Sinergia Estratégica com GCP**  
  * Análise de como a FoundLab atua como a "Camada de Confiança" (Trust Layer) que habilita e *desbloqueia* a adoção em larga escala de serviços de IA de alto valor do Google (como o Gemini) dentro do setor financeiro, resolvendo a objeção de *compliance*.1  
* **Anexo C: Segurança Operacional Detalhada (Defesa em Profundidade)**  
  * Especificações técnicas sobre o *sandbox* de execução (GKE Sandbox / gVisor) para isolar o código de IA "não confiável" 1 e o uso de políticas de rede L7 (Cilium / eBPF).1  
* **Anexo D: O "Fosso" de Domínio**  
  * Análise da convergência de expertise (Jurídica, *Deep-Tech* e Financeira) que levou ao pivô arquitetônico do Veritas 2.0 (distanciando-se do *hashing* de PII, uma falha de *compliance*).1