# Factory Method

**Factory Method:**

A intenção do Factory Method é delegar a criação de objetos para subclasses, ao invés de instanciar diretamente no código com `new`. Dessa forma, o código fica mais flexível, desacoplado e preparado para futuras mudanças ou expansões.
Além disso, o uso desse padrão melhora a organização e o encapsulamento, pois o código principal não precisa conhecer os detalhes das classes concretas que estão sendo criadas.


**Como ele faz isso?**

O Factory Method funciona ao criar uma **classe abstrata ou interface** que define um método para criar objetos. As subclasses concretas implementam esse método, decidindo qual objeto exatamente será criado.
Dessa forma, o código principal só chama o método da fábrica e recebe o objeto pronto, sem precisar saber o que está sendo instanciado diretamente.
