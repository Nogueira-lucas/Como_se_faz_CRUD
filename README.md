# Como se faz um CRUD - LUCAS NOGUEIRA, 2019.

### Essa é a minha exposição de aprendizado que gostaria de compartilhar em forma de etapas.

# PASSOS PARA APRENDER A DESENVOLVER CRUD EM QUALQUER LINGUAGEM DE PROGRAMAÇÃO

Decidi estruturar meu manual em etapas com alguns exemplos de código para facilitar a imersão.

## 1. Escolha sua linguagem Back-end:
Recomendo:	
- JAVA
- PHP

> Obs.: é muito bom possuir uma noção de Orientação a Objetos. Caso não tenha ainda, recomendo muito as aulas do professor Guanabara (Segue o link abaixo)

## 2. Escolha um SGBD relacional de sua preferencia (Sistema gerenciador de banco de dados)
- PostgreSQL
- MySQL
- Access
- SQL Server
- Oracle Database
- MariaDB

## 3. Encontre o driver de conexão entre o banco de dados e aplicação:

Procure na documentação exatamente essas funções:

- Como conectar-se ao banco de dados;
- Como fechar conexao;
- Como acionar comandos SQL com a linguagem; (criação, alteração, exclusão e visualização);

> Dica: caso a documentação esteja confusa demais procure em foruns, video-aulas ou pergunte a um colega da comunidade de sua preferencia.	

## 4. Crie seu modelo relacional do banco de dados (crie suas tabelas)
  
