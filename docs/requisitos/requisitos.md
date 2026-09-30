# REQUISITOS DO FUBÁ — BETA/MVP V1

## 1. GERENCIAMENTO DE USUÁRIOS E ACESSO

### RF01 — Cadastrar usuário

O sistema deve permitir que um usuário com permissão administrativa cadastre novos usuários, definindo seus dados necessários e seu perfil de acesso.

Os perfis da V1 são:

- Root
- Gestor
- Inspetor
- Consultor

### RF02 — Controlar acesso por perfil

O sistema deve permitir que cada usuário execute somente as funcionalidades autorizadas para seu perfil.

O Root possui acesso às funcionalidades administrativas e às demais funcionalidades do sistema.

### RF03 — Realizar primeiro acesso

O sistema deve permitir que um usuário previamente cadastrado realize seu primeiro acesso utilizando as credenciais fornecidas no cadastro.

No primeiro acesso, o usuário deve completar/atualizar seus dados de perfil e definir suas credenciais para os acessos posteriores.

### RF04 — Criar usuário Root inicial

Na primeira inicialização do sistema, o sistema deve criar automaticamente o usuário Root inicial.

## 2. CADASTRO E GERENCIAMENTO DE AMOSTRAS

### RF05 — Cadastrar amostra

O sistema deve permitir que um Inspetor cadastre uma amostra de açúcar relacionada a uma operação do terminal.

O cadastro deve armazenar as informações necessárias para identificar a amostra, a operação, o responsável e seus resultados de análise.

### RF06 — Registrar dados da amostra

O sistema deve permitir registrar, conforme o tipo de operação, os dados definidos para a amostra:

#### Dados gerais

- data
- hora
- Inspetor responsável

#### Resultados

- umidade (%)
- impurezas (%)

Quando não houver impurezas, o percentual registrado deve ser 0.

#### Recebimento por trem

- de 1 a 4 números de vagões
- armazém de destino
- lacre

#### Embarque por navio

- nome do navio
- armazém de origem
- parcial
- um ou mais lacres

Os vagões, o parcial e os armazéns representam informações relacionadas à amostra/operação e não constituem, por si só, um cadastro independente na V1.

### RF07 — Identificar amostra internamente

O sistema deve atribuir uma identificação interna única a cada amostra cadastrada, utilizada para identificar o registro no sistema.

Essa identificação é independente dos números de lacre utilizados fisicamente.

## 3. FLUXO DE APROVAÇÃO

### RF08 — Submeter amostra para aprovação

Ao concluir o cadastro de uma nova amostra, o sistema deve colocá-la no status “aguardando aprovação”.

A amostra deve ficar disponível para análise do Gestor.

### RF09 — Alterar amostra não aprovada

Enquanto a amostra não estiver aprovada, o Inspetor responsável deve poder alterar seus dados.

Após a alteração, a amostra deve continuar ou retornar ao fluxo de aprovação.

### RF10 — Solicitar alteração

O Gestor deve poder solicitar alteração de uma amostra quando identificar uma inconsistência.

A solicitação deve exigir uma observação/justificativa.

Ao solicitar a alteração, o status da amostra deve passar para “alteração solicitada”.

### RF11 — Visualizar solicitação de alteração

O Inspetor deve poder visualizar a observação registrada pelo Gestor ao abrir uma amostra cuja alteração foi solicitada.

### RF12 — Corrigir amostra

O Inspetor deve poder corrigir uma amostra que esteja com status “alteração solicitada”.

Após a correção e o salvamento, a amostra deve retornar ao status “aguardando aprovação”.

### RF13 — Aprovar amostra

O Gestor deve poder aprovar uma amostra após verificar que seus dados estão corretos.

Após a aprovação:

- a amostra deve deixar de aparecer na fila de pendências;
- a amostra não deve permanecer livremente editável;
- a amostra deve ficar disponível para consulta conforme as permissões de cada perfil.

### RF14 — Solicitar nova alteração de amostra aprovada

