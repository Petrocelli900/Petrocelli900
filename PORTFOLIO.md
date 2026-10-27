# Portfólio técnico · João Petrocelli

Seleção de projetos em Java e Python com foco em fundamentos de engenharia. Cada projeto inclui código executável, testes, verificação automática e um documento de decisões técnicas.

## 01 · Reservas de estoque — Java

**Problema:** requisições simultâneas não podem reservar mais unidades do que existem.

**Implementação:** monitor único torna consulta e débito atômicos; uma chave de idempotência identifica o payload; estados finais impedem devolução duplicada de estoque.

**Verificação:** 100 tentativas concorrentes disputam 10 unidades. O cenário exige exatamente 10 sucessos e saldo final zero. Também há testes de repetição, transições inválidas e overflow.

**Compromisso:** lock global simplifica a correção em uma instância, com menor paralelismo. Não há persistência nem coordenação entre processos.

[Repositório](https://github.com/Petrocelli900/inventory-reservations-java) · [Decisões](https://github.com/Petrocelli900/inventory-reservations-java/blob/main/docs/decisions.md)

## 02 · Livro financeiro — Java

**Problema:** lançamentos precisam manter precisão decimal e não podem ser duplicados ao repetir uma operação.

**Implementação:** records imutáveis, BigDecimal com duas casas, identificadores idempotentes, relatórios por mês e categoria e exportação CSV.

**Verificação:** soma de 0,10 e 0,20, isolamento entre meses, conflito de identificadores, valores inválidos e escape de texto em CSV.

**Compromisso:** uma moeda implícita por livro e armazenamento em memória. Não implementa contabilidade fiscal, câmbio ou estorno.

[Repositório](https://github.com/Petrocelli900/expense-ledger-java) · [Decisões](https://github.com/Petrocelli900/expense-ledger-java/blob/main/docs/decisions.md)

## 03 · Fila de tarefas — Java

**Problema:** tarefas com falha precisam aguardar antes da próxima tentativa, e uma resposta antiga não pode concluir a tentativa atual.

**Implementação:** aquisição atômica, Clock injetável, atraso fixo, limite de tentativas e token de tentativa para conclusão.

**Verificação:** relógio controlado sem sleep, limite de tentativas, respostas atrasadas e aquisição concorrente de uma única tarefa.

**Compromisso:** sem persistência e sem recuperação automática de tarefas RUNNING quando um consumidor morre.

[Repositório](https://github.com/Petrocelli900/task-queue-java) · [Decisões](https://github.com/Petrocelli900/task-queue-java/blob/main/docs/decisions.md)

## 04 · Qualidade de dados — Python

**Problema:** arquivos CSV podem conter dados inválidos, campos ausentes ou duplicados antes de uma importação.

**Implementação:** esquema explícito, validação de tipos, obrigatoriedade e unicidade. CLI retorna JSON e códigos de saída para automação.

**Verificação:** seis testes, incluindo cabeçalhos inválidos, campos multilinha, decimais não finitos e códigos de saída.

**Compromisso:** memória cresce com valores únicos e problemas encontrados; validação de e-mail é apenas sintática.

[Repositório](https://github.com/Petrocelli900/data-quality-python) · [Decisões](https://github.com/Petrocelli900/data-quality-python/blob/main/docs/decisions.md)

## 05 · Análise de logs — Python

**Problema:** obter indicadores básicos de requisições a partir de logs JSON Lines.

**Implementação:** contagem de requisições e eventos inválidos, taxa HTTP 5xx, percentil nearest-rank p95 e agrupamento por caminho sem query string.

**Verificação:** cinco testes cobrem percentil, entradas inválidas, dados vazios, agregação e CLI.

**Compromisso:** guarda durações em memória; não anonimiza informações no caminho nem substitui observabilidade em produção.

[Repositório](https://github.com/Petrocelli900/log-insights-python) · [Decisões](https://github.com/Petrocelli900/log-insights-python/blob/main/docs/decisions.md)

## 06 · API de tarefas — Python

**Problema:** criar, listar e concluir tarefas por HTTP com dados preservados entre execuções.

**Implementação:** servidor local, SQLite transacional com parâmetros SQL, paginação limitada e validação JSON.

**Verificação:** três testes com múltiplas verificações, incluindo servidor HTTP real em porta efêmera, persistência, erros e conteúdo semelhante a injeção SQL tratado como dado.

**Compromisso:** demonstração em localhost, sem autenticação, TLS, migrações ou exclusão.

[Repositório](https://github.com/Petrocelli900/sqlite-task-api-python) · [Decisões](https://github.com/Petrocelli900/sqlite-task-api-python/blob/main/docs/decisions.md)

---

Implementações iniciais criadas com assistência de IA. Este portfólio registra projetos de estudo e não atribui experiência profissional ou resultados de produção a essas demonstrações.
