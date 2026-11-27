# Uma Arquitetura de Referência para Frameworks de Orquestração de Agentes de IA

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24573327.svg)](https://doi.org/10.5281/zenodo.24573327)

Pacote de replicação do Trabalho de Conclusão de Curso (Monografia em Sistemas de Informação II) de **Bernardo Viggiano Campos**, Bacharelado em Sistemas de Informação, Departamento de Ciência da Computação, Universidade Federal de Minas Gerais (UFMG).

Orientador: Prof. Marco Túlio Valente.

## Sobre o trabalho

O trabalho propõe uma arquitetura de referência para frameworks de orquestração de agentes de IA, com 4 dimensões, 12 componentes e 16 decisões arquiteturais, e a instancia em quatro frameworks: **n8n**, **LangGraph**, **CrewAI** e **OpenAI Agents SDK (Python)**. A instanciação se baseia na análise da documentação e do código-fonte de cada framework em revisões fixadas, e produziu **64 registros** (16 decisões × 4 frameworks), sustentados por 150 evidências de código.

Este repositório contém os registros, para que cada afirmação do texto possa ser conferida no código.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `registros-64.csv` | Os 64 registros de análise, com uma linha por evidência de código (150 linhas). |
| `README.md` | Este arquivo. |

## Revisões analisadas

Todas as evidências apontam para os commits abaixo. Para reproduzir a análise, use esses commits, e não as tags públicas: as tags n8n 2.41.0 e CrewAI 1.15.28 apontam para commits diferentes dos analisados.

| Framework | Repositório | Versão | Commit |
|---|---|---|---|
| n8n | [n8n-io/n8n](https://github.com/n8n-io/n8n) | 2.41.0 (declarada no `package.json`) | `2f2bac4645472e5efc72c4efedaadff6ef50348e` |
| LangGraph | [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 1.2.13 | `2d942085e214ef6b99b6f54ed4d544a7c7c5ac56` |
| CrewAI | [crewAIInc/crewAI](https://github.com/crewAIInc/crewAI) | 1.15.28 (declarada no código) | `65cdd70ac0fc0ba93c553fa30d3dd13a498559e2` |
| OpenAI Agents SDK | [openai/openai-agents-python](https://github.com/openai/openai-agents-python) | 0.24.0 | `17d994bd3045dae71acda676a4ef4762ed8ecd94` |

## Dicionário de dados de `registros-64.csv`

O arquivo usa codificação UTF-8 e vírgula como separador.

| Coluna | Descrição |
|---|---|
| `decisao` | Identificador da decisão arquitetural (D01 a D16). |
| `nome_decisao` | Nome da decisão (por exemplo, "Delegação entre Agentes"). |
| `framework` | Framework analisado. |
| `registro` | Identificador do registro: N (n8n), L (LangGraph), CR (CrewAI) ou OA (OpenAI Agents SDK), seguido do número da decisão. Exemplo: CR14. |
| `alternativa_tabela_resumo` | Alternativa adotada pelo framework para a decisão, como resumida no texto. |
| `simbolo` | Classe, função ou método que sustenta a evidência. |
| `repositorio` | Repositório no GitHub. |
| `commit` | Commit analisado (hash completo). |
| `caminho` | Caminho do arquivo no repositório. |
| `linha_inicial`, `linha_final` | Intervalo de linhas da evidência no commit. |
| `permalink` | Link fixo para o trecho de código. |
| `tipo_evidencia` | Implementação executável, contrato de API ou configuração. |
| `camada` | Núcleo do framework, integração de suporte ou composição da aplicação. |
| `documentacao` | Chaves das referências de documentação usadas no texto. |
| `sintese_do_registro` | Síntese do registro, como apresentada no texto. |

Um registro pode ter mais de uma linha, uma por evidência de código.

## Critérios de classificação

**Tipo de evidência**

| Valor | Critério | Exemplos |
|---|---|---|
| Implementação executável | Trecho com lógica executada pelo runtime (corpo de função ou método). | `Pregel.stream`, `Flow._resume_async_body`, `processHitlResponses` |
| Contrato de API | Declaração de tipos, classes de dados, interfaces, classes base ou assinaturas que definem o que a aplicação ou outros módulos fornecem e recebem. | `Command`, `Checkpoint`, `BaseStore`, `RunContextWrapper`, `INodeExecutionData` |
| Configuração | Parâmetro ou estrutura que regula o comportamento sem implementá-lo. | `RetryPolicy`, `ToolExecutionConfig`, `batchSize`, `onError` |

**Camada**

| Valor | Critério | Exemplos |
|---|---|---|
| Núcleo | Mecanismos de orquestração do framework: motor de execução, agentes, ferramentas, estado, aprovação, políticas e rastreamento. | `WorkflowExecute`, `StateGraph`, `Crew`, `AgentRunner` |
| Integração de suporte | Adaptadores para protocolos ou serviços externos, implementações de backends de armazenamento e extensões opcionais. | `HttpRequestV3`, clientes MCP, `InMemorySaver`, `SQLiteSession`, `MemoryPostgresChat`, memória do sandbox |

A camada "composição da aplicação", citada no texto, não aparece no arquivo: ela descreve responsabilidades que ficam com quem usa o framework (por exemplo, idempotência e autenticação do revisor), e não trechos do código dos frameworks.

Resultado: 122 evidências de implementação executável, 24 de contrato de API e 4 de configuração; 138 no núcleo e 12 em integração de suporte.

## Decisões arquiteturais

| Dimensão | Decisões |
|---|---|
| Controle e Orquestração | D01 Modelo de orquestração; D02 Fluxo de controle; D03 Coordenação multiagente; D04 Delegação entre agentes; D05 Concorrência e paralelismo; D06 Tratamento de falhas e recuperação |
| Ferramentas e Integração | D07 Invocação de ferramentas; D08 Integração externa |
| Estado, Memória e Contexto | D09 Gerenciamento de estado; D10 Persistência e pontos de verificação; D11 Retomada da execução; D12 Memória; D13 Propagação e escopo de contexto |
| Governança e Observabilidade | D14 Intervenção humana; D15 Políticas e salvaguardas; D16 Observabilidade e rastreamento |

## Limitações

- Os registros descrevem o código nos commits indicados. Versões posteriores podem se comportar de outra forma.
- A documentação do n8n e do LangGraph não tem versão fixada e pode ter mudado desde o acesso.
- A análise foi feita por um único pesquisador e não inclui a execução da aplicação comum descrita no texto.

## Como citar

Pacote de replicação (este repositório):

> CAMPOS, Bernardo Viggiano. *Uma Arquitetura de Referência para Frameworks de Orquestração de Agentes de IA: pacote de replicação*. Versão v1.0.0. Zenodo, 2026. DOI: [10.5281/zenodo.24573327](https://doi.org/10.5281/zenodo.24573327).

Trabalho de Conclusão de Curso:

> CAMPOS, Bernardo Viggiano. *Uma Arquitetura de Referência para Frameworks de Orquestração de Agentes de IA*. Trabalho de Conclusão de Curso (Bacharelado em Sistemas de Informação), Universidade Federal de Minas Gerais, Belo Horizonte, 2026.

## Licença

Os dados deste repositório estão disponíveis sob a licença [Creative Commons Atribuição 4.0 Internacional (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.pt_BR). Os trechos de código referenciados pertencem aos respectivos projetos e seguem suas próprias licenças.
