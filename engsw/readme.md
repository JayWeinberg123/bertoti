# Engenharia-de-software

We see three critical differences between programming and software engineering: time, scale, and the trade-offs at play. On a software engineering project, engineers need to be more concerned with the passage of time and the eventual need for change. In a software engineering organization, we need to be more concerned about scale and efficiency, both for the software we produce as well as for the organization that is producing it. Finally, as software engineers, we are asked to make more complex decisions with higher-stakes outcomes, often based on imprecise estimates of time and growth.

A engenharia de software carrega um peso muito maior, junto com diversos fatores que devem ser levados em conta. O tempo para realizar o projeto e a importância de um código funcional se provam essenciais, pois a escala de um erro que pode levar milhares de clientes/usuários a perderem acesso ao software é monumental comparado a um erro encontrado ao programar um projeto pessoal.

## Trade-offs na programação

### Consistência e acessibilidade
No caso de um grande fluxo de dados, o sacrifício da acessibilidade destes dados por uma consistência pode ocorrer. Isso resulta em um erro caso um sistema não consiga garantir que os dados que estão sendo acessados são os mais recentes, enquanto um foco em acessibilidade resultaria no oposto.

### Velocidade e legibilidade do código
No desenvolvimento de software, desenvolvedores podem escolher o caminho mais fácil e rápido ao criar seus códigos. Contudo, futuramente, quando se prova necessário realizar alterações ou manutenções no programa, até mesmo os desenvolvedores podem ter sérios problemas para entender as funcionalidades do código, especialmente sem a documentação adequada.

### Funções e linguagens específicas

É possível reparar que algumas linguagens possuem uma melhor compatibilidade com funções específicas, por exemplo:

    Python: desenvolvimento de fórmulas matemáticas.
    Engines de jogos: como GameMaker e Unity, no desenvolvimento de jogos.

Não que o desenvolvimento de jogos seja impossível no Python, mas a quantidade de funções e recursos da linguagem para fazer um jogo é muito menor do que o que o GameMaker oferece.


### Classe do Objeto "Carro"
```java
public class Carro {
    
    
    private String modelo;
    private String fabricante;
    private int anoFabricacao;
    
    public Carro(String modelo, String fabricante, int anoFabricacao) {
        this.modelo = modelo;
        this.fabricante = fabricante;
        this.anoFabricacao = anoFabricacao;
    }
    
    public String getModelo() {
        return modelo;
    }
    
    public String getFabricante() {
        return fabricante;
    }
    
    public int getAnoFabricacao() {
        return anoFabricacao;
    }

    public void setModelo(String modelo) {
        this.modelo = modelo;
    }
    
    public void setFabricante(String fabricante) {
        this.fabricante = fabricante;
    }

    public void setAnoFabricacao(int anoFabricacao) {
        this.anoFabricacao = anoFabricacao;
    }
}
```

### Classe da Concessionaria

```java
package saladeaula;
import java.util.LinkedList;
import java.util.List;

public class Concessionaria {

    private List<Carro> carrosDisponiveis = new LinkedList<Carro>();

    public void adicionarNovoCarro(Carro carro) {
        carrosDisponiveis.add(carro);
    }

    public List<Carro> buscarPorModelo(String modelo) {
        List<Carro> carrosEncontrados = new LinkedList<Carro>();
        for (Carro carro : carrosDisponiveis) {
            if (carro.getModelo().equals(modelo)) {
                carrosEncontrados.add(carro);
            }
        }
        return carrosEncontrados;
    }

    public List<Carro> getCarros() {
        return carrosDisponiveis;
    }
}
```

### Caso de teste usando o Junit

```java
package saladeaula;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.util.List;

public class ConcessionarioTest {

    @Test
    public void testAdicionarNovoCarro() {
        Concessionario concessionario = new Concessionario();
        Carro carro = new Carro("Civic", "Honda", 2020);
        
        concessionario.adicionarNovoCarro(carro);
        List<Carro> carros = concessionario.getCarros();
        
        assertEquals(1, carros.size());
        assertEquals("Civic", carros.get(0).getModelo());
        assertEquals("Honda", carros.get(0).getFabricante());
        assertEquals(2020, carros.get(0).getAnoFabricacao());
    }

    @Test
    public void testBuscarPorModelo_Encontrado() {
        Concessionario concessionario = new Concessionario();
        Carro carro1 = new Carro("Corolla", "Toyota", 2021);
        Carro carro2 = new Carro("Civic", "Honda", 2020);
        
        concessionario.adicionarNovoCarro(carro1);
        concessionario.adicionarNovoCarro(carro2);
        
        List<Carro> carrosEncontrados = concessionario.buscarPorModelo("Civic");
        
        assertEquals(1, carrosEncontrados.size());
        assertEquals("Civic", carrosEncontrados.get(0).getModelo());
    }

    @Test
    public void testBuscarPorModelo_NaoEncontrado() {
        Concessionario concessionario = new Concessionario();
        Carro carro1 = new Carro("Corolla", "Toyota", 2021);
        
        concessionario.adicionarNovoCarro(carro1);
        
        List<Carro> carrosEncontrados = concessionario.buscarPorModelo("Civic");
        
        assertTrue(carrosEncontrados.isEmpty());
    }

    @Test
    public void testGetCarros() {
        Concessionario concessionario = new Concessionario();
        Carro carro1 = new Carro("Corolla", "Toyota", 2021);
        Carro carro2 = new Carro("Civic", "Honda", 2020);
        
        concessionario.adicionarNovoCarro(carro1);
        concessionario.adicionarNovoCarro(carro2);
        
        List<Carro> carros = concessionario.getCarros();
        
        assertEquals(2, carros.size());
        assertEquals("Corolla", carros.get(0).getModelo());
        assertEquals("Civic", carros.get(1).getModelo());
    }
}
```

## UML das classes utilizadas no teste Junit

```bat
+------------------+                  +----------------------------+                  +-----------------------------+
|      Carro       |<----------------|       Concessionario       |<................ |      ConcessionarioTest     |
+------------------+                  +----------------------------+                  +-----------------------------+
| - modelo: String |                  | - carrosDisponiveis: List<Carro> |             | + testAdicionarNovoCarro(): void |
| - fabricante: String |              +----------------------------+                   | + testBuscarPorModelo_Encontrado(): void |
| - anoFabricacao: int |              | + adicionarNovoCarro(carro: Carro): void |     | + testBuscarPorModelo_NaoEncontrado(): void |
| + getModelo(): String |             | + buscarPorModelo(modelo: String): List<Carro> | | + testGetCarros(): void                  |
| + setModelo(modelo: String): void | | + getCarros(): List<Carro>                |    |                                             |
+------------------+                  +----------------------------+                  +-----------------------------+

```
