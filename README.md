## Draw io link
* https://app.diagrams.net/#G1f0UWbymXDkLwG26AsF7Y8095WguSz6wk#%7B%22pageId%22%3A%22UNnTjreAtW9Vjduv4I7x%22%7D

## Contexto

Você foi contratado para liderar a arquitetura de um novo sistema de pagamentos escalável e resiliente, totalmente baseado em **microsserviços escritos em GoLang**, hospedado em **AWS**, e utilizando **eventos assíncronos** entre os serviços.

O sistema será responsável por processar **até 6000 transações por segundo**, com foco em:

- Alta disponibilidade
- Transações distribuídas (padrão **SAGA**)
- Integridade e consistência dos dados
- Garantia de **unicidade de pagamentos**
- **Idempotência** em cada etapa do fluxo

---

## Fluxo de Pagamento

Cada pagamento percorre os seguintes serviços:

1. **Validação** da solicitação de pagamento  
2. **Autorização** (serviço principal da orquestração)  
3. **Registro contábil**  
4. **Notificação por evento** 
5. **Verificação de integridade** (serviço que valida a consistência final das sagas)

Cada microserviço deve emitir **eventos** após executar sua função. O **serviço de integridade** escuta os eventos e garante que todas as etapas foram executadas corretamente ou realiza compensações, se necessário.

---

## Requisitos Funcionais

- Pagamentos iniciados via API devem ser processados com rastreabilidade total.
- Cada microserviço deve ser desacoplado, escalável e resiliente.
- Todos os eventos devem ser rastreados e persistidos para auditoria.
- O mesmo pagamento **nunca** deve ser processado mais de uma vez.
- O sistema deve ser capaz de **compensar** etapas em caso de falha parcial.

---

## Requisitos Não Funcionais

- Alta disponibilidade (99.99%)
- Escalabilidade horizontal para suportar **6000 TPS**
- Resiliência a falhas e consistência eventual
- Deploy 100% em **AWS**
- Microsserviços escritos em **GoLang**

---

## Stack Esperada (AWS Cloud-Native)

- **GoLang** para todos os microsserviços
- **Cloud Native - Amazon AWS

---

## Desafio para o(a) Candidato(a)

### 1. Desenho da Arquitetura
- Diagrama de alto nível
- Fluxo de eventos entre os serviços
- Destaque do **serviço de autorização** como coordenador

### 2. Modelo de SAGA
- Escolha entre coreografia ou orquestração
- Descreva a estratégia de compensação 

### 3. Idempotência e Unicidade
- Estratégia para prevenir duplicidade de pagamento
- Como aplicar idempotência com DynamoDB e GoLang

### 4. Escalabilidade e Alta Disponibilidade
- Estratégias para atingir 6000 TPS
- Tolerância a falhas de serviços individuais

### 5. Serviço de Integridade
- Como monitora e repara sagas incompletas
- Ações em caso de inconsistência detectada

### 6. Observabilidade
- Ferramentas e abordagens para tracing e logs distribuídos

### 7. Extras (bônus)
- Como realizar deploys sem downtime
- Como versionar e validar contratos de eventos entre os serviços

---

## Critérios de Avaliação

- Clareza e solidez da arquitetura proposta
- Coerência com os requisitos
- Estratégias para idempotência e unicidade
- Design e papel do serviço de integridade
- Argumentação técnica com foco em escalabilidade, segurança e consistência
