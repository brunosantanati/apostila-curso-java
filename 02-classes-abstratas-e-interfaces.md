### Classes Abstratas

Uma classe abstrata não pode ser instanciada, em outras palavras, você não pode usar new para criar objetos a partir dela. Criamos classes desse tipo para serem estendidas por outras classes.

Se você deseja tornar uma classe abstrata basta usar a palavra abstract em sua definição:

```java
public abstract class Animal { }
```
Uma classe definida como abstrata pode ter métodos igualmente abstratos(sem implementação) e métodos não abstratos(com implementação). Os métodos abstratos serão sobrescritos e implementados pelas filhas da classe abstrata. Quando usamos a palavra filhas nesse contexto, quer dizer as classes concretas que irão herdar da classe abstrata(usando a palavra extends). Vejamos um exemplo para ficar tudo mais claro.

Iremos criar uma classe Animal que terá uma variável mamifero do tipo boolean para guardar um valor true ou false indicando se o animal é ou não é um mamífero. Criaremos um getter e um setter para essa variável também para manter o encapsulamento. Além disso a classe Animal terá um método comer() que não será abstrato pois vamos aplicar um comportamento exatamente igual para todos animais que herdarem dessa classe. Afinal para esse programa não nos importa qualquer diferença entre o modo de comer de cada animal, portanto teremos um comportamento comer() mais genérico que serve para todos. Já o outro método chamado fazerSom() será marcado como abstract pois cada animal faz um som diferente(alguns relincham, outros rugem, etc). Portanto o comportamento de fazer algum som terá que ser implementado nas classes filhas.

####### Animal.java

```java
public abstract class Animal {
	
	private boolean mamifero;

	public boolean isMamifero() {
		return mamifero;
	}

	public void setMamifero(boolean mamifero) {
		this.mamifero = mamifero;
	}
	
	public void comer() {
		System.out.println("comendo...");
	}
	
	public abstract void fazerSom();

}
```
Agora que temos a classe Animal criada mas não podemos "dar new" nela, vamos criar uma classe concreta - entenda por concreta uma classe não abstrata - que irá estender Animal. Veja como poderia ser uma classe Cavalo que sobrescreve o método fazerSom() da classe pai Animal.

####### Cavalo.java

```java
public class Cavalo extends Animal {

	@Override
	public void fazerSom() {
		System.out.println("relinchando...");		
	}

}
```

Podemos criar uma segunda classe que herda de Animal, nesse caso Leao, e que também irá prover sua própria implementação do método fazerSom().

####### Leao.java

```java
public class Leao extends Animal {

	@Override
	public void fazerSom() {
		System.out.println("rugindo...");		
	}

}
```

Agora uma classe chamada Principal que tem o método main onde vamos testar tudo que fizemos até agora. Veja que tanto a classe Cavalo como a classe Leao, herdaram todas as coisas da classe Animal. Além disso elas forneceram sua própria lógica para fazerSom().

####### Principal.java

```java
public class Principal {

	public static void main(String[] args) {
		// Animal a = new Animal(); //Isso resultaria em ERRO de compilação
		
		Cavalo c = new Cavalo();
		c.setMamifero(true);
		c.comer();
		c.fazerSom();
		System.out.println("cavalo eh mamifero? " + c.isMamifero());
		
		Leao l = new Leao();
		l.setMamifero(true);
		l.comer();
		l.fazerSom();
		System.out.println("leao eh mamifero? " + c.isMamifero());
	}

}
```
O código acima gera o seguinte output:

```sh
comendo...
relinchando...
cavalo eh mamifero? true
comendo...
rugindo...
leao eh mamifero? true
```

É importante dizer que se apenas um método for abstrato, a classe deve ser abstrata. Também é válido ressaltar que uma classe abstract não pode ser final ao mesmo tempo, já que são coisas opostas.

### Interfaces

Considere uma interface como uma classe 100% abstrata, porém você deve utilizar a palavra interface no lugar de class na sua definição:

```java
public interface Carro { }
```
As variáveis declaradas em uma interface são sempre constantes, ou seja, mesmo que não especifiquemos elas são sempre public static final.

Os métodos declarados em uma interface são sempre públicos e abstratos, independente de indicarmos isso ou não.

```java
public interface Carro {
	
	int quantidadeDeRodas = 4; //é implicitamente public static final
	public static final String paisDeFabricacao = "Brasil"; //declarando de forma mais explícita
	
	void acelerar(); //implicitamente public abstract
	public abstract void freiar(); //declarando de forma mais explícita

}
```

Alguns pontos importantes:

- Os métodos declarados em uma interface são abstratos, portanto não podem ser final.
- Uma interface pode estender uma ou mais interfaces.
- Uma interface não pode estender nada que não seja uma interface.
- Uma interface não pode implementar nem outra interface nem outra classe.
- Posso usar a palavra abstract na definição da interface, mas isso é considerado redundante, pois as interfaces são implicitamente abstract.