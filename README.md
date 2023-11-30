#Sub - 1TDSPM

## Objetivo - Criar uma API para cadastro e busca de carros
	
### Dom�nio - 2pt
	
- Criar a classe Carro no pacote br.com.fiap.sub.estacionamento.dominio com os seguintes atributos, bem como seus getters e setters:

	- placa: String
	- marca: String
	- modelo: String
	- ano: int


- Criar a interface RepositorioDeCarros no pacote br.com.fiap.sub.estacionamento.dominio.repositorios com dois m�todos: 

	- inserir, recebendo um objeto do tipo Carro como argumento, sem retorno
	- buscarPorPlaca, recebendo uma string placa como argumento, com um retorno do tipo Carro
	
### JDBC - 3pt

- Para testes, criar a tabela abaixo no seu banco FIAP:

	CREATE TABLE carro (
	placa varchar(30) PRIMARY KEY,
	modelo varchar(255) NOT NULL,
	marca varchar(255) NOT NULL,
	ano integer NOT NULL);

- Criar a classe RepositorioDeCarrosJDBC no pacote br.com.fiap.sub.estacionamento.infraestrutura, que implementa a interface RepositorioDeCarros
- implementar o m�todo inserir:

	- conectar no seu banco Oracle da fiap
	- realizar o comando "insert into carro(placa, marca, modelo, ano) values (?, ?, ?, ?)" passando como par�metros os atributos do objeto carro
	- As exce��es checadas devem ser transformadas em RuntimeException
	
	
- implementar o m�todo buscarPorPlaca:
	
	- conectar no seu banco Oracle da fiap (Classe do driver: oracle.jdbc.OracleDriver
	- realizar o select abaixo, passando o argumento placa para ele, esperando um ou nenhum registro:
		- select * from carro where placa = ?
	- Se houver registro, transform�-lo em um objeto do tipo Carro e retornar
	- Se n�o houver registro, retornar nulo
	- As exce��es checadas devem ser transformadas em RuntimeException
	
### Services - 2pt


- Criar a classe EstacionamentoServico no pacote br.com.fiap.sub.estacionamento.aplicacao

	- Atributo repositorio do tipo RepositorioDeCarros
	- Construtor recebendo um objeto do tipo RepositorioDeCarros
	
	- m�todo registrarCarro, recebendo como argumento objeto do tipo Carro, sem retorno

		- Realizar as valida��es abaixo:
		
	
			- Se placa for nula ou uma string em branco, lan�ar a exce��o RuntimeException informando que a placa � inv�lida
			- Se marca for nula ou uma string em branco, lan�ar a exce��o RuntimeException informando que a marca � inv�lida
			- Se modelo for nulo ou uma string em branco, lan�ar a exce��o RuntimeException informando que o modelo � inv�lido
			- Se ano for menor que 1940 ou maior que 2023, lan�ar uma exce��o RuntimeException informando que o ano � inv�lido
			
		- Deve verificar se j� existe um carro existente no banco com a mesma placa utilizando o m�todo buscarPorPlaca do RepositorioDeCarros. Em caso positivo, lan�ar uma exce��o do tipo RuntimeException, informando o erro.
		
		- Se n�o houver carro com a mesma placa, deve inserir no banco de dados chamando o m�todo inserir do RepositorioDeCarros
		
	- m�todo buscarPorPlaca, recebendo como argumento uma String representando a placa buscada, com retorno do tipo Carro
		- Deve chamar o m�todo buscarPorPlaca do RepositorioDeCarros. Caso exista um carro retorn�-lo
		- Caso n�o exista, retornar nulo
		
### API - 3pt

- Criar classe EstacionamentoApi no pacote br.com.fiap.sub.estacionamento.api
	- Anotar a classe para ser criada a api "carros"
	
	- Criar um m�todo representando uma API de cria��o de carro utilizando o verbo HTTP correto. 
		- Deve utilizar um objeto da classe EstacionamentoServico e chamar o m�todo registrarCarro, retornando os c�digos corretos em caso de sucesso ou erro.
	
	- Criar um m�todo representando uma api de busca por placa. Deve chamar a classe buscarPorPlaca da classe EstacionamentoServico, tratando os casos de registro encontrado, registro n�o encontrado, e erro.
	
### B�nus - 2pts

- Criar uma classe TesteLeituraArquivo com um m�todo main que leia o arquivo carros.txt existente no projeto, e transforme em objetos do tipo Carro, imprimindo seus atributos na tela sobrescrevendo o m�todo toString
- Dica: O arquivo est� com as informa��es marca, modelo, placa e ano, nesta ordem, separados por ";". A classe String possui o m�todo split, que permite dividir uma string por um delimitador. Ex: String[] conteudoLinha = linha.split(";");	
	





	
