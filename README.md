# 🏢 Sistema de Gestão de Grupos Econômicos

<p align="justify">
  Este projeto foi desenvolvido para uma atividade avaliativa da disciplina de Programação Orientada a Objetos, no curso de Ciência da Computação do CESUPA. Trata-se de uma aplicação em Java, executada pelo terminal, que permite registrar vendas de produtos e prestações de serviços de entidades pertencentes a um grupo econômico, além de consultar informações e gerar relatórios de arrecadação.
</p>

<br>

## 👥 Autoria

<p align="justify">
  Este trabalho foi desenvolvido em conjunto por <strong>Hugo Brasil</strong> (Hugo-Brasil) e <strong>Rafael Dessbesell</strong> (RafaelDessbesell). Os autores acordaram a publicação deste trabalho em suas respectivas contas do GitHub, com atribuição conjunta do código desenvolvido para esta atividade avaliativa específica.
</p>

<br>

## 🎯 Descrição do Problema

<p align="justify">
  Quando diferentes entidades pertencentes a um mesmo grupo econômico realizam vendas e prestam serviços, surge a necessidade de organizar as informações de cada entidade e reunir os resultados do grupo. Sem registros relacionados entre si, torna-se mais difícil identificar os produtos disponíveis, consultar as operações realizadas, calcular os valores movimentados e comparar a arrecadação das entidades.
</p>

<p align="justify">
  O programa representa esse problema de forma simplificada: cada entidade mantém seu estoque, seu cadastro de serviços e seus históricos de operações, enquanto o grupo reúne essas informações para consultas e relatórios. O objetivo é permitir o acompanhamento das operações individuais e dos resultados conjuntos em uma aplicação acadêmica de terminal.
</p>

<br>

## 📦 Tecnologias

- Java 17;
- Maven, para organização do projeto e gerenciamento de dependências;
- JUnit 5, utilizado em um teste básico de cadastro de entidade;
- Visual Studio Code (VS Code), como ambiente de edição e execução do projeto com suporte a Java;
- `Scanner`, `ArrayList` e `FileWriter`, recursos da biblioteca padrão do Java utilizados na entrada de dados, nas coleções e na escrita de arquivos.

<p align="justify">
  A opção de exportação apresentada no menu como CSV gera, na versão atual, o arquivo <code>entidade.cvs</code>, contendo nome e cidade das entidades, separados pelo caractere <code>|</code>. Trata-se de uma exportação simples de texto delimitado, cuja extensão, cabeçalhos e separador podem ser padronizados para CSV. JSON não é utilizado na implementação atual. O VS Code é uma ferramenta de desenvolvimento; JUnit é uma dependência do projeto.
</p>

<br>

## ⚙️ Funcionalidades

- Cadastro de produtos no estoque de cada entidade, informando tipo, nome e preço;
- Cadastro dos serviços disponíveis em cada entidade, informando tipo e preço;
- Registro de vendas com um ou mais produtos e identificação do cliente, retirando os itens vendidos do estoque;
- Registro de atendimentos com um ou mais serviços previamente cadastrados e identificação do cliente;
- Listagem de produtos vendidos, serviços prestados e entidades do grupo econômico;
- Pesquisa de produtos em estoque pelo tipo;
- Consulta do produto de maior preço no estoque de uma entidade;
- Relatórios de arrecadação por entidade e pelo grupo, com os valores de vendas e de serviços;
- Cálculo da média de arrecadação por entidade, incluindo as entidades que ainda não arrecadaram;
- Ranking das entidades por arrecadação, da maior para a menor, com posições compartilhadas em caso de empate;
- Consulta da quantidade de vendas realizadas por uma entidade;
- Edição do nome e da cidade das entidades, além da possibilidade de remoção;
- Geração de um arquivo com a relação de entidades, contendo nome e cidade.

<p align="justify">
  O cadastro de um serviço apenas o disponibiliza para contratação. Seu valor entra no cálculo da arrecadação quando o atendimento é registrado. Da mesma forma, o valor de um produto em estoque somente integra a arrecadação após a venda. Neste projeto, a arrecadação corresponde à soma dos preços das operações registradas.
</p>

<br>

## 📋 Regras de Negócio

