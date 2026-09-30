# Fubá

## O que é o Fubá?

O Fubá é um sistema para registro, acompanhamento e consulta de dados de amostras de açúcar e grãos coletadas durante operações de recebimento e embarque em terminais logísticos.

O sistema tem como objetivo centralizar os registros das amostras, seus resultados de análise e o processo de aprovação dessas informações, permitindo que os dados sejam consultados de forma rápida e controlada.

## Que problemas ele busca resolver?

O Fubá busca:

* reduzir riscos de erros e fraudes relacionados aos registros de qualidade dos produtos;
* centralizar os dados das amostras em um único sistema;
* aumentar a velocidade de compartilhamento das informações;
* garantir que os resultados publicados tenham passado por um processo de conferência e aprovação;
* manter um histórico das principais ações realizadas sobre os registros;
* futuramente permitir o compartilhamento controlado dos dados com clientes e outros terminais.

## Objetivos da primeira versão

A primeira versão será um Produto Mínimo Viável (MVP) voltado para operações com açúcar.

O MVP deverá permitir:

* cadastro de amostras de açúcar durante a descarga de trens na moega;
* cadastro de amostras relacionadas ao embarque de açúcar em navios;
* registro dos resultados das análises;
* controle do processo de aprovação dos registros;
* solicitação de alterações em registros antes ou depois da aprovação;
* consulta dos registros aprovados de acordo com o nível de acesso do usuário;
* registro das principais ações realizadas no sistema.

Versões futuras poderão incluir outros produtos, como milho e soja, além de permitir a utilização do sistema por outros terminais e disponibilizar dados de forma controlada para clientes.

## Tecnologias planejadas

### Backend

* Python
* Django

### Banco de dados

* PostgreSQL

### Interface

* Django Templates
* HTML
* CSS
* JavaScript

### Infraestrutura e desenvolvimento

* Git
* GitHub
* Docker
* Testes automatizados
* CI/CD

A arquitetura inicial será baseada em um **monólito modular**, buscando manter uma estrutura simples para o MVP sem impedir a evolução futura do sistema.

A infraestrutura será inicialmente dimensionada para a primeira versão e poderá evoluir conforme o crescimento da aplicação.

## Situação atual do projeto

O projeto encontra-se na fase de engenharia.

Neste momento estão sendo definidos e documentados os requisitos, regras de negócio, modelo de dados e arquitetura que deverão orientar o desenvolvimento do sistema.

Após a conclusão dessa etapa, será iniciado o desenvolvimento do MVP.
