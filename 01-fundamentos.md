### Hello World em Java

Como de praxe iremos fazer o famoso Hello World, algo comum quando estamos aprendendo uma nova linguagem.

Abra seu editor de texto preferido e digite o código abaixo:

####### MinhaPrimeiraClasseJava.java

```java
public class MinhaPrimeiraClasseJava 
{
    public static void main( String[] args ){
		System.out.println("Hello World!");
    }
}
```

Salve o arquivo como MinhaPrimeiraClasseJava.java. Abra o terminal ou prompt de comando de seu sistema operacional, vá até a pasta onde salvou o arquivo e execute:

```sh
javac MinhaPrimeiraClasseJava.java
```
Isso irá gerar um arquivo `MinhaPrimeiraClasseJava.class` que é um arquivo compilado com bytecodes dentro. Para executar esse arquivo compilado(isso só é possível pois o arquivo que o originou tem um método main) execute:

```sh
java MinhaPrimeiraClasseJava
```
Verá a seguinte saída no terminal:

```sh
Hello World!
```
Parabéns! Você compilou e executou seu primeiro programa Java!

### Classes e Objetos

Antes de nos aventurarmos a aprender uma nova linguagem orientada a objetos, é primordial que aprendamos alguns conceitos fundamentais sobre orientação a objetos.

Dois conceitos muito importantes são classes e objetos. Podemos abordar essas questões pensando sobre os objetos físicos ao nosso redor como por exemplo um televisor, um computador ou uma bicicleta.

Todo objeto do mundo real compartilha duas características: possui estado e comportamento. Uma televisão possui estado(ligada ou desligada, canal no qual está sintonizada, volume atual, etc) e comportamento(ser ligada, ser desligada, trocar de canal, aumentar volume, etc).

No paradigma orientado a objetos iremos modelar objetos do mundo real dentro do nosso código. Para modelar uma televisão dentro de um software podemos contar com uma classe, que será composta por seus membros. Temos membros conhecidos como campos, que são variáveis, que irão representar o estado e membros conhecidos como métodos, análogos as funções de outras linguages, que irão representar os comportamentos.

####### Televisao.java

```java
public class Televisao{

	//os campos abaixo representam o estado
	boolean ligada;
	int canal;
	int volume;
	
	//os métodos abaixo representam os comportamentos
	void ligar(){
		//código para ligar a TV
	}
	
	void desligar(){
		//código para desligar a TV
	}
	
	void trocarDeCanal(int canal){
		//código para trocar de canal
	}
	
	void aumentarVolume(){
		volume = volume + 1; 
	}
	
	@Override
	public String toString() {
		return "Televisao [ligada=" + ligada + ", canal=" + canal + ", volume=" + volume + "]";
	}
	
}
```
Essa classe chamada Televisao será a base para criarmos quantos objetos quisermos. Para criar um objeto em Java usamos a palavra new. Existem termos muitos comuns que com certeza irá ouvir ou já ouviu, que são instância e instanciar. Um objeto criado a partir de uma classe é uma instância daquela classe. Em outras palavras, quando criamos um novo objeto estamos instanciando uma classe. Na prática podemos fazer assim:

```java
// criando um objeto, ou seja, instanciando a classe Televisao
Televisao tv1 = new Televisao();
// mudando o estado do objeto
tv1.ligada = true;
tv1.canal = 4;
tv1.volume = 50;
// chamando método para executar um comportamento/ação
tv1.aumentarVolume();
// imprime objeto no console
System.out.println(tv1);

// criando outro objeto, ou seja, criando outra instância
Televisao tv2 = new Televisao();
// mudando o estado do objeto, ou seja,
// alterando os valores das variáveis de instância
tv2.ligada = true;
tv2.canal = 5;
tv2.volume = 70;
// imprime objeto no console
System.out.println(tv2);
```
Para melhor compreensão podemos dizer que os as classes ditam como nossos objetos serão, quais características eles terão(campos) e quais ações eles serão capazes de fazer(métodos). No exemplo acima, os objetos criados a partir da classe Televisao tem características em comum, como por exemplo ambos possuem um canal, mas enquanto um objeto mantém o valor 4 em sua variável canal, o outro mantém o valor 5. Portanto embora todos objetos compartilhem coisas em comum definidas na classe que os originou, eles mantém valores diferentes em suas variáveis, ou seja, mantém estados diferentes.

### Encapsulamento

