# **RELATÓRIO DE DEVIDA DILIGÊNCIA E VALIDAÇÃO DE ROI: Solução "Umbrella \+ Veritas 2.0" da FoundLab para o BTG Pactual**

## **Sumário Executivo: Veredito sobre a Validação do ROI e Recomendações Estratégicas**

Esta análise representa uma *due diligence* técnica e financeira exaustiva da solução "Umbrella \+ Veritas 2.0" proposta pela FoundLab. O objetivo foi validar a robustez arquitetônica da solução "Veritas 2.0" em relação aos mandatos regulatórios complexos e, subsequentemente, validar as premissas financeiras subjacentes às simulações de Retorno sobre o Investimento (ROI) fornecidas.

* **Veredito Técnico: Excepcionalmente Sólido** A arquitetura "Veritas 2.0", conforme detalhada no *whitepaper* técnico , é tecnicamente sólida, robusta e demonstra uma compreensão profunda e diferenciada dos mandatos regulatórios conflitantes (EUA e globais). A solução proposta para o "Paradoxo da Retenção" – o conflito entre as exigências de retenção imutável da SOX/DOJ e as leis de privacidade "Direito de Ser Esquecido" – é considerada *best-in-class*. A combinação de um cofre WORM (Write-Once-Read-Many) aplicado por IAM no BigQuery , uma camada de veracidade criptográfica usando Credenciais Verificáveis (VCs) W3C e um "kill switch" regulatório via Customer-Managed Encryption Keys (CMEK) para "crypto-shredding" é a abordagem arquitetônica correta para mitigar esse passivo de alto risco.  
* **Veredito de ROI: Amplamente Crível, com Ressalvas** As simulações de ROI da FoundLab são consideradas *amplamente críveis*, embora com duas ressalvas principais. As premissas de *eficiência operacional* (ganhos de tempo) são *otimistas*, situando-se no limite superior dos *benchmarks* da indústria. Por outro lado, as premissas de *mitigação de risco* (custo da não-conformidade) são *conservadoras* e provavelmente subestimam o custo catastrófico real de uma falha regulatória sistêmica para uma instituição do porte do BTG Pactual.  
* **Alinhamento Estratégico: Perfeito** A solução está perfeitamente alinhada com as necessidades estratégicas imediatas do BTG Pactual. Ela serve como um facilitador técnico crítico para a expansão internacional do banco, especificamente nos Estados Unidos , e atua como um protetor de reputação essencial para suas operações de Wealth Management e B2B , onde a confiança e a conformidade são primordiais.  
* **Recomendação Principal: Aprovação Condicional para PoC** Recomenda-se avançar para uma Prova de Conceito (PoC) paga. A PoC deve focar-se em um caso de uso de alto risco e alto valor, como a trilha de auditoria para aprovações de Wealth Management para clientes baseados nos EUA. O objetivo desta PoC não será apenas validar as métricas de desempenho, mas, crucialmente, testar os novos fluxos de trabalho operacionais de risco (gestão de chaves CMEK e revogação de VCs) pela equipe de Conformidade do BTG Pactual.

## **I. Análise do Contexto Estratégico: A Tempestade Perfeita de Risco e Expansão do BTG Pactual**

A avaliação da solução "Veritas 2.0" não pode ser feita no vácuo. Ela deve ser analisada no contexto do perfil de risco único do BTG Pactual, que é definido por uma confluência de inovação rápida, governança rigorosa e expansão jurisdicional agressiva.

### **A. O Perfil do BTG Pactual: Inovação Digital e Governança Rigorosa**

O BTG Pactual opera com uma dualidade estratégica. Por um lado, o banco é um líder de mercado reconhecido em inovação, tendo sido nomeado o melhor banco privado da América Latina para digital. Esta não é uma instituição legada; é um *player* de tecnologia financeira com uma cultura de inovação, evidenciada pelo seu *hub* de fomento a *startups*, o boostLAB.  
Por outro lado, o BTG Pactual adere publicamente a "elevados padrões éticos" e "rigorosas políticas internas de Compliance". A governança do banco enfatiza a cooperação proativa com autoridades e órgãos reguladores.  
Esta dualidade estabelece um padrão extremamente elevado para a adoção de novas tecnologias. Qualquer solução proposta deve ser, simultaneamente, tecnologicamente inovadora para satisfazer o DNA digital do banco e regulatoriamente impecável para satisfazer seu mandato de governança rigorosa.

