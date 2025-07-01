# 🏭 Padrão de Projeto: Abstract Factory

## 📘 O que é?

O **Abstract Factory** é um padrão de projeto criacional que fornece uma interface para criar **famílias de objetos relacionados ou dependentes** sem especificar suas classes concretas.

Ele é útil quando você precisa garantir que os produtos criados em conjunto sejam compatíveis entre si.

---

## 🚫 Exemplo **sem** o uso de Abstract Factory

```python
class BotaoWindows:
    def render(self):
        print("Renderizando botão no estilo Windows")

class BotaoMac:
    def render(self):
        print("Renderizando botão no estilo Mac")

sistema = input("Sistema operacional (windows/mac): ")

if sistema == "windows":
    botao = BotaoWindows()
elif sistema == "mac":
    botao = BotaoMac()
else:
    botao = None

if botao:
    botao.render()
```

### ❌ Problemas:
- O cliente está **acoplado** às classes concretas.
- Para cada novo tipo de sistema, o cliente precisa ser modificado.
- Nenhuma garantia de que os produtos pertencem à mesma família.

---

## ✅ Exemplo **com** o padrão Abstract Factory

```python
class Botao:
    def render(self):
        pass

class Janela:
    def abrir(self):
        pass

class BotaoWindows(Botao):
    def render(self):
        print("Renderizando botão no estilo Windows")

class JanelaWindows(Janela):
    def abrir(self):
        print("Abrindo janela no estilo Windows")

class BotaoMac(Botao):
    def render(self):
        print("Renderizando botão no estilo Mac")

class JanelaMac(Janela):
    def abrir(self):
        print("Abrindo janela no estilo Mac")

class GUIFactory:
    def criar_botao(self):
        pass

    def criar_janela(self):
        pass

class WindowsFactory(GUIFactory):
    def criar_botao(self):
        return BotaoWindows()

    def criar_janela(self):
        return JanelaWindows()

class MacFactory(GUIFactory):
    def criar_botao(self):
        return BotaoMac()

    def criar_janela(self):
        return JanelaMac()

def rodar_interface(factory: GUIFactory):
    botao = factory.criar_botao()
    janela = factory.criar_janela()
    botao.render()
    janela.abrir()

sistema = input("Sistema operacional (windows/mac): ")

if sistema == "windows":
    factory = WindowsFactory()
elif sistema == "mac":
    factory = MacFactory()
else:
    factory = None

if factory:
    rodar_interface(factory)
```

### ✅ Vantagens:
- O cliente trabalha apenas com interfaces abstratas, **sem depender das classes concretas**.
- É fácil **adicionar novas famílias** de produtos sem modificar o código cliente.
- Garante que os produtos criados são **compatíveis entre si**.

---

## ⚖️ Pontos Fortes e Fracos do Abstract Factory

### ✅ Pontos Fortes:
- Garante **coerência entre objetos** criados em conjunto.
- Desacopla o código cliente da implementação concreta.
- Facilita a **troca de famílias inteiras** de produtos.

### ❌ Pontos Fracos:
- Mais classes e complexidade estrutural.
- Difícil de manter se você precisa suportar muitos tipos de produtos independentes.

---

## 🧠 Conclusão

O padrão Abstract Factory é útil quando há a necessidade de criar **famílias de objetos inter-relacionados**, como componentes gráficos de uma interface (botões, janelas, etc). Ele facilita a manutenção e expansão de sistemas complexos e promove uma arquitetura **flexível e desacoplada**. Apesar de exigir mais código e estrutura, sua aplicação é vantajosa em projetos com múltiplas variações de contexto (ex: temas, sistemas operacionais, ambientes).

---