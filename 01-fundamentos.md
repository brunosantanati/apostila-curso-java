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

### Encapsulamento

modificadores de acesso private e public em membros da classe
getters e setters

### Modificadores de Acesso Para Classes

(padrão/nível de acesso de pacote e público)

### Herança

### Modificadores de Acesso Para Membros de uma Classe

(público, protegido, padrão e privado) --->