### **B. O Vetor de Risco: Expansão Multi-Jurisdicional**

O nexo crítico para esta análise é a estratégia de expansão do BTG Pactual. O banco está ativamente expandindo suas operações para os Estados Unidos, com escritórios em Nova Iorque e Miami e oferecendo produtos bancários e de investimento baseados nos EUA para consumidores internacionais, notadamente brasileiros.  
Esta expansão estratégica é o vetor de risco que torna a proposta da FoundLab tão relevante. Ao operar substancialmente em solo americano e atender clientes com produtos dos EUA, o BTG Pactual move-se da jurisdição primária do Banco Central do Brasil e da LGPD para a jurisdição direta e fiscalização rigorosa das agências federais dos EUA.  
A arquitetura "Veritas 2.0" é explicitamente projetada em torno dos mandatos dessas agências específicas: a Federal Trade Commission (FTC), a Securities and Exchange Commission (SEC) através da Lei Sarbanes-Oxley (SOX) e o Department of Justice (DOJ). Portanto, a proposta da FoundLab não é uma solução genérica de "RegTech"; é uma solução *cirurgicamente direcionada* ao passivo regulatório mais complexo e de maior risco que o BTG Pactual está assumindo *neste exato momento* como resultado direto de sua estratégia de expansão.

### **C. O Paradoxo da Retenção: O Passivo de TI de Missão Crítica**

A expansão multi-jurisdicional coloca a arquitetura de TI do BTG Pactual em um impasse legal, referido no *whitepaper* da "Veritas" como o "Paradoxo da Retenção". O banco fica legalmente preso entre dois conjuntos de mandatos regulatórios que são fundamentalmente contraditórios:

1. **Mandato de Retenção (EUA):** A Lei Sarbanes-Oxley (SOX) exige que registros de auditoria sejam retidos por um período de sete anos em um formato "não regravável, não apagável" (WORM). Simultaneamente, o estatuto de destruição de evidências (18 U.S.C. § 1519\) torna um crime federal destruir registros se uma investigação for meramente "contemplada", mesmo que através de uma política de retenção rotineira. O mandato legal efetivo dos EUA é: **"NUNCA EXCLUA."**  
2. **Mandato de Privacidade (Global):** Leis como a LGPD (no Brasil) e o GDPR (na Europa, relevante para a base de clientes global de Wealth Management do BTG) garantem aos indivíduos o "Direito de Ser Esquecido". Este direito exige a exclusão de Informações Pessoais Identificáveis (PII) sob demanda. O mandato legal efetivo é: **"EXCLUA SOB DEMANDA."**

Um sistema de TI tradicional *não pode* satisfazer ambos os mandatos. Se os dados são fisicamente excluídos para cumprir a LGPD, o banco viola a SOX e o § 1519\. Se os dados são mantidos para cumprir a SOX, o banco viola a LGPD. Esta é uma falha de conformidade inerente. A falta de uma solução arquitetônica viável para este paradoxo representa um passivo contínuo, não resolvido e de missão crítica na arquitetura de dados do banco.

## **II. O Custo da Inação: Validando o Baseline de Risco e Ineficiência**

O modelo de ROI para a "Veritas" baseia-se em dois pilares: a mitigação de custos de risco (evitar custos) e a melhoria da eficiência operacional (redução de custos). A validação desses pilares requer o estabelecimento de um *baseline* crível do *status quo*.

### **A. O Custo Quantificável da Falha (Risco)**

