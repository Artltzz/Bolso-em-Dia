# Bolso em Dia — Controle de Gastos Pessoais

**Aluno:** Arthur Filipe  
**Curso:** Análise e Desenvolvimento de Sistemas  

## 1. Termo de abertura do projeto

### Problema real

Muitas pessoas fazem pequenas compras ao longo do mês e perdem a noção do total gasto e das categorias que mais consomem seu dinheiro.

### Proposta de valor

Oferecer uma forma simples de registrar despesas e visualizar o total mensal e sua distribuição por categoria.

### Dentro do escopo

- Cadastrar, editar e excluir despesas.
- Classificar despesas por categoria.
- Consultar despesas por mês e categoria.
- Calcular o total gasto no mês.
- Exibir o total gasto em cada categoria.

### Fora do escopo

- Integração com bancos e cartões.
- Pagamentos ou transferências.
- Controle de investimentos.
- Cadastro de usuários e login.
- Despesas recorrentes automáticas.
- Recomendações financeiras com IA.

A primeira versão será uma aplicação web de uso individual, executada localmente.

## 2. Histórias de usuário

**HU01:** Como usuário, quero registrar o valor, a categoria e a data de uma despesa, para que eu consiga acompanhar meus gastos.

**HU02:** Como usuário, quero consultar o total gasto em determinado mês, para que eu compreenda quanto dinheiro utilizei nesse período.

**HU03:** Como usuário, quero visualizar os gastos por categoria, para que eu identifique onde estou concentrando minhas despesas.

**HU04:** Como usuário, quero corrigir ou excluir um lançamento, para que meus registros representem os gastos realizados.

## 3. Requisitos do sistema

### Requisitos funcionais

| Código | Requisito |
|---|---|
| RF01 | Cadastrar despesas com descrição, valor, categoria e data. |
| RF02 | Validar os campos obrigatórios e aceitar somente valores maiores que zero. |
| RF03 | Listar as despesas da mais recente para a mais antiga. |
| RF04 | Permitir editar e excluir despesas cadastradas, solicitando confirmação antes da exclusão. |
| RF05 | Filtrar despesas por mês e categoria, individualmente ou em conjunto. |
| RF06 | Calcular o total das despesas do mês selecionado. |
| RF07 | Exibir os totais por categoria referentes ao mês selecionado. |

### Requisitos não funcionais

| Código | Requisito |
|---|---|
| RNF01 | Armazenar os dados em SQLite, preservando os registros após reiniciar a aplicação. |
| RNF02 | Permitir o uso da interface em telas a partir de 360 pixels de largura, sem rolagem horizontal. |
| RNF03 | Exibir valores em reais, com duas casas decimais, e mensagens em português. |
| RNF04 | Armazenar valores monetários em centavos inteiros para evitar imprecisões de ponto flutuante nos cálculos. |

## 4. Caso de uso principal e tratamento de erros

**Caso de uso principal:** Registrar uma despesa.

**Ator:** Usuário.

**Pré-condições:** Aplicação em execução e banco disponível.

### Fluxo principal

1. O usuário seleciona “Nova despesa”.
2. O sistema apresenta o formulário de cadastro.
3. O usuário preenche descrição, valor, categoria e data.
4. O usuário seleciona “Salvar”.
5. O sistema verifica os campos obrigatórios, a validade da data e se o valor é maior que zero.
6. O sistema armazena a despesa no banco.
7. A interface confirma o cadastro e atualiza a listagem e os totais do período exibido.

### Regras de negócio

- A descrição não pode conter apenas espaços.
- O valor deve ser positivo e ter, no máximo, duas casas decimais.
- A categoria deve pertencer à lista: alimentação, transporte, moradia, saúde, lazer, educação ou outros.
- A data deve ser válida e não pode ser futura, pois o sistema registra gastos já realizados.
- A edição ou exclusão de uma despesa deve atualizar os totais correspondentes.

### Fluxos de exceção

- **Dados inválidos:** impedir o cadastro, indicar o campo que precisa de correção e preservar o formulário.
- **Falha de conexão com o backend:** informar que não foi possível salvar e permitir nova tentativa.
- **Falha no banco:** apresentar uma mensagem de erro sem confirmar o cadastro.
- **Registro não encontrado:** informar que a despesa não está disponível e atualizar a listagem.

## 5. Arquitetura e escolha da stack tecnológica

| Camada | Tecnologia | Responsabilidade |
|---|---|---|
| Frontend | HTML, CSS e JavaScript | Apresentar formulários, filtros, listagem e resumo dos gastos. |
| Backend | Python com Flask | Receber requisições, validar dados e calcular os totais. |
| Armazenamento | SQLite | Guardar os registros das despesas. |

### Arquitetura

O navegador enviará requisições HTTP ao backend, que acessará o SQLite e retornará os dados em JSON.

O frontend será responsável pela apresentação das informações e pela interação com o usuário. O backend realizará as validações, aplicará as regras de negócio e acessará o banco de dados.

### Justificativa

HTML, CSS e JavaScript atendem às necessidades de uma interface pequena. Flask permite organizar as rotas e regras em Python, enquanto SQLite simplifica a persistência por dispensar um servidor de banco separado.

## 6. Critérios de aceite e definição de pronto

### Critérios de aceite

O projeto será considerado concluído quando:

- [ ] Despesas válidas puderem ser cadastradas, listadas, editadas e excluídas.
- [ ] Valores iguais ou menores que zero, datas futuras e campos obrigatórios vazios forem rejeitados.
- [ ] Os dados permanecerem disponíveis após reiniciar a aplicação.
- [ ] Os filtros exibirem somente os registros que correspondem ao período e à categoria selecionados.
- [ ] Um mês com despesas de R$ 25,50 e R$ 14,50 apresentar o total de R$ 40,00.
- [ ] Os totais por categoria corresponderem à soma dos respectivos lançamentos.
- [ ] Um período sem despesas apresentar lista vazia e total de R$ 0,00.
- [ ] A interface atender à largura mínima definida.
- [ ] O README explicar como instalar, executar e testar as funcionalidades na entrega da implementação.

### Definição de pronto

Funcionalidades do escopo implementadas e verificadas, cálculos corretos, validações funcionando e instruções suficientes para outra pessoa executar o sistema localmente.
