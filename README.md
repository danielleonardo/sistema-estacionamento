#Sub - 1TDSPM

## Objetivo - Criar uma API para cadastro e busca de carros
	
### Domínio - 2pt
	
- Criar a classe Carro no pacote br.com.fiap.sub.estacionamento.dominio com os seguintes atributos, bem como seus getters e setters:

	- placa: String
	- marca: String
	- modelo: String
	- ano: int


- Criar a interface RepositorioDeCarros no pacote br.com.fiap.sub.estacionamento.dominio.repositorios com dois métodos: 

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
- implementar o método inserir:

	- conectar no seu banco Oracle da fiap
	- realizar o comando "insert into carro(placa, marca, modelo, ano) values (?, ?, ?, ?)" passando como parâmetros os atributos do objeto carro
	- As exceções checadas devem ser transformadas em RuntimeException
	
	
- implementar o método buscarPorPlaca:
	
	- conectar no seu banco Oracle da fiap (Classe do driver: oracle.jdbc.OracleDriver
	- realizar o select abaixo, passando o argumento placa para ele, esperando um ou nenhum registro:
		- select * from carro where placa = ?
	- Se houver registro, transformá-lo em um objeto do tipo Carro e retornar
	- Se não houver registro, retornar nulo
	- As exceções checadas devem ser transformadas em RuntimeException
	
### Services - 2pt


- Criar a classe EstacionamentoServico no pacote br.com.fiap.sub.estacionamento.aplicacao

	- Atributo repositorio do tipo RepositorioDeCarros
	- Construtor recebendo um objeto do tipo RepositorioDeCarros
	
	- método registrarCarro, recebendo como argumento objeto do tipo Carro, sem retorno

		- Realizar as validações abaixo:
		
	
			- Se placa for nula ou uma string em branco, lançar a exceção RuntimeException informando que a placa é inválida
			- Se marca for nula ou uma string em branco, lançar a exceção RuntimeException informando que a marca é inválida
			- Se modelo for nulo ou uma string em branco, lançar a exceção RuntimeException informando que o modelo é inválido
			- Se ano for menor que 1940 ou maior que 2023, lançar uma exceção RuntimeException informando que o ano é inválido
			
		- Deve verificar se já existe um carro existente no banco com a mesma placa utilizando o método buscarPorPlaca do RepositorioDeCarros. Em caso positivo, lançar uma exceção do tipo RuntimeException, informando o erro.
		
		- Se não houver carro com a mesma placa, deve inserir no banco de dados chamando o método inserir do RepositorioDeCarros
		
	- método buscarPorPlaca, recebendo como argumento uma String representando a placa buscada, com retorno do tipo Carro
		- Deve chamar o método buscarPorPlaca do RepositorioDeCarros. Caso exista um carro retorná-lo
		- Caso não exista, retornar nulo
		
### API - 3pt

- Criar classe EstacionamentoApi no pacote br.com.fiap.sub.estacionamento.api
	- Anotar a classe para ser criada a api "carros"
	
	- Criar um método representando uma API de criação de carro utilizando o verbo HTTP correto. 
		- Deve utilizar um objeto da classe EstacionamentoServico e chamar o método registrarCarro, retornando os códigos corretos em caso de sucesso ou erro.
	
	- Criar um método representando uma api de busca por placa. Deve chamar a classe buscarPorPlaca da classe EstacionamentoServico, tratando os casos de registro encontrado, registro não encontrado, e erro.
	
### Bônus - 2pts

- Criar uma classe TesteLeituraArquivo com um método main que leia o arquivo carros.txt existente no projeto, e transforme em objetos do tipo Carro, imprimindo seus atributos na tela sobrescrevendo o método toString
- Dica: O arquivo está com as informações marca, modelo, placa e ano, nesta ordem, separados por ";". A classe String possui o método split, que permite dividir uma string por um delimitador. Ex: String[] conteudoLinha = linha.split(";");	
	





	
