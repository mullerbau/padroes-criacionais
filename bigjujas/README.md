
# 🧱 Padrão de Projeto: Builder

## 🧩 Introdução

O padrão **Builder** é um padrão de projeto **criacional** que facilita a criação de objetos complexos de forma **passo a passo** e com **legibilidade**.

---

## ❓ Por que usar o Builder?

Sem o Builder, objetos com muitos parâmetros podem ficar difíceis de entender e manter:

```ts
// Sem Builder
const burger = new Burger(true, false, true, false, "grande", "brioche");
```

Com o Builder, o código fica mais claro:

```ts
// Com Builder
const burger = new BurgerBuilder()
  .addCheese()
  .addBacon()
  .setSize("grande")
  .setBread("brioche")
  .build();
```

---

## 🛠️ Estrutura do Builder

```ts
class BurgerBuilder {
  private cheese = false;
  private bacon = false;
  private size = "";
  private bread = "";

  addCheese() { this.cheese = true; return this; }
  addBacon() { this.bacon = true; return this; }
  setSize(size: string) { this.size = size; return this; }
  setBread(bread: string) { this.bread = bread; return this; }

  build() {
    return new Burger(this.cheese, this.bacon, this.size, this.bread);
  }
}
```

---

## 🎯 Quando usar o Builder?

- Quando o objeto tem **muitos parâmetros opcionais**
- Quando queremos construir objetos **em etapas**
- Quando precisamos de mais **clareza e controle** na construção

---

## ⚠️ Ponto fraco

- Adiciona **complexidade extra** em projetos simples
- Pode gerar **código repetitivo**
- Requer mais **classes/arquivos**

> Use o Builder **somente quando a complexidade justificar**.

---

## 🧠 Resumo

- É um padrão **criacional**
- Cria objetos complexos de forma **modular**
- Ajuda na **legibilidade** e **manutenção** do código