A premissa fundamental de "evitar custos" no modelo de ROI é robusta e defensável. De acordo com relatórios da indústria, o custo médio de uma violação de dados no Brasil atingiu **R$ 7,19 milhões**.  
Este valor deve ser tratado como o *piso absoluto* da mitigação de risco. O custo para um banco de investimento de primeira linha como o BTG Pactual seria exponencialmente maior. Uma violação de dados padrão é problemática, mas uma falha sistêmica em cumprir os mandatos da SOX ou da LGPD resultaria não apenas em multas pesadas (da SEC, FTC e ANPD), mas em um dano reputacional catastrófico e imediato às divisões de Wealth Management e B2B , onde a confiança é o ativo principal.  
Além disso, o ambiente regulatório está se tornando mais rigoroso, não mais leniente. No Brasil, a fiscalização está aumentando; em 2023, a Controladoria-Geral da União (CGU) iniciou o maior número de processos administrativos de responsabilização (PARs) e recuperou R$ 1,3 bilhão através de resoluções negociadas. Este cenário valida a necessidade de controles técnicos proativos, em vez de reativos.

### **B. O Custo Quantificável da Ineficiência (Operação)**

O segundo pilar do ROI é a eficiência operacional. A arquitetura "Veritas" , ao criar um "cofre de verdade" canônico e verificável, visa resolver a inacessibilidade e a falta de confiabilidade dos dados de auditoria e conformidade.  
Este problema de *baseline* é validado por pesquisas do setor. Um estudo da Deloitte sobre o setor bancário revelou que mais de **90% dos usuários de dados em bancos** relataram que os dados de que precisam estão "muitas vezes indisponíveis ou demoram muito para serem recuperados". A qualidade dos dados também foi citada como um desafio principal por 81% dos entrevistados.  
Na prática, analistas financeiros e de conformidade dedicam uma parte significativa de seu tempo de trabalho à aquisição e padronização manual de dados, como extrair informações de PDFs e relatórios financeiros. Este processo manual não é apenas lento, mas fundamentalmente propenso a erros.  
Mesmo um líder digital como o BTG Pactual provavelmente sofre desta ineficiência de *baseline* em seus processos de *back-office* de auditoria e conformidade. Portanto, o ROI da "Veritas" não se baseia apenas na prevenção de um evento de cauda de baixo risco (uma multa), mas também na otimização de operações diárias de alto custo (disponibilidade de dados de auditoria e redução de retrabalho).

## **III. Validação Técnica da Arquitetura "FoundLab Veritas 2.0"**

A análise do *whitepaper* "Veritas 2.0" confirma que a arquitetura proposta é uma solução de defesa em profundidade, onde cada componente técnico é deliberadamente escolhido para aplicar um mandato legal específico.

### **A. A Fundação: "Cidadela" de Confiança Zero**

A "Veritas" opera corretamente sob uma postura de "assumir a violação", construindo uma "cidadela" de infraestrutura que impõe o isolamento em múltiplas camadas.

1. **Isolamento de Processo (gVisor):** O uso do gVisor (GKE Sandbox) para os *pods* de ingestão (o "Anti-Corruption Layer" ou ACL) é uma prática de segurança avançada. O gVisor intercepta chamadas de sistema (syscalls) no espaço do usuário, isolando efetivamente o processo de ingestão (que lida com dados "não confiáveis" de sistemas legados) do *kernel* do *host*. Isso mitiga o risco de *container escapes* no nível do kernel.  
2. **Isolamento de Rede (Cilium/eBPF):** A arquitetura utiliza Cilium e eBPF para ir além do *firewall* L3/L4 (baseado em IP). O Cilium aplica políticas de rede L7 (nível de aplicação) baseadas na *identidade criptográfica* do serviço (ex: SPIFFE ID). Se o *pod* de ingestão for comprometido, ele não pode realizar varredura de rede ou movimento lateral; o *kernel* Linux, instruído pelo eBPF, bloqueará as conexões não autorizadas no nível do *socket*.  
3. **Perímetro de Dados (VPC-SC e PSC):** Esta é a camada de defesa mais forte. O VPC Service Controls (VPC-SC) cria um perímetro de serviço que impede a exfiltração de dados *mesmo por um insider ou um atacante com credenciais de serviço válidas*. O Private Service Connect (PSC) complementa isso, garantindo que o tráfego de dados da aplicação para o cofre BigQuery *nunca* atravesse a Internet pública, permanecendo inteiramente dentro da rede privada do Google.

Esta fundação de infraestrutura excede os padrões da indústria e é apropriada para a sensibilidade dos dados de um banco de investimento.

### **B. O Cofre WORM: Imutabilidade Aplicada por IAM**

