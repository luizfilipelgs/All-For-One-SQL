
# Boas vindas ao repositório do projeto All For One


## O que foi desenvolvido 👨‍💻

Um projeto com o codinome *All For One* em que foi praticado todos os conceitos de SQL vistos até o momento atravez de uma série de desafios com diferentes níveis de complexidade, utilizando o banco de dados `Northwind`. 


<details>
  <summary><strong>🐋 Rodando no Docker vs Localmente</strong></summary><br />

  ## Com Docker

  **:warning: Antes de começar, seu docker-compose precisa estar na versão 1.29 ou superior. [Veja aqui](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04-pt) ou [na documentação](https://docs.docker.com/compose/install/) como instalá-lo. No primeiro artigo, você pode substituir onde está com `1.26.0` por `1.29.2`.**

  > :information_source: Rode os serviços `node` e `db` com o comando `docker-compose up -d`.
  - Lembre-se de parar o `mysql` se estiver usando localmente na porta padrão (`3306`), ou adapte, caso queria fazer uso da aplicação em containers
  - Esses serviços irão inicializar um container chamado `all_for_one` e outro chamado `all_for_one_db`.
  - A partir daqui você pode rodar o container `all_for_one` via CLI ou abri-lo no VS Code.

  > :information_source: Use o comando `docker exec -it all_for_one bash`.
  - Ele te dará acesso ao terminal interativo do container criado pelo compose, que está rodando em segundo plano.
  - As credencias de acesso ao banco de dados estão definidas no arquivo `docker-compose.yml`, e são acessíveis no container através das variáveis de ambiente `MYSQL_USER` e `MYSQL_PASSWORD`. 💡

  > :information_source: Instale as dependências [**Caso existam**] com `npm install`. (Instale dentro do container)

  - **:warning: Atenção:** Caso opte por utilizar o Docker, **TODOS** os comandos disponíveis no `package.json` (npm start, npm test, npm run dev, ...) devem ser executados **DENTRO** do container, ou seja, no terminal que aparece após a execução do comando `docker exec` citado acima.

  - **:warning: Atenção:** O **git** dentro do container não vem configurado com suas credenciais. Ou faça os commits fora do container, ou configure as suas credenciais do git dentro do container.

  - **:warning: Atenção:** Não rode o comando npm audit fix! Ele atualiza várias dependências do projeto, e essa atualização gera conflitos com o avaliador.

  - ✨ **Dica:** A extensão `Remote - Containers` (que estará na seção de extensões recomendadas do VS Code) é indicada para que você possa desenvolver sua aplicação no container Docker direto no VS Code, como você faz com seus arquivos locais.

  ![remote-containers](./images/remote-container.png)

  <br />

  ## Sem Docker

  > :information_source: Instale as dependências [**Caso existam**] com `npm install`

  - **:warning: Atenção:** Não rode o comando npm audit fix! Ele atualiza várias dependências do projeto, e essa atualização gera conflitos com o avaliador.

  - **✨ Dica:** Para rodar o projeto desta forma, obrigatoriamente você deve ter o `node` instalado em seu computador.
  - **✨ Dica:** O avaliador espera que a versão do `node` utilizada seja a 16.

  <br/>
</details>

<details>
  <summary><strong>📑 Instruções para testar as queries</strong></summary><br />

  #### Para executar os testes locais com Docker 🐋

  - Após ter seguido os passos anteriores do `docker-compose up -d` e `docker exec -it all_for_one bash`, dentro do terminal interativo do container, rode:
  ```sh
  npm test
  ```

  #### Para executar os testes locais usando a instalação do MySQL feita na sua máquina 💻

  - Para executar localmente os testes é preciso escrever o seguinte no seu terminal:
  ```sh
  MYSQL_USER=<SEU_NOME_DE_PESSOA_USUARIA> MYSQL_PASSWORD=<SUA SENHA> HOSTNAME=<NOME_DO_HOST> PORT=<PORTA> npm test
  ```

  - Não esqueça de substituir os locais indicados com `< >` por suas credenciais:
  ```sh
  MYSQL_USER=root MYSQL_PASSWORD=password HOSTNAME=localhost PORT=3306 npm test
  ```

  #### Dicas e pontos de atenção

  - ✨ **Dica:** variáveis de ambiente definidas na mesma linha do comando valem apenas para aquele comando. Se preferir, você pode exportar as variáveis de ambiente para toda a _sessão_ (todos os comandos até você fechar aquele terminal). Por exemplo:
  ```sh
  export MYSQL_USER=root MYSQL_PASSWORD=password HOSTNAME=localhost PORT=3306
  ```
  > E depois disso você só precisa rodar `npm test` quando for testar os projetos.

  - ✨ **Dica:** Caso queira utilizar _Docker_ para rodar os testes localmente, basta executar o comando:
  ```sh
  docker run -p 3306:3306 --name mysql_57 -e MYSQL_ROOT_PASSWORD=1234 -d mysql:5.7 mysqld --default-authentication-plugin=mysql_native_password
  ```
  - Depois de usar o comando acima, agora basta executar os testes digitando no terminal:
  ```sh
  MYSQL_USER=root MYSQL_PASSWORD=1234 HOSTNAME=localhost npm test
  ```

  <details close>
    <summary>O que está sendo feito na dica acima</summary>
    <br>

    - :point_right: flag --name:
    > Define um nome para o nosso _container_: "meu-mysql-5_7".

    - :point_right: flag -e:
    > Define a variável de ambiente "MYSQL_ROOT_PASSWORD" com o valor "1234".

    - :point_right: flag -d:
    > Define que o container rode em segundo plano.

    - :point_right: flag -p:
    > Mapeia uma porta local a uma porta do _container_.

    - :point_right: mysql:5.7:
    > Define qual versão da imagem  mySQL queremos, no caso, a 5.7, que é a esperada pelo avaliador.
  </details>

  - **:warning: Atenção:** O avaliador espera que a versão do  MySQL seja a 5.7. Em caso de erro nos testes, verifique se essa é a versão que está sendo usada por você.

  - **:warning: Atenção:** Não é necessário colocar `USE northwind` ou `SET SQL_SAFE_UPDATES = 0;` no início dos seus arquivos

  - **:warning: Atenção:** Após a execução dos teste locais, o banco de dados `northwind` é recriado :warning:
</details>

  ---

## Requisitos do projeto

Monte queries para encontrar as informações esperadas pelos desafios:

### Desafios Iniciais

- [x] 1 - Exiba apenas os nomes dos produtos na tabela `products`.

  ---

- [x] 2 - Exiba os dados de todas as colunas da tabela `products`.

  ---

- [x] 3 - Escreva uma query que exiba os valores da coluna que representa a _primary key_ da tabela `products`.

  ---

- [x] 4 - Conte quantos registros existem na coluna `product_name` da tabela `products`.

  ---

- [x] 5 - Monte uma query que exiba os dados da tabela `products` a partir do quarto registro até o décimo terceiro.

  ---

- [x] 6 - Exiba os dados das colunas `product_name` e `id` da tabela `products` de maneira que os resultados estejam em ordem alfabética dos nomes.

  ---

- [x] 7 - Mostre apenas os ids dos 5 últimos registros da tabela `products` (a ordernação deve ser baseada na coluna `id`).

  ---

- [x] 8 - Faça uma consulta que retorne três colunas, respectivamente, com os nomes 'A', 'Trybe' e 'eh', e com valores referentes a soma de '5 + 6', a string 'de', a soma de '2 + 8'.


### Desafios sobre filtragem de dados

- [x] 9 - Mostre todos os valores de `notes` da tabela `purchase_orders` que não são nulos.

  ---

- [x] 10 - Mostre todos os dados da tabela `purchase_orders` em ordem decrescente, ordenados por `created_by` em que o `created_by` é maior ou igual a 3.

  - Ordene também os resultados pelo `id` de forma crescente, como critério de desempate para a ordenação.

  ---

- [x] 11 - Exiba os dados da coluna `notes` da tabela `purchase_orders` em que seu valor de `Purchase generated based on Order` é maior ou igual a 30 e menor ou igual a 39.

  ---

- [x] 12 - Mostre as `submitted_date` de `purchase_orders` em que a `submitted_date` é do dia 26 de abril de 2006.

  ---

- [x] 13 - Mostre o `supplier_id` das `purchase_orders` em que o `supplier_id` seja 1 ou 3.

  ---

- [x] 14 - Mostre os resultados da coluna `supplier_id` da tabela `purchase_orders` em que o `supplier_id` seja maior ou igual a 1 e menor ou igual 3.

  ---

- [x] 15 - Mostre somente as horas (sem os minutos e os segundos) da coluna `submitted_date` de todos registros da tabela `purchase_orders`.

  - No resultado, a hora extraída da coluna `submitted_date` deve ser chamada de `submitted_hour`.

  ---

- [x] 16 - Exiba a `submitted_date` das `purchase_orders` que estão entre `2006-0- 1-26 00:00:00` e `2006-03-31 23:59:59`.

  ---

- [x] 17 - Mostre os registros das colunas `id` e `supplier_id` das `purchase_orders` em que os `supplier_id` sejam tanto 1, ou 3, ou 5, ou 7.

  ---

- [x] 18 - Mostre todos os registros de `purchase_orders` que tem o `supplier_id` igual a 3 e `status_id` igual a 2.

  ---

- [x] 19 - Mostre a quantidade de pedidos que foram feitos na tabela `orders` pelo `employee_id` igual a 5 ou 6, e que foram enviados através do método(coluna) `shipper_id` igual a 2.

  - No resultado, a coluna que contém a contagem de pedidos deve ser chamada de `orders_count`.

  ---

## Desafios de manipulação de tabelas

- [x] 0 - Adicione à tabela `order_details` um registro com `order_id`: 69, `product_id`: 80, `quantity`: 15.0000, `unit_price`: 15.0000, `discount`: 0, `status_id`: 2, `date_allocated`: NULL, `purchase_order_id`: NULL e `inventory_id`: 129.

  ---

- [x] 21 - Adicione com um único `INSERT`, duas linhas à tabela `order_details` com os mesmos dados do requisito 20.

  ---

- [x] 22 - Atualize os dados de `discount` do `order_details` para 15.

⚠️ Para testar localmente, pode ser necessário utilização do SAFE UPDATE, porém **não é necessário adicionar a instrução do SAFE UPDATE no arquivo `desafio22.sql` junto a query**, pois o próprio avaliador irá ajustar isso.

  ---

- [x] 23 - Atualize os dados da coluna `discount` da tabela `order_details` para 30, onde o valor na coluna `unit_price` seja menor que 10.0000.

  ---

- [x] 24 - Atualize os dados da coluna `discount` da tabela `order_details` para 45, onde o valor na coluna `unit_price` seja maior que 10.0000 e o id seja um número entre 30 e 40.

  ---

- [x] 25 - Delete todos os dados em que a `unit_price` da tabela `order_details` seja menor que 10.0000.

  ---

- [x] 26 - Delete todos os dados em que a `unit_price` da tabela `order_details` seja maior que 10.0000.

  ---

- [x] 27 - Delete todos os dados da tabela `order_details`.

---