## 5. Crie sua fábrica de conexão
    
    public class FabricaConexao {
    
	    private static final String DRIVER  = "org.postgresql.Driver";
	    private static final String URL     = "jdbc:postgresql://localhost:5432/db_teste";
	    private static final String USER    = "postgres";
	    private static final String PASS    = "1234";

	    public static Connection getConexao(){

		try {
		    Class.forName(DRIVER);
		    return DriverManager.getConnection(URL, USER, PASS);
		} catch (ClassNotFoundException | SQLException e){
		    throw new RuntimeException("Erro de conexão", e);
		}
	    }

	    public static void fecharConexao(Connection conn){
		if(conn != null){    
		    try {
			conn.close();
		    } catch (SQLException ex) {
			System.err.println("Erro ao fechar conexao"+ex.getMessage());
		    }
	    }
    }

## 6. Crie suas classes de domínio

public class Cliente {
    private Integer id;
    private String nome;
    private String email;
    private String cpf;

    public Cliente(){
        
    }
    
    public Cliente(String nome, String email, String cpf) {
        this.nome = nome;
        this.email = email;
        this.cpf = cpf;
    }
    
    public Cliente(Integer id, String nome, String email, String cpf) {
        this.id = id;
        this.nome = nome;
        this.email = email;
        this.cpf = cpf;
    }
    
    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getCpf() {
        return cpf;
    }

    public void setCpf(String cpf) {
        this.cpf = cpf;
    }

}


## 7. Crie as classes DAO a partir das classes de dominio:

public class ClienteDAO {
    
    private Connection conn = null;

    public ClienteDAO() {
        conn = FabricaConexao.getConexao();
    }
    
    public boolean salvar(Cliente cliente){
        String sql = "INSERT INTO tb_cliente(nome, email, cpf) VALUES(?,?,?)";
        PreparedStatement stmt = null;
        
        try {
            stmt = conn.prepareStatement(sql);
            
            stmt.setString(1, cliente.getNome());
            stmt.setString(2, cliente.getEmail());
            stmt.setString(3, cliente.getCpf());
            
            stmt.executeUpdate();
            return true;
        } catch (SQLException ex) {
            System.err.println("Erro ao salvar :"+ex);
            return false;
        }finally{
            FabricaConexao.fecharConexao(conn);
        }
    }
    
    public boolean atualizar(Cliente cliente){
        
        String sql = "UPDATE tb_cliente "
                    + "SET nome=?, email=?, cpf=?"
                    + "WHERE(id=?)";
        PreparedStatement stmt = null;
        
        try{
            stmt = conn.prepareStatement(sql);
            
            stmt.setString(1, cliente.getNome()  );
            stmt.setString(2, cliente.getEmail() );
            stmt.setString(3, cliente.getCpf()   );
            stmt.setInt(4,cliente.getId()        );
            
            stmt.execute();
            return true;
        }catch(Exception ex){
            System.err.println("Erro ao atualizar"+ex);
            return false;
        }finally{
            FabricaConexao.fecharConexao(conn);
        }
    }
    
    public void excluir(Cliente cliente){
        String sql = "DELETE FROM tb_cliente WHERE(nome = ? and email = ? and cpf = ?)";
        PreparedStatement stmt;
        
        try{
            stmt = conn.prepareStatement(sql);
            
            stmt.setString(1, cliente.getNome());
            stmt.setString(2, cliente.getEmail());
            stmt.setString(3, cliente.getCpf());
            
            stmt.executeUpdate();
        }catch(Exception ex){
            System.err.println("Erro ao excluir: "+ex);
        }finally{
            FabricaConexao.fecharConexao(conn);
        }
    }
    
    public ArrayList<Cliente> listarTodos(){
        String sql = "SELECT * FROM tb_cliente";
        
        PreparedStatement stmt = null;
        ResultSet rs = null;
        ArrayList<Cliente> clientes = new ArrayList<>();
        
        try {
            stmt = conn.prepareStatement(sql);
            rs = stmt.executeQuery();
            
            while(rs.next()){
                Cliente cliente = new Cliente();
                
                cliente.setId(rs.getInt("id"));
                cliente.setNome(rs.getString("nome"));
                cliente.setEmail(rs.getString("email"));
                cliente.setCpf(rs.getString("cpf"));
                
                clientes.add(cliente);   
            }
        } catch (SQLException ex) {
            System.err.println("Erro ao listar dados: "+ex);
        }finally{
            FabricaConexao.fecharConexao(conn, stmt, rs);
        }
        return clientes;
    }
    
}

> Dica: se você está nos primeiros passos tente com apenas uma unica entidade de dominio e uma unica entidade relacional para ficar mais facil de aprender.

## 8. Se você estiver trabalhando com interface gráfica lembre-se que você pode envolver Orientação a Eventos então procure separar o que é interface gráfica das classes de dominio para ficar mais fácil de focar sua lógica de programação.

> Obs.: pensei dessa forma já que o nível lógico de acionar comandos sql entre tratar dados do formulario são duas coisas completamente diferentes. Acredito que existe uma relação muito forte com as interfaces gráficas(janelinhas) e os eventos como 'clicar', 'carregar nova janela'...

## 9. Crie uma rotina de testes para executar metodos DAO
	
Isso ajuda você a comprender seu código com mais rapidez e realizar testes em poucos segundos. Deixando de lado o "teste1", "teste2" na sua base de dados e te premiando com mais tempo para focar no seu aprendizado.

> Obs.: É importante já ficar sabendo que é possivel testar seu código com auxílio de frameworks de teste unitários;

> Ok, talvez você não conheça todas as ferramentas e técnicas que eu citei. 

Segue uma lista carinhosamente recomendada por mim de um material super bacana pra conseguir fazer seu primeiro CRUD Orientado a Objetos, Padrão DAO com MVC e Testes Unitários. 

## MATERIAL COMPLEMENTAR

### Aprenda Orientação a Objetos, CURSO EM VIDEO. 

- CURSO EM VIDEO <https://www.youtube.com/watch?v=KlIL63MeyMY&list=PLHz_AreHm4dkqe2aR0tQK74m8SFe-aGsY>

### Aprenda o que são classes de domínio.
	
- Atributos em Diagramas de Modelagem de Dominio 
<https://www.ibm.com/support/knowledgecenter/pt-br/SS8PJ7_9.1.1/com.ibm.xtools.viz.class.diagram.doc/topics/cattributes.html>

### Guia dos comandos SQL, W3SCHOOLS. 
- W3SCHOOLS <https://www.w3schools.com/sql/default.asp>

### Guia de modelagem de bancos de dados relacionais. 

- CURSO EM VIDEO <https://www.youtube.com/watch?v=Ofktsne-utM&list=PLHz_AreHm4dkBs-795Dsgvau_ekxg8g1r>

### Aprenda o que é uma Fabrica de Conexão e o Desing Pattern Factory
	
- DevMedia: <https://www.devmedia.com.br/design-patterns-factory/17158>	
- Wiki: <https://pt.wikipedia.org/wiki/Factory_Method>

### Aprenda o  que é o Desing Pattern DAO e como usar.

- Tutorials Point: <https://www.tutorialspoint.com/design_pattern/data_access_object_pattern.htm>
### Aprenda o que é o padrão MVC e como usar.
- Tableless : <https://tableless.com.br/mvc-afinal-e-o-que/>

### Aprenda o que é a metodologia ágil TDD e como usar frameworks de testes.

- Dev Media: <https://www.devmedia.com.br/test-driven-development-tdd-simples-e-pratico/18533>
- Descompila: <https://www.youtube.com/watch?v=x40DQ5TyCEY> - JUnit
- Dmitry Skibitsky: <https://www.youtube.com/watch?v=1RL9ZvhD17k> - PHPUnit

LUCAS NOGUEIRA, 2019.
 