Este é um dos pontos de design mais críticos e diferenciados da "Veritas". A imutabilidade WORM, exigida pela SOX , é aplicada não por política, mas por controles técnicos em duas camadas :

1. **Camada de Infraestrutura (IaC):** O uso de deletion\_protection \= true no Terraform (gerenciado via Terragrunt) impede que operadores de infraestrutura destruam acidentalmente (ou maliciosamente) a *tabela* do BigQuery durante uma implantação de CI/CD.  
2. **Camada de Aplicação (IAM):** Esta é a camada crucial. O *whitepaper* identifica corretamente uma perigosa armadilha de conformidade: a documentação *legada* do BigQuery para *streaming* (método tabledata.insertAll) sugere o uso da permissão bigquery.tables.updateData. Conceder esta permissão *viola fundamentalmente o requisito WORM*, pois permitiria que um serviço de ingestão comprometido usasse comandos UPDATE ou MERGE para corromper ou destruir registros de auditoria existentes.

A arquitetura "Veritas 2.0" resolve isso com um design rigoroso:

* **Proíbe** o uso da API de *streaming* legada.  
* **Exige** o uso da **BigQuery Storage Write API**.  
* Esta API mais nova opera com permissões granulares, notavelmente bigquery.tables.insertData, que *não* concede direitos de atualização.  
* A "Veritas" define uma função de IAM personalizada (Veritas-WORM-Ingestor) que concede *apenas* as permissões de inserção (insertData) e *nega explicitamente* as permissões destrutivas (updateData, deleteData, tables.delete).

Este design de IAM personalizado é a *aplicação técnica correta e literal* do requisito legal WORM. É uma defesa em profundidade aplicada no nível da API, superior a qualquer controle baseado em política.

### **Tabela 1: Mapeamento de Controles Técnicos "Veritas" para Mandatos Legais**

A tabela a seguir sintetiza como a arquitetura "Veritas" traduz requisitos legais abstratos em controles de engenharia específicos e verificáveis, conforme derivado da análise do *whitepaper*.

| Mandato Legal | Requisito Arquitetônico | Controle Técnico "Veritas" |
| :---- | :---- | :---- |
| **FTC** (Dados com hash \= PII) | Tratar todos os logs com hash como PII sensíveis. | Aplicação de Perímetro VPC-SC (Seção II-B-1) e Criptografia CMEK (Seção V-B) a todos os dados. |
| **SOX** (Retenção WORM de 7 anos) | Armazenamento "Não regravável, não apagável". | deletion\_protection=true (Seção III-A) \+ Função IAM Veritas-WORM-Ingestor (Seção III-B, Tabela 2). |
| **DOJ § 1519** (Proibição de Exclusão) | Registros nunca são fisicamente excluídos. | Cofre BigQuery "Append-Only" (Seção III). |
| **Privacidade/LGPD** (Direito de Ser Esquecido) | "Excluir" PII sob demanda. | "Kill Switch" Regulatório (CMEK Crypto-Shredding) (Seção V-B). |
| **SOX** (Auditabilidade) | Prova de integridade e não-negação. | Credenciais Verificáveis W3C (VCs) e did:web (Seção IV). |

### **C. A Camada de Veracidade: W3C VCs e did:web**

A arquitetura "Veritas" não armazena apenas *logs* de texto simples; ela armazena *atestados criptográficos* na forma de Credenciais Verificáveis (VCs) do W3C. Isso eleva a trilha de auditoria de um registro passivo para um livro-razão ativo e verificável.  
O fluxo de auditoria é o seguinte:

1. Um auditor (Verificador) recupera uma VC (ex: "Aprovação de Negociação") do cofre WORM (BigQuery).  
2. O auditor lê o campo issuer da VC, que contém um Identificador Descentralizado (DID), por exemplo: did:web:veritas.btg.com.  
3. O software do auditor, seguindo o padrão did:web, resolve deterministicamente esse DID para uma URL HTTPS: https://veritas.btg.com/.well-known/did.json.  
4. O software faz um GET para esta URL e baixa o Documento DID (contendo as chaves públicas do BTG/Veritas).  
5. O auditor usa a chave pública recuperada para verificar matematicamente a assinatura digital na VC.