O sistema deve permitir que o Gestor solicite posteriormente uma nova alteração em uma amostra já aprovada, fazendo com que ela retorne ao fluxo de correção e aprovação.

> Observação: o mecanismo exato de reabertura ainda é uma decisão que deverá ser detalhada nas regras de negócio.

## 4. CONSULTA

### RF15 — Consultar amostras

O sistema deve permitir que usuários autorizados consultem as amostras registradas.

A consulta deve apresentar as amostras mais recentes primeiro.

### RF16 — Filtrar amostras

O sistema deve permitir filtrar as amostras por critérios relevantes, incluindo pelo menos:

- data;
- navio;
- prefixo do trem.

Outros filtros poderão ser adicionados posteriormente conforme a necessidade.

### RF17 — Restringir informações da consulta

O sistema deve respeitar as permissões de cada perfil durante a consulta.

O Consultor não deve visualizar as observações registradas pelo Gestor nas solicitações de alteração.

## 5. LOG DO SISTEMA

### RF18 — Registrar ações importantes

O sistema deve registrar as principais ações realizadas no ciclo de uma amostra, incluindo:

- cadastro;
- solicitação de alteração;
- alteração;
- aprovação.

Cada registro do log deve conter, no mínimo:

- usuário responsável pela ação;
- data e hora;
- ação realizada;
- registro/amostra afetado.

### RF19 — Consultar/extrair log

O Root deve poder extrair os registros do log informando uma data inicial e uma data final.

## 6. REQUISITOS NÃO FUNCIONAIS

### RNF01 — Disponibilidade

O sistema deve estar disponível para utilização 24 horas por dia, 7 dias por semana, ressalvados períodos programados de manutenção.

### RNF02 — Segurança de acesso

O sistema deve exigir autenticação dos usuários e aplicar as permissões correspondentes ao perfil de cada usuário.

### RNF03 — Isolamento de dados

A arquitetura do sistema deve permitir que os dados pertencentes a diferentes organizações/empresas sejam isolados entre si, possibilitando a evolução futura para um modelo multi-tenant.

> Observação: isso é uma preocupação arquitetural desde o início, mas a administração completa de múltiplas organizações não faz parte da V1.

### RNF04 — Integridade dos dados

O sistema deve preservar a integridade dos dados das amostras, evitando alterações não autorizadas ou inconsistentes.

Em particular, uma amostra aprovada não deve poder ser modificada livremente.

### RNF05 — Rastreabilidade

O sistema deve manter registros das principais ações realizadas sobre as amostras, permitindo identificar quem realizou cada ação e quando ela ocorreu.

### RNF06 — Persistência

Os dados cadastrados devem permanecer armazenados para posterior consulta, respeitando as regras de acesso do sistema.

### RNF07 — Configuração por ambiente

As configurações específicas do ambiente de execução, especialmente informações sensíveis, devem ser mantidas separadas do código da aplicação.

### RNF08 — Manutenibilidade

O sistema deve ser estruturado de forma modular, mantendo separadas as principais responsabilidades da aplicação, de modo a facilitar sua manutenção e evolução.

### RNF09 — Evolutividade

A solução deve permitir a evolução gradual do sistema sem exigir a reconstrução completa da aplicação para a inclusão de novas funcionalidades.

## OBSERVAÇÕES ARQUITETURAIS

Os requisitos não devem ser confundidos com decisões técnicas.

Tecnologias como Python, Django, PostgreSQL, Git, Docker, AWS, ECS, RDS, Redis, SQS ou React são decisões técnicas/arquiteturais, e não requisitos funcionais do usuário.

### Diretriz geral

> “Beta pequena + fundamentos sólidos + evolução gradual.”

A arquitetura pretendida é um monólito modular, com PostgreSQL, preparado para futura evolução para um SaaS multi-tenant, sem introduzir complexidade de infraestrutura antes de existir uma necessidade concreta.

O objetivo é evitar tanto um MVP descartável e mal estruturado quanto uma arquitetura excessivamente complexa construída antes de existir um produto.