1. **Organização por entidade:** cada entidade do grupo possui seu próprio estoque, cadastro de serviços e histórico de vendas e atendimentos.
2. **Cadastro de produtos:** o cadastro pelo menu somente adiciona o produto quando tipo e nome não estão em branco e o preço é maior que zero.
3. **Cadastro de serviços:** o cadastro pelo menu somente adiciona o serviço quando o tipo não está em branco e o preço é maior que zero.
4. **Unidades em estoque:** cada registro de produto representa uma unidade disponível. A versão atual não possui um campo separado de quantidade.
5. **Registro de vendas:** uma venda reúne um ou mais produtos selecionados do estoque e é registrada uma única vez. Os produtos escolhidos são retirados do estoque. Uma seleção sem produtos válidos não gera uma venda.
6. **Registro de prestações:** um atendimento reúne um ou mais serviços selecionados do cadastro da entidade. O serviço permanece disponível para novos atendimentos. Uma seleção sem serviços válidos não gera uma prestação.
7. **Associação ao cliente:** cada venda e cada prestação possuem um objeto `Cliente`, que armazena o nome informado para aquela operação.
8. **Preço do atendimento:** cada serviço selecionado para uma prestação é registrado em um novo objeto, com o tipo e o preço daquele momento. Uma alteração posterior no cadastro não modifica os atendimentos anteriores.
9. **Total das operações:** o valor de uma venda é a soma dos preços dos produtos selecionados; o valor de uma prestação é a soma dos preços dos serviços selecionados. O cadastro de produtos ou serviços, isoladamente, não gera arrecadação.
10. **Arrecadação da entidade e do grupo:** o total de uma entidade corresponde às suas vendas mais suas prestações. O total do grupo corresponde à soma dos totais das entidades atualmente cadastradas.
11. **Média de arrecadação:** o total do grupo é dividido pela quantidade de entidades cadastradas, incluindo aquelas com arrecadação igual a zero. Sem entidades, o método de cálculo retorna zero e o relatório informa a ausência de cadastros.
12. **Ranking:** as entidades são apresentadas da maior para a menor arrecadação. Totais iguais compartilham a posição, no modelo `1, 1, 3`. Dentro de um empate, mantém-se a ordem de cadastro. O ranking preserva os índices originais usados pelo menu.
13. **Contagem de vendas:** cada operação de venda conta uma vez, independentemente da quantidade de produtos incluídos naquela operação.
14. **Manutenção dos dados:** os dados das operações permanecem em memória durante a execução. A exportação atual registra apenas nome e cidade das entidades e sobrescreve o arquivo anterior; não permite restaurar o histórico das operações.

<br>

## 🧩 Organização do Código

| Classe | Responsabilidade principal |
| --- | --- |
| `GrupoEconomico` | Reunir as entidades e oferecer consultas, relatórios, média e ranking de arrecadação. |
| `Entidade` | Manter os dados da entidade, seu estoque, o cadastro de serviços e os históricos de vendas e atendimentos. |
| `Estoque` | Armazenar os produtos disponíveis e permitir sua inclusão e remoção. |
| `Produto` e `Servico` | Representar os dados dos produtos e dos serviços. |
| `Venda` e `Prestacao` | Reunir os itens de cada operação, identificar o cliente e calcular o respectivo total. |
| `Cliente` | Representar o nome do cliente associado à operação. |
| `VendasGrupoEconomico` e `PrestacaoGrupoEconomico` | Reunir grupos para listar suas vendas e prestações de serviços. |
| `Main` | Iniciar o programa e apresentar o menu de interação com o usuário. |

<br>

## ⏳ O Processo de Criação

<p align="justify">
  Desenvolvemos este projeto em dupla, procurando aplicar os conhecimentos trabalhados na disciplina de Programação 
  Orientada a Objetos, disciplina do 2° semestre do curso de bacharelado em Ciência da Computação, ministrada no Centro Universitário 
  do Estado do Pará (CESUPA). Acordamos em dispor as informações de um grupo econômico em classes e estabelecer 
  relações entre entidades, produtos, serviços, clientes e operações.
</p>

<p align="justify">
  Durante o desenvolvimento, trabalhamos a distinção entre cadastrar um item e registrar uma operação, a organização dos históricos de vendas e atendimentos e a soma dos valores em diferentes níveis: primeiro em cada operação, depois na entidade e, por fim, no grupo. Também revisamos a seleção dos itens por índice e a leitura das informações digitadas pelo usuário.
</p>

<br>

## 📚 Aprendizados

Neste projeto, praticamos:

- A criação de classes, objetos, construtores e métodos;
- O uso de atributos privados e de métodos de acesso, como getters e setters;
- A associação entre objetos para representar as relações do sistema;
- O armazenamento e a consulta de objetos em listas com `ArrayList`;
- A utilização de estruturas condicionais e de repetição para organizar o menu e percorrer as listas;
- O uso de acumuladores e de métodos com retorno para calcular totais e médias;
- A busca do maior valor em uma lista e a construção de um ranking com uma lista temporária, preservando os índices originais;
- A diferença entre o cadastro de um serviço e o registro de uma prestação, preservando o preço de cada atendimento;
- A leitura de dados pelo terminal com `Scanner` e o cuidado ao combinar entradas numéricas com `nextLine()`;
- A escrita de informações em arquivo com `FileWriter`;
- A elaboração de um teste básico com JUnit para verificar a inclusão de uma entidade no grupo.

<br>

## 🌨️ Como este Projeto pode ser Melhorado?

<p align="justify">
  O projeto foi construído com finalidade acadêmica e apresenta possibilidades de aperfeiçoamento, como:
</p>

- Permitir o cadastro de novos grupos e entidades diretamente pelo menu;
- Salvar e recuperar os dados das operações entre as execuções do programa;
- Acrescentar o controle de quantidade de produtos no estoque;
- Ampliar as validações das entradas e o tratamento de situações como consultas a estoques vazios;
- Aprimorar a representação e a apresentação dos valores monetários;
- Padronizar a exportação em CSV, incluindo a extensão do arquivo, os cabeçalhos e o separador dos dados;
- Ampliar os testes para contemplar vendas, prestações, cálculos e situações de empate no ranking.