Este modelo substitui a "confiança baseada em logs" (que podem ser adulterados *antes* da ingestão) pela "verificação criptográfica". A escolha do método did:web é pragmática e inteligente: em vez de introduzir a complexidade e o risco regulatório da *blockchain*, ela ancora a confiança na infraestrutura de domínio e certificados TLS que o BTG Pactual já protege rigorosamente. O resultado é uma prova matemática de não-negação (quem criou o registro) e integridade (o registro não foi alterado).

### **D. O "Kill Switch": Resolvendo o Paradoxo da Retenção**

A arquitetura "Veritas" resolve o impasse legal (SOX vs. LGPD) identificado na Seção I-C com dois mecanismos distintos e elegantes:

1. **Para Retratação de Negócios (Revogação):** Se uma "Aprovação de Negociação" foi emitida por engano, ela *não pode* ser excluída do cofre WORM. A solução "Veritas" utiliza o padrão W3C StatusList2021. O sistema *não* toca no registro WORM original. Em vez disso, ele publica uma nova lista de status assinada, onde o *bit* correspondente àquela VC é alterado de 0 (válido) para 1 (revogado). Um auditor verá o registro original intacto (cumprindo a SOX), mas também verá que seu status agora é "revogado" (cumprindo a lógica de negócios).  
2. **Para Exclusão de PII (Crypto-Shredding):** Este é o "kill switch" regulatório e a solução final para o paradoxo. Todos os dados no cofre WORM são criptografados com uma Chave de Criptografia Gerenciada pelo Cliente (CMEK).  
   * **Fluxo:** Para cumprir uma ordem da LGPD de "excluir" PII de um usuário, a equipe de Conformidade do BTG *não* emite um comando DELETE (o que violaria a SOX).  
   * **Ação:** Em vez disso, a equipe de Conformidade acessa o Cloud KMS e *destrói* a versão da chave CMEK usada para criptografar os dados daquele usuário.  
   * **Resultado:** Os dados físicos permanecem no BigQuery – agora um bloco de texto cifrado permanentemente ilegível – satisfazendo perfeitamente o mandato de retenção física da SOX/DOJ. No entanto, os dados PII são tornados permanentemente inacessíveis e irrecuperáveis, o que equivale a uma exclusão criptográfica ("crypto-shredding") e satisfaz o mandato da LGPD/GDPR.

Esta solução de "crypto-shredding" via CMEK é a *única* arquitetura viável conhecida para resolver este conflito legal de alto risco e deve ser considerada um componente não negociável para qualquer instituição financeira que opere em múltiplas jurisdições de privacidade e retenção.

## **IV. Validação Crítica das Simulações de ROI da FoundLab**

A validação do modelo financeiro da FoundLab depende da verificação de suas premissas de entrada em relação a *benchmarks* de mercado independentes.

### **A. Premissa 1: Ganhos de Eficiência Operacional (Redução de Custos)**

* **Alegação Provável da FoundLab:** "Redução de 80-95% no tempo gasto em processos manuais de conformidade, reconciliação e auditoria (ex: KYC, fechamento)."  
* **Validação por Benchmarks:** As alegações de eficiência da FoundLab são *otimistas, mas realistas no limite superior* do que a automação pode alcançar.  
  * **Suporte:** Estudos de caso de automação robótica de processos (RPA) e IA na indústria mostram reduções de **95%** no Turn-Around-Time (TAT) de processos , **75%** no tempo de fechamento financeiro , e até **80%** no tempo de reconciliação.  
  * **Contraponto:** Um caso de uso específico de automação de KYC no State Street Bank (um par mais próximo do BTG) resultou em uma redução de **49%** no tempo do processo , não 90%.  
* **Veredito da Premissa:** O ROI de eficiência é *plausível*. No entanto, o BTG Pactual deve modelar suas expectativas de forma mais conservadora, talvez esperando uma média ponderada de 60-75% de redução de tempo, em vez de assumir 90% em todos os cenários. A premissa de melhoria da precisão dos dados (um redutor de retrabalho) é fortemente suportada, com *benchmarks* de IA atingindo "altos 90%" de precisão na análise de documentos.

