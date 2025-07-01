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

class Inimigo implements Cloneable {
    private String tipo;
    private int vida;
    private int dano;

    public Inimigo(String tipo, int vida, int dano) {
        this.tipo = tipo;
        this.vida = vida;
        this.dano = dano;
        
        System.out.println("-> Criando protótipo para '" + tipo + "' (processo custoso)...");
    }

    
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

    
    @Override
    public Inimigo clone() {
        System.out.println("   Clonando '" + this.tipo + "'...");
        try {
            
            return (Inimigo) super.clone();
        } catch (CloneNotSupportedException e) {
            
            return null;
        }
    }
}


public class Main {
    public static void main(String[] args) {
        
        Inimigo prototipoDeOrc = new Inimigo("Orc Guerreiro", 100, 15);

        System.out.println("\n--- Gerando uma horda de inimigos a partir do protótipo ---");

        
        Inimigo orc1 = prototipoDeOrc.clone();
        Inimigo orc2 = prototipoDeOrc.clone();
        
        
        Inimigo chefeOrc = prototipoDeOrc.clone();
        chefeOrc.setTipo("Chefe Orc");
        chefeOrc.setVida(250); 

        System.out.println("\n--- Horda criada ---");
        System.out.println("Protótipo Original: " + prototipoDeOrc);
        System.out.println("Clone 1: " + orc1);
        System.out.println("Clone 2: " + orc2);
        System.out.println("Clone modificado (Chefe): " + chefeOrc);
    }
}
```