<br>

## 🛠️ Configuração do Ambiente

1. Instale o **JDK 17** e verifique sua disponibilidade no terminal com `java -version` e `javac -version`;
2. Faça o download ou clone este repositório e localize a pasta `Sistema_de_Gestao_de_Grupos_Economicos` que contém o arquivo `pom.xml`;
3. Abra essa pasta na IDE de sua preferência. No VS Code, utilize suporte à linguagem Java e selecione o JDK 17 para o projeto;
4. Para utilizar o gerenciamento de dependências pelo terminal, instale o **Maven** e verifique sua disponibilidade com `mvn -version`. A dependência do JUnit 5 está declarada no `pom.xml` e pode ser obtida pelo Maven ou pelo suporte da IDE ao projeto Maven.

<p align="justify">
  O programa não exige banco de dados, credenciais ou acesso a uma API externa para executar suas operações. O arquivo exportado é criado no diretório de execução do programa. As entradas numéricas devem ser digitadas no formato aceito pelo ambiente Java utilizado.
</p>

<br>

## 🛞 Rodando o Projeto

1. Faça o download deste repositório ou clone o projeto para seu computador;
2. Instale o JDK 17 ou uma versão compatível com a configuração do projeto;
3. Abra, na IDE de sua preferência, a pasta `Sistema_de_Gestao_de_Grupos_Economicos` que contém o arquivo `pom.xml`;
4. Execute o método `main` da classe `Main`, localizada em `src/main/java/com/gerenciamento/Main.java`;
5. Utilize os números apresentados no menu para escolher as operações. Para encerrar, selecione `0`.

Também é possível compilar e executar pelo terminal. Na pasta que contém o arquivo `pom.xml`, utilize:

```bash
javac -encoding UTF-8 -d out src/main/java/com/gerenciamento/*.java
java -cp out com.gerenciamento.Main
```

<br>

## 🧪 Exemplos de Utilização

<p align="justify">
  O programa inicia com o grupo <strong>Computação do futuro</strong> e duas entidades: <strong>Rafael</strong>, em Curitiba, no índice <code>0</code>; e <strong>Hugo</strong>, em Belem, no índice <code>1</code>. O exemplo abaixo considera uma execução nova, antes de cadastrar operações ou remover entidades. Quando o programa perguntar se deseja adicionar outro item, escolha <code>0</code>, salvo se desejar ampliar a operação.
</p>

| Etapa | Opção do menu e dados de exemplo | Resultado esperado |
| --- | --- | --- |
| 1 | Opção `1`: entidade `0`; tipo `Informática`; nome `Mouse`; preço `100`. | Produto cadastrado no estoque, sem gerar arrecadação. |
| 2 | Opção `2`: entidade `0`; serviço `Suporte técnico`; preço `200`. | Serviço cadastrado, sem gerar arrecadação. |
| 3 | Opção `3`: entidade `0`; produto de índice `0`; cliente `Ana`. | Venda de R$ 100 e retirada do produto do estoque. |
| 4 | Opção `4`: entidade `0`; serviço de índice `0`; cliente `Ana`. | Prestação de R$ 200. A entidade passa a totalizar R$ 300. |
| 5 | Opção `2`: entidade `1`; serviço `Consultoria`; preço `500`. | Serviço cadastrado na segunda entidade. |
| 6 | Opção `4`: entidade `1`; serviço de índice `0`; cliente `Bruno`. | Prestação de R$ 500 na segunda entidade. |
| 7 | Opção `13`: entidade `0`. | Relatório com R$ 100 em vendas, R$ 200 em serviços e total de R$ 300. |
| 8 | Opção `14`. | Arrecadação total do grupo: R$ 800. |
| 9 | Opção `15`. | Média por entidade: R$ 400, pois `800 / 2 = 400`. |
| 10 | Opção `16`. | Hugo em primeiro, com R$ 500; Rafael em segundo, com R$ 300. |
| 11 | Opção `21`: entidade `0`. | Quantidade de vendas: `1`. |
| 12 | Opção `20`. | Criação do arquivo `entidade.cvs` com nome e cidade das entidades. |

<br>

## 🤖 Utilização de Inteligência Artificial

<p align="justify">
  A implementação inicial foi desenvolvida em conjunto pelos integrantes. Posteriormente, utilizamos o ChatGPT como apoio à revisão do código, à identificação e correção de problemas, à implementação de funcionalidades complementares e à elaboração e revisão deste README.
</p>

<p align="justify">
  O apoio incluiu a separação entre cadastro de serviços e registro de prestações, o ajuste do registro de vendas para evitar duplicação, os cálculos de arrecadação por entidade e pelo grupo, a média e o ranking. Solicitamos que as soluções utilizassem os recursos já presentes no projeto, mantendo a abordagem trabalhada na disciplina.
</p>