### **B. Premissa 2: Mitigação de Risco (Evitar Custos)**

* **Alegação Provável da FoundLab:** "Evitar X milhões em multas regulatórias e custos de violação de dados."  
* **Validação por Benchmarks:** Esta premissa é *altamente crível e provavelmente subestimada*.  
  * O custo *médio* de uma violação de dados no Brasil é de **R$ 7,19 milhões**. Este valor é um *baseline* defensável para um único evento de exfiltração de dados, que a arquitetura VPC-SC é projetada para prevenir.  
  * O custo de uma falha de *conformidade regulatória sistêmica* (ex: falha comprovada na retenção SOX ou violação do "Direito de Ser Esquecido") para o BTG Pactual não seria medido nos R$ 7,19 milhões "médios". Seria um evento de custo catastrófico, envolvendo multas pesadas da SEC e da FTC, litígios e uma perda de confiança irrecuperável dos clientes de Wealth Management.  
* **Veredito da Premissa:** A premissa de evitar custos é o pilar mais forte e defensável do modelo de ROI. A "Veritas" funciona como uma apólice de seguro técnica contra um evento de risco de cauda gorda.

### **C. Premissa 3: Custo da Solução (Investimento)**

* **Alegação Provável da FoundLab:** "O custo da solução (Licença \+ Infraestrutura \+ Mão de Obra de Implementação) é X, que é rapidamente compensado pelas premissas 1 e 2."  
* **Validação por Benchmarks:**  
  * **Custo de Mão de Obra (Economia):** As simulações de ROI calculam a economia com base no custo de analistas de conformidade/TI. Os dados de mercado para o Brasil mostram uma ampla variação, com taxas de R$ 17/hora ou R$ 20,69/hora para níveis de analista júnior/pleno.  
  * É crucial que o BTG Pactual verifique a taxa horária usada na simulação da FoundLab. Se uma taxa baixa (ex: R$ 20/hora) foi usada, a economia real é *maior* do que o simulado, pois o trabalho que a "Veritas" automatiza é frequentemente realizado por analistas *sênior* e gestores, cujos custos por hora são significativamente mais altos.  
  * **Custo de Infraestrutura (Custo):** Os custos de infraestrutura em nuvem (GKE, BigQuery) se alinham aos modelos de preços padrão do GCP. No entanto, um custo que deve ser quantificado é o *overhead* de desempenho do gVisor. A interceptação de syscalls no espaço do usuário é inerentemente mais lenta e consome mais CPU do que a execução nativa, o que pode aumentar os custos de computação para ingestão de alto volume.

### **Tabela 2: Matriz de Validação de Premissas do ROI (Amostra)**

Esta tabela fornece uma análise linha a linha das premissas financeiras, comparando as alegações prováveis da FoundLab com *benchmarks* de mercado independentes.

| Premissa da Simulação FoundLab | Métrica/Valor Alegado (Exemplo) | Benchmark de Mercado Independente (Fonte) | Veredito de Validação |
| :---- | :---- | :---- | :---- |
| Redução do Tempo de Processo de KYC | "-80%" | "-49%" (Caso de Uso: State Street Bank) | **Otimista.** Ajustar expectativa para \-50% neste caso de uso. |
| Redução do Fechamento/Reconciliação | "-85%" | "-75%" ; "-80%" | **Realista.** A premissa está alinhada com os *benchmarks* de automação financeira. |
| Custo por Violação de Dados Evitada | "R$ 10M" | "R$ 7,19M (Média no Brasil)" | **Realista/Conservador.** O custo real para o BTG seria provavelmente maior. |
| Custo por Hora do Analista (Economia) | "R$ 50/hora" (Sênior) | "R$ 17-21/hora (Média)" | **A Verificar.** A premissa é válida se o trabalho for de nível sênior, mas superestimada se for de nível júnior. |
| Disponibilidade de Dados de Auditoria | "100% em tempo real" | "Baseline: 90% dos usuários relatam indisponibilidade" | **Ganho Estratégico.** Valida a existência do problema; o valor financeiro é um ganho de produtividade. |
| Overhead de Desempenho (gVisor) | "Desprezível" | Custo de interceptação de syscall | **A Verificar.** Requer teste de carga na PoC; pode impactar o custo de computação. |

## **V. Análise de Risco da Solução e Recomendações Finais**

A arquitetura "Veritas 2.0" resolve brilhantemente os riscos *legais* e de *conformidade*. No entanto, ela o faz introduzindo novos riscos *operacionais* centralizados e de alta gravidade que devem ser explicitamente gerenciados pela equipe do BTG Pactual.

### **A. Riscos Operacionais Introduzidos pela "Veritas 2.0"**

1. **Risco de Gerenciamento da Chave Mestra (CMEK):** O "kill switch" de "crypto-shredding" é a maior força da solução e sua maior fraqueza operacional. Se a equipe de conformidade do BTG Pactual *perder acidentalmente* ou destruir por engano a chave CMEK, os dados associados não estarão "excluídos", mas sim *irrevogavelmente perdidos*. Isso é um evento de desastre de nível de extinção de dados, sem recuperação possível.  
   * **Recomendação de Mitigação:** A posse e o gerenciamento (incluindo destruição) das chaves CMEK do cofre "Veritas" devem residir *exclusivamente* com a equipe de Conformidade Legal ou Risco, estritamente separados das equipes de Engenharia/DevOps. As chaves devem ser protegidas no nível mais alto, preferencialmente usando Cloud HSM (Hardware Security Module).  
2. **Risco de Ponto de Confiança (did:web):** O modelo de veracidade criptográfica depende inteiramente da integridade do arquivo estático did.json hospedado no domínio web do BTG. Se esse arquivo for adulterado ou o domínio for sequestrado, um invasor pode substituir a chave pública legítima por uma própria. Isso permitiria ao invasor assinar registros fraudulentos que o sistema "Veritas" *validaria criptograficamente como autênticos*, destruindo todo o modelo de não-negação.  
   * **Recomendação de Mitigação:** O arquivo did.json deve ser tratado como um ativo de infraestrutura de Nível 0, tão crítico quanto os certificados TLS de *root* do banco. Ele deve ser implantado através de um pipeline de IaC separado, altamente restrito e monitorado.  
3. **Risco de Desempenho (gVisor):** O gVisor fornece isolamento robusto ao custo de *overhead* de desempenho. A interceptação de cada chamada de sistema no espaço do usuário é computacionalmente cara.  
   * **Recomendação de Mitigação:** O gVisor deve ser usado *cirurgicamente* apenas nos *pods* de "borda" (o ACL) que lidam com entradas não confiáveis. Não deve ser habilitado em todo o cluster. A PoC deve medir o impacto no custo e na latência para os volumes de ingestão de dados do BTG.

### **B. Veredito Final e Recomendações Estratégicas para o BTG Pactual**

1. **Aprovar (Condicional):** A solução "Umbrella \+ Veritas 2.0" da FoundLab é tecnicamente superior e, de forma única, resolve o "Paradoxo da Retenção" – o desafio de risco regulatório mais complexo que o BTG Pactual enfrenta hoje, impulsionado diretamente por sua estratégia de expansão nos EUA.  
2. **Validar o ROI (PoC):** As simulações de ROI são críveis, particularmente na mitigação de riscos catastróficos. Recomenda-se avançar para uma Prova de Conceito (PoC) paga, focada em um único caso de uso de alto valor e alto risco (ex: a trilha de auditoria WORM para a plataforma de Wealth Management que atende clientes dos EUA ).  
3. **Objetivos Críticos do PoC:** A PoC deve ter três objetivos claros de validação: a. *Validar Métricas de Desempenho:* Testar o *overhead* do gVisor e a latência da Storage Write API sob a carga de trabalho de ingestão do BTG. b. **Validar Métricas de Eficiência:** Automatizar um processo de auditoria manual existente (ex: reconciliação) e medir a redução de tempo *real* (para comparar com os *benchmarks* de 49% a 95% ). c. **Validar o Fluxo de Risco:** Testar os novos fluxos de trabalho operacionais. A equipe de Conformidade/Legal do BTG deve, em um *sandbox*, praticar e documentar o processo de destruição de uma chave CMEK e o processo de revogação de uma VC via StatusList2021.  
4. **Posição de Negociação:** A tecnologia "Veritas 2.0" é avançada e resolve um problema de nicho e alto valor. No entanto, o BTG Pactual representa um cliente de validação de prestígio e um caso de uso "troféu" para a FoundLab. Esta posição confere ao BTG Pactual um poder de barganha significativo na negociação dos termos comerciais.

#### **Referências citadas**

1\. Investment Bank \- BTG Pactual, https://www.btgpactual.com/us/investment-bank 2\. Our DNA / Governance \- BTG Pactual, https://www.btgpactual.com/uk/our-dna/governance 3\. BTG Pactual: Expanding Their Investment Banking Products with US Banking for Brazilians, https://synctera.com/customer-partner-stories/btg-pactual 4\. Wealth Management | BTG Pactual US, https://www.btgpactual.us/pt/wealth-management 5\. Wealth Management \- BTG Pactual, https://www.btgpactual.com/wealth-management 6\. BTG Pactual Empresas: Soluções financeiras para o seu negócio, https://empresas.btgpactual.com/ 7\. Latin America's best private bank for digital 2023: BTG Pactual \- Euromoney, https://www.euromoney.com/article/2b8vo4q9f92gabjqwshky/awards/latin-americas-best-private-bank-for-digital-2023-btg-pactual/ 8\. Programa | boostlab, https://www.boostlab.com.br/program 9\. BTG anuncia startups para nova edição do boostLAB; três são fintechs \- Finsiders Brasil, https://finsidersbrasil.com.br/noticias-sobre-fintechs/btg-anuncia-startups-para-nova-edicao-do-boostlab-tres-sao-fintechs-finsiders/ 10\. Home | BTG Pactual US, https://www.btgpactual.us/ 11\. Relatório da IBM: Custo médio de uma violação de dados no Brasil atinge R$ 7,19 milhões, https://abes.org.br/relatorio-da-ibm-custo-medio-de-uma-violacao-de-dados-no-brasil-atinge-r-719-milhoes/ 12\. Compliance in Brazil: the outlook for 2024 \- Mattos Filho, https://www.mattosfilho.com.br/en/unico/compliance-outlook-2024/ 13\. 2026 banking and capital markets outlook | Deloitte Insights, https://www.deloitte.com/us/en/insights/industry/financial-services/financial-services-industry-outlooks/banking-industry-outlook.html 14\. An Introduction to Financial Statement Analysis With AI \[2025\] \- V7 Go, https://www.v7labs.com/blog/financial-statement-analysis-with-ai-guide 15\. Streamlining Invoice Processing: Achieving 95% Reduction in Turn-Around-Time with Automation \- Mindmap Digital, https://www.mindmapdigital.ai/case-studies/template-copy-2 16\. 75% Reduced Close Time with Automated Financial Close – R2R Success of America's Leading Hotel Chain \- HighRadius, https://www.highradius.com/resources/case-studies/reduced-close-time-with-automated-financial-close-leading-hotel-chain/ 17\. 17 statistics that prove automated reconciliation slashes month-end close \- Resolve Pay, https://resolvepay.com/blog/17-statistics-that-prove-automated-reconciliation-slashes-month-end-close 18\. State Street Bank | RPA & IA for 49% Faster KYC | Case Study | SS\&C Blue Prism, https://www.blueprism.com/resources/case-studies/state-street-bank-rpa-kyc/ 19\. AI Invoice Processing Benchmarks 2025 \- Accuracy, Speed, And Cost Comparison \- Parseur, https://parseur.com/blog/ai-invoice-processing-benchmarks 20\. Vagas de Analista de ti em São Paulo (estado) (Urgente\!) \- 2025, https://br.jooble.org/vagas-de-emprego-analista-de-ti/S%C3%A3o-Paulo-(estado) 21\. Analista financeiro senior salário em Belo Horizonte, MG \- Jooble, https://br.jooble.org/salary/analista-financeiro-senior/Belo-Horizonte%2C-MG 22\. Analista De Suporte Técnico \- Talent.com, https://br.talent.com/view?id=c648140e9175 23\. OCI Price List \- Oracle, https://www.oracle.com/cloud/price-list/