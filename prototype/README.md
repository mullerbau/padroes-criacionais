# Padrão de Projeto: Prototype

O **Prototype** é um padrão de projeto criacional que permite a cópia ou "clonagem" de objetos existentes, sem que o código que faz a cópia precise conhecer as classes específicas desses objetos.

Isso reduz dependências e melhora o encapsulamento, já que o objeto original não precisa ser exposto ou modificado a todo momento; em vez disso, trabalhamos com seus clones.

---

## Como ele faz isso?

O padrão funciona definindo um método **`clone()`** no objeto que servirá como protótipo.

Quando um novo objeto é necessário, em vez de criá-lo do zero (com o operador `new`), simplesmente chamamos o método **`clone()`** do protótipo. Este método é responsável por criar uma nova instância e copiar os dados do objeto original para a nova.

Assim, o clone nasce com o mesmo estado do original, pronto para ser usado ou modificado de forma independente.

---

## Exemplo de código:

Este exemplo em **Java** mostra a implementação clássica usando a interface `Cloneable` em uma classe `Carro`.

```java
// 1. A classe do inimigo implementa a interface Cloneable
class Inimigo implements Cloneable {
    private String tipo;
    private int vida;
    private int dano;

    public Inimigo(String tipo, int vida, int dano) {
        this.tipo = tipo;
        this.vida = vida;
        this.dano = dano;
        // Simula um processo custoso, como carregar a IA ou modelo 3D
        System.out.println("-> Criando protótipo para '" + tipo + "' (processo custoso)...");
    }

    // Métodos para modificar os clones e criar variações
    public void setVida(int vida) {
        this.vida = vida;
    }
    
    public void setTipo(String tipo) {
        this.tipo = tipo;
    }

    @Override
    public String toString() {
        return "Inimigo[tipo='" + tipo + "', vida=" + vida + ", dano=" + dano + "]";
    }

    // 2. Sobrescrevemos o método clone() para criar cópias rápidas
    @Override
    public Inimigo clone() {
        System.out.println("   Clonando '" + this.tipo + "'...");
        try {
            // super.clone() realiza a cópia superficial do objeto
            return (Inimigo) super.clone();
        } catch (CloneNotSupportedException e) {
            // Esta exceção não deveria acontecer se a classe implementa Cloneable
            return null;
        }
    }
}

// 3. Cliente (o motor do jogo) que utiliza o padrão
public class Main {
    public static void main(String[] args) {
        // A criação original e custosa do protótipo acontece apenas uma vez
        Inimigo prototipoDeOrc = new Inimigo("Orc Guerreiro", 100, 15);

        System.out.println("\n--- Gerando uma horda de inimigos a partir do protótipo ---");

        // Os clones são criados de forma rápida para popular o jogo
        Inimigo orc1 = prototipoDeOrc.clone();
        Inimigo orc2 = prototipoDeOrc.clone();
        
        // Criamos uma variação (um chefe) a partir do mesmo protótipo
        Inimigo chefeOrc = prototipoDeOrc.clone();
        chefeOrc.setTipo("Chefe Orc");
        chefeOrc.setVida(250); // Modificamos apenas o clone

        System.out.println("\n--- Horda criada ---");
        System.out.println("Protótipo Original: " + prototipoDeOrc);
        System.out.println("Clone 1: " + orc1);
        System.out.println("Clone 2: " + orc2);
        System.out.println("Clone modificado (Chefe): " + chefeOrc);
    }
}
```