Iremos começar pela [definição de encapsulamento encontrada nesse link da Oracle](https://docs.oracle.com/javase/tutorial/java/concepts/object.html): "Ocultar o estado interno e exigir que toda a interação seja realizada através dos métodos de um objeto é conhecido como encapsulamento de dados - um princípio fundamental da programação orientada a objetos.".

Vamos entender melhor essa afirmação na prática. Veja que no exemplo anterior as variáveis de instância da classe Televisao não tem modificadores de acesso(private, public e protected), o que permite que seus valores sejam modificados diretamente por algum código externo a essa classe(nesse caso qualquer código em outra classe no mesmo pacote, pois na ausência da declaração de um modificador de acesso de forma explícita, o Java assume visibilidade apenas dentro do mesmo pacote).

```java
//Esse código está fora da classe Televisao
Televisao tv1 = new Televisao();
// Ops, a classe Televisao permitiu acesso direto as suas variáveis
tv1.ligada = true;
tv1.canal = 4;
tv1.volume = 50;
```
Programar do jeito acima fere o princípio do encapsulamento e causa alguns problemas:

- Isso permite que sejam atribuídos valores inapropriados as variáveis, exemplo: ``tv1.volume = -50;``
- Se quisesse adicionar uma validação afim de assegurar que está sendo atribuido um valor válido a variável, ou executar um processamento a cada mudança nessa variável, deixando qualquer código acessar a variável diretamente certamente dificultará a realização de tarefas como as exemplificadas.
- Se a implementação interna da classe Televisao mudar e removermos a variável de instância volume, iria quebrar muitas partes do sistema que utilizam essa variável, pois essas outras partes do sistema conhecem mais do que deveriam sobre a implementação interna de Televisao.
- <s>Adicionar outras coisas aqui para assustar os programadores que ainda quiserem programar dessa forma <insira risada malígna></s>

Portanto um passo na direção do encapsulamento seria declarar as variáveis de instância da classe como privadas e permitir o acesso a elas apenas através de métodos públicos. O método para recuperar o valor da variável tem o padrão de nomenclatura getNomeDaPropriedade, e o método para atribuir um valor a variável tem o padrão de nomenclatura setNomeDaPropriedade. Esses tipos de método são conhecidos no mundo Java como getters e setters. Uma observação importante seria que o padrão de nomenclatura geralmente adotado para recuperar valores de campos do tipo boolean é isNomeDaPropriedade. Vejamos como ficaria nossa classe com essa alteração:

```java
public class Televisao{

	private boolean ligada;
	private int canal;
	private int volume;
	
	public boolean isLigada() {
		return ligada;
	}

	public void setLigada(boolean ligada) {
		this.ligada = ligada;
	}

	public int getCanal() {
		return canal;
	}

	public void setCanal(int canal) {
		this.canal = canal;
	}

	public int getVolume() {
		return volume;
	}

	public void setVolume(int volume) {
		this.volume = volume;
	}
	
	//restante do código...
}
```

Agora podemos testar nossa classe refatorada usando o seguinte código:

```java
public class TestaTelevisao {

	public static void main(String[] args) {
		
		//instanciando objeto
		Televisao tv = new Televisao();
		
		//usando setters
		tv.setLigada(true);
		tv.setCanal(4);
		tv.setVolume(50);
		tv.aumentarVolume();
		
		//usando getters
		System.out.println("Televisao -> ligada=" + tv.isLigada() +
				" canal=" + tv.getCanal() + " volume=" + tv.getVolume());
	}

}
```
O código acima imprime:

```sh
Televisao -> ligada=true canal=4 volume=51
```

Com esse ajuste na classe, agora ficou fácil criar uma validação para volume toda vez que alguém tentar alterá-lo, já que a única forma de alterá-lo de fora da classe é usando o método público setVolume. Em outras palavras, sabemos que qualquer tentativa de alteração de volume passará pelo código do método setVolume, portanto basta incluirmos uma validação ali:

```java
	public void setVolume(int volume) {
		
		if(volume < 0)
			throw new IllegalArgumentException("Volume não pode ser menor que zero");
		
		this.volume = volume;
	}
```

Agora se tentarmos "setar" uma valor negativo para volume, portanto inválido, será lançada uma exception do tipo IllegalArgumentException:

```java
Televisao tv = new Televisao();
tv.setVolume(-10); //Essa linha agora irá causar o lançamento de uma IllegalArgumentException
```
Output no console:

```sh
Exception in thread "main" java.lang.IllegalArgumentException: Volume não pode ser menor que zero
	at me.brunosantana.codigo_apostila_curso_java.chapter01.encapsulamento_validation.Televisao.setVolume(Televisao.java:32)
	at me.brunosantana.codigo_apostila_curso_java.chapter01.encapsulamento_validation.TestaTelevisao.main(TestaTelevisao.java:9)
```
Como vimos acima os métodos getters e setters tem relação com o encapsulamento, mas o conceito de encapsulamento é mais abrangente do que isso. O conceito é encapsular como as coisas são feitas, e expor uma API pública da classe para que ela seja usada. Em outras palavras devemos esconder as variáveis de instância da classe e ocultar as implementações internas da classe, deixando exposto de forma pública apenas o mínimo necessário para que a classe seja usada. Assim alterações internas na classe não quebram os códigos que a utilizam. Também asseguramos que os códigos externos também não quebrem o código de dentro da classe atribuindo valores inválidos a suas variáveis.

Por exemplo poderíamos até mesmo deletar o método setVolume da classe Televisao, e permitir a alteração do volume apenas através dos métodos aumentarVolume e diminuirVolume como é comum nos televisores. Assim quem está utilizando a classe Televisao nem precisa saber que internamente essa classe tem uma variável volume, basta saber que tem dois métodos expostos que possibilitam o aumento ou diminuição do volume, sem se preocupar como é a implementação interna dessa lógica.

```java
//setVolume apagado

public void aumentarVolume(){
	volume = volume + 1; 
}

public void diminuirVolume() {
	volume = volume - 1;
}
```
Vamos testar a alteração:

```java
Televisao tv = new Televisao();
System.out.println("volume: " + tv.getVolume());

tv.aumentarVolume();
tv.aumentarVolume();
System.out.println("volume: " + tv.getVolume());

tv.diminuirVolume();
System.out.println("volume: " + tv.getVolume());
```
O código acima imprime no console:

```sh
volume: 10
volume: 12
volume: 11
```

### Exercício Encapsulamento

Temos a seguinte classe que representa uma HQ(revista de história em quadrinhos):

```java
import java.math.BigDecimal;

public class HQ {
	
	public String nome;
	public BigDecimal preco;
	public String roteirista;
	public String artista;
	public String ISBN;
	
	@Override
	public String toString() {
		return "HQ: \nnome=" + nome + "\npreco=" + preco + "\nroteirista=" + roteirista + "\nartista=" + artista
				+ "\nISBN=" + ISBN + "";
	}

}
```
Imagine também que a Panini, editora de revistas em quadrinhos fornece um serviço que retorna os dados de uma HQ, apenas precisamos passar o ISBN:

```java
import java.util.HashMap;
import java.util.Map;

public class PaniniService {
	
	private final static String O_REI_DA_COZINHA_DO_INFERNO_ISBN = "9788583681595";
	private final static String BATMAN_ANO_ZERO = "9788583682325";
	
	public Map<String, String> getDadosHQByIsbn(String IsbnHQ) {
		
		Map<String, String> infoHQ = new HashMap<>();
		
		switch (IsbnHQ) {
		case O_REI_DA_COZINHA_DO_INFERNO_ISBN:
			infoHQ.put("nome", "O Rei da Cozinha do Inferno");
			infoHQ.put("preco", "50.00");
			infoHQ.put("roteirista", "Brian Michael Bendis");
			infoHQ.put("artista", "Alex Maleev");
			infoHQ.put("ISBN", O_REI_DA_COZINHA_DO_INFERNO_ISBN);
			break;
		case BATMAN_ANO_ZERO:
			infoHQ.put("nome", "Batman: Ano Zero");
			infoHQ.put("preco", "70.00");
			infoHQ.put("roteirista", "Scott Snyder");
			infoHQ.put("artista", "Greg Capullo");
			infoHQ.put("ISBN", BATMAN_ANO_ZERO);
			break;
		}
		
		return infoHQ;
	}

}
```
Toda vez que em nosso programa precisamos criar uma HQ executamos um código parecido com esse:

```java
import java.math.BigDecimal;
import java.util.Map;

public class Principal {

	public static void main(String[] args) {
		
		PaniniService service = new PaniniService();
		Map<String, String> dadosHQ = service.getDadosHQByIsbn("9788583681595");
		
		HQ hq = new HQ();
		hq.nome = dadosHQ.get("nome");
		hq.preco = new BigDecimal(dadosHQ.get("preco"));
		hq.roteirista = dadosHQ.get("roteirista");
		hq.artista = dadosHQ.get("artista");
		hq.ISBN = dadosHQ.get("ISBN");
		
		System.out.println(hq);

	}

}
```

Temos dois problemas principais nesse código que iremos ter que resolver através do encapsulamento.

- O primeiro problema que deve resolver é criar os getters e setters na classe HQ e passar a usá-los no lugar de acessarmos diretamente as variáveis de instância da classe.
- O segundo problema é que em todos lugares do código que precisarmos criar uma HQ teremos um código repetitivo e isso se transformará em um pesadelo de manutenção <s>SOCORRO!!!</s>. Seu trabalho será encapsular esse código que chama o serviço da Panini e popula os valores na HQ em um método da própria classe HQ. Assim essa lógica ficará isolada do restante do código e centralizada em um lugar só que estará encapsulado. O método deve se chamar consumirPaniniService.

Exemplo de como deverá ser chamado o método consumirPaniniService:
 
```java
hq.consumirPaniniService("9788583682325");
```

Além disso você também deve fazer uma validação dentro de setPreco para evitar que seja atribuido um valor negativo ao preço da revista. Caso seja passado ao método setPreco um valor negativo, será lançada uma IllegalArgumentException.

```java
hq.setPreco(new BigDecimal("-10.00")); //Isso deverá produzir uma IllegalArgumentException

```

### Solução do Exercício Encapsulamento

####### PaniniService.java (não mudou)

```java
//O código dessa classe não mudou e foi omitido
```

####### HQ.java

```java
import java.math.BigDecimal;
import java.util.Map;

public class HQ {
	
	private String nome;
	private BigDecimal preco;
	private String roteirista;
	private String artista;
	private String ISBN;

	public String getNome() {
		return nome;
	}

	public void setNome(String nome) {
		this.nome = nome;
	}

	public BigDecimal getPreco() {
		return preco;
	}

	public void setPreco(BigDecimal preco) {
		
		if(preco.compareTo(BigDecimal.ZERO) == -1) {
			throw new IllegalArgumentException("Preço inválido");
		}
		
		this.preco = preco;
	}

	public String getRoteirista() {
		return roteirista;
	}

	public void setRoteirista(String roteirista) {
		this.roteirista = roteirista;
	}

	public String getArtista() {
		return artista;
	}

	public void setArtista(String artista) {
		this.artista = artista;
	}

	public String getISBN() {
		return ISBN;
	}

	public void setISBN(String iSBN) {
		ISBN = iSBN;
	}

	@Override
	public String toString() {
		return "HQ: \nnome=" + nome + "\npreco=" + preco + "\nroteirista=" + roteirista + "\nartista=" + artista
				+ "\nISBN=" + ISBN + "";
	}
	
	public void consumirPaniniService(String IsbnHQ) {
		
		PaniniService service = new PaniniService();
		Map<String, String> dadosHQ = service.getDadosHQByIsbn(IsbnHQ);
		
		this.nome = dadosHQ.get("nome");
		this.preco = new BigDecimal(dadosHQ.get("preco"));
		this.roteirista = dadosHQ.get("roteirista");
		this.artista = dadosHQ.get("artista");
		this.ISBN = dadosHQ.get("ISBN");
	}

}
```

####### Principal.java

```java
import java.math.BigDecimal;

public class Principal {

	public static void main(String[] args) {
		
		HQ hq = new HQ();
		hq.consumirPaniniService("9788583682325");		
		System.out.println(hq);

		hq.setPreco(new BigDecimal("-10.00")); //Isso deve produzir uma IllegalArgumentException
	}

}
```
<!--- modificadores de acesso private e public em membros da classe --->
<!--- 

### Configurar Variáveis de Ambiente

### Construtores

### Pacotes

### Identificadores Legais

### Convenções de Código

### Regras Para Arquivos Fonte

regras de declaração para arquivos fonte

### Eclipse IDE

criar projeto do tipo JavaProject no Eclipse

### Modificadores de Acesso Para Classes

(padrão/nível de acesso de pacote e público)

### Herança

### Modificadores de Acesso Para Membros de uma Classe

(público, protegido, padrão e privado) --->