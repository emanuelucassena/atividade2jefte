# 📌 Composição e Injeção de Dependência em POO

## 🏗️ Composição

Composição é um princípio da **Programação Orientada a Objetos (POO)** no qual uma classe é formada por outras classes. Em vez de herdar comportamento, ela **possui instâncias de outras classes** como seus atributos.

### 🎯 **Benefícios da Composição**
- ✅ **Baixo acoplamento**: `Animal` não precisa saber como `Andar`, `Falar`, `Respirar`, `Nadar` ou `Voar` funcionam. Cada classe usa apenas os comportamentos necessários.
- 🔄 **Flexibilidade**: Podemos adicionar novos comportamentos sem modificar a hierarquia de classes.
- 🔁 **Reutilização de código**: Classes como `Respirar`, `Andar` e `Falar` podem ser utilizadas por diferentes animais sem duplicação de código.

---

## 🛠️ Injeção de Dependência (IoC)

### 🔹 **O que é?**
Injeção de dependência é uma das formas de implementar **Inversão de Controle (IoC)**, garantindo **baixo acoplamento** entre as classes.

### 🏷️ **Tipos de Injeção de Dependência**
1. **Injeção por Construtor** (*Constructor Injection*).
2. **Injeção por Getters e Setters** (*Setter Injection*).
3. **Injeção por Interface** (*Interface Injection*).

---

## ❌ Código sem Injeção de Dependência Adequada

No exemplo abaixo, a classe `Cachorro` cria suas dependências dentro do próprio construtor, o que não é ideal:

```java
import comportamentos.Andar;
import comportamentos.Falar;
import comportamentos.Respirar;

public class Cachorro extends Animal {
    private Falar falar;
    private Respirar respirar;
    private Andar andar;

    public Cachorro(String nome, int idade, String categoria) {
        super(nome, idade, categoria);
        
        falar = new Falar();  // 👎 Criando dependências internamente
        respirar = new Respirar();
        andar = new Andar();
    }

    public void falar() {
        this.falar.falar("au au");
    }

    public void respirar() {
        this.respirar.respirar(10);
    }

    public void andar() {
        this.andar.andar(10);
    }
}
```

🔴 **Problema**: A classe `Cachorro` **cria** suas próprias instâncias, dificultando a reutilização e testes unitários.

---

## ✅ Código Melhorado com Injeção de Dependência

A melhor abordagem é passar as dependências pelo **construtor**, tornando a classe mais flexível e reutilizável:

```java
public class Cachorro extends Animal {
    private Falar falar;
    private Respirar respirar;
    private Andar andar;

    // ✅ Injeção de dependências via construtor
    public Cachorro(String nome, int idade, String categoria, Falar falar, Respirar respirar, Andar andar) {
        super(nome, idade, categoria);
        this.falar = falar;
        this.respirar = respirar;
        this.andar = andar;
    }

    public void falar() {
        this.falar.falar("au au");
    }

    public void respirar() {
        this.respirar.respirar(10);
    }

    public void andar() {
        this.andar.andar(10);
    }
}
```

💡 **Vantagens da Injeção de Dependência**
- 🔹 **Mais testável**: Podemos substituir dependências por **mocks** em testes.
- 🔹 **Mais modular**: `Cachorro` apenas **recebe** as dependências, sem precisar criá-las.
- 🔹 **Mais reutilizável**: Podemos passar diferentes implementações de `Falar`, `Andar` e `Respirar` conforme necessário.

---

## 🎯 **Conclusão**
📌 **Composição** nos permite estruturar classes a partir de outras classes, garantindo código mais modular e reutilizável.
📌 **Injeção de Dependência** reduz o acoplamento entre classes, tornando o código mais flexível e testável.

🛠️ Aplicar esses conceitos melhora **organização**, **escalabilidade** e **manutenção** dos sistemas! 🚀

