-- PASSOS PARA APRENDER A DESENVOLVER CRUD EM QUALQUER LINGUAGEM DE PROGRAMAÇÃO --

1º) Escolha sua linguagem Back-end
	Recomendo:	
	- JAVA
	- PHP
		
*Obs.: é muito bom possuir uma noção de Orientação a Objetos. Caso não tenha ainda, recomendo muito as aulas do professor Guanabara (Segue o link abaixo)

2ª) Escolha um SGBD relacional de sua preferencia (Sistema gerenciador de banco de dados)
	- PostgreSQl
	- MySQL
	- Access
	- SQL Server
	- Oracle Database
	- MariaDB
	

3º) Encontre o driver de conexão entre o banco de dados e aplicação

	- Procure na documentação exatamente essas funções:

		Como conectar-se ao banco de dados;
		Como fechar conexao;
		Como acionar comandos SQL com a linguagem; (criação, alteração, 								exclusão e 									visualização)

*Dica: caso a documentação esteja confusa demais procure em foruns, video-aulas ou pergunte a um colega da comunidade de sua preferencia.	

4º) Crie seu modelo relacional do banco de dados (crie suas tabelas)

5º) Crie sua fábrica de conexão
	
6º) Crie suas classes de domínio

7º) Crie as classes DAO a partir das classes de dominio:

*Dica: se você está nos primeiros passos tente com apenas uma unica entidade de dominio e uma unica entidade relacional para ficar mais facil de aprender.

8º) Se você estiver trabalhando com interface gráfica lembre-se que você pode envolver Orientação a Eventos então procure separar o que é interface gráfica das classes de dominio para ficar mais fácil de focar sua lógica de programação.

*Obs.: pensei dessa forma já que o nível lógico de acionar comandos sql entre tratar dados do formulario são duas coisas completamente diferentes. Acredito que existe uma relação muito forte com as interfaces gráficas(janelinhas) e os eventos como 'clicar', 'carregar nova janela'...

9º) Crie uma rotina de testes para executar classes DAO
	
	Isso ajuda você a comprender seu código com mais rapidez e realizar testes em poucos segundos. Deixando de lado o "teste1", "teste2" na sua base de dados e te premiando com mais tempo para focar no seu aprendizado.

Obs.: É importante já ficar sabendo que é possivel testar seu código com auxílio de frameworks de teste unitários;

	Ok, talvez você não conheça todas as ferramentas e técnicas que eu citei. 
Segue uma lista carinhosamente recomendada por mim de um material super bacana pra conseguir fazer seu primeiro CRUD Orientado a Objetos, Padrão DAO com MVC e Testes Unitários. 

MATERIAL COMPLEMENTAR:

- Aprenda Orientação a Objetos, CURSO EM VIDEO. 
<https://www.youtube.com/watch?v=KlIL63MeyMY&list=PLHz_AreHm4dkqe2aR0tQK74m8SFe-aGsY>

- Aprenda o que são classes de domínio.
	
	Atributos em Diagramas de Modelagem de Dominio 
<https://www.ibm.com/support/knowledgecenter/pt-br/SS8PJ7_9.1.1/com.ibm.xtools.viz.class.diagram.doc/topics/cattributes.html>

- Guia dos comandos SQL, W3SCHOOLS. 
<https://www.w3schools.com/sql/default.asp>

- Guia de modelagem de bancos de dados relacionais. 
	CURSO EM VIDEO <https://www.youtube.com/watch?v=Ofktsne-utM&list=PLHz_AreHm4dkBs-795Dsgvau_ekxg8g1r>

- Aprenda o que é uma Fabrica de Conexão e o Desing Pattern Factory
	
DevMedia: <https://www.devmedia.com.br/design-patterns-factory/17158>	
Wiki: <https://pt.wikipedia.org/wiki/Factory_Method>

- Aprenda o  que é o Desing Pattern DAO e como usar.

Tutorials Point: <https://www.tutorialspoint.com/design_pattern/data_access_object_pattern.htm>

- Aprenda o que é o padrão MVC e como usar.

Tableless : <https://tableless.com.br/mvc-afinal-e-o-que/>

- Aprenda o que é a metodologia ágil TDD e como usar frameworks de testes.

Dev Media: <https://www.devmedia.com.br/test-driven-development-tdd-simples-e-pratico/18533>

Descompila: <https://www.youtube.com/watch?v=x40DQ5TyCEY> - JUnit
Dmitry Skibitsky: <https://www.youtube.com/watch?v=1RL9ZvhD17k> - PHPUnit


 

