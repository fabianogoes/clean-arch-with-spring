# Clean Architecture References

Referencias de palestras e artigos sobre Clean Architecture

**Modelos de Arquitetura dentro da Clean Architecture**   

- [Ports and Adapter / Hexagonal Architecture - 2005 (Dr. Alistair Cockburn)](#ports-and-adapter-ou-hexagonal-architecture)
- [Onion Architecture - 2008  (Jeffrey Palermo)](#onion-architecture)
- [Architecture - 2017 (Robert C. Martin aka Uncle Bob others SOLID, Clean Code)](#clean-architecture)


### Ports and Adapter ou Hexagonal Architecture   

![Ports and Adapter / Hexagonal Architecture](images/Ports-and-Adapters.png)

### Onion Architecture   

![Onion Architecture](images/Onion-Architecture.png)

### Clean Architecture   

![Clean Architecture](images/Clean-Architecture-UncleBob.png)


### Uncle Bob's Idea
--------------------

![Uncle Bob's Idea](images/UncleBob-CleanArch-Idea.png)

- **Interactor**: Boundary/UseCase
- **EntityGateway**: PortInterface
- **EntityGatewayImplementation**: AdapterImplementation
- **Boundary**: UseCaseInterface


### The Onion/Hexagonal Architecture
------------------------------------

![The Onion/Hexagonal Architecture](images/TheOnion-Architecture.png)

### The Onion Approach
----------------------

![The Onion Approach](images/TheOnion-Approach.png)

> Nessa abordagem o importate é que o UseCase fica isolado e protegendo as Entdades/Dominio
> Se a Persistencia vai ser no Banco X ou Y o UseCase e Domain não precisão saber, e se precisar trocar de Banco quem consome os dados não será afetado.
> Se será exposto por uma API Rest, um MVC, Jobs, Queue... O UseCase/Domain não sabe, e se vai usar Spring ou qualquer outro Framework não importa para o UseCase/Domain.
> Assim podemos testar e estressar os UseCases colocando um Mock/Fake como Persistencia, e quando chegar o momento escolhemos o tipo de persistencia isoladamente.
> O mesmo acontece com a escolha de Framework para REST, MVC, etc...

:warning: Essa abordagem pode ser considerada um **OverEngineering** e ficar dificil de manter, a menos que o time esteja seguro dos conceitos.

### Clean Arch Good Enough Approach
-----------------------------------

![Clean Arch Good Enough Approach](images/CleanArch-GoodEnoughApproach.png)

> By Mercado Livre
> O UseCase continua isolado e se tudo ao redor são apenas detalhes, podem ficar em uma camada externa apenas
> Assim teria um package de **Application** e outro de **Domain**

- **domain/dataprovider**: são as abstrações/interfaces (like Gateway Uncle Bob's Approach) que são implementadas na camada de **application/dataprovider**
- O mesmo acontece com os **application/entrypoint** que ficam isolados e suas implementações não comprometem os UseCases/Domain
- Podemos ter **SubDomains** dentro de **Domain** exemplo: Order, Invoice, Seller, Payment...
- O importante é que as Entidades de SubDomain não se conheçam, e toda comunicação deve ser por fora, usando uma **Facade** para fazer as Invokes dos **UseCases**, assim mantemos nossos **Boundaries Contexts**.

:information_source: As classes de UseCase não precisam estar sujas com o Framework, por exemplo o Spring, se usarmos a especificação `@Named` o Spring consegue identificar como um `Bean` durante o Scan e Fazer o `Inject`. 

:bell: Neste modelo do lado do **Domain** fazemos apenas **Testes Unitários** e do lado de **Application** fazemos apenas **Testes Integrados**


### Arquitetura Hexagonal: O que você precisa saber
---------------------------------------------------

![Onion Layers](images/Onion-Layers.png)

![Domain Layer Objects](images/Domain-Layer-Objects.png)

![Application Layer Objects](images/Application-Layer-Objects.png)

![Framework Layer Objects](images/Framework-Layer-Objects.png)

![Onion Relationship](images/Onion-Access-of-Layers.png)

![How To Do it](images/how-to-do-it.png)

![Dependency Injection](images/Dependency-Injection.png)

![Dependency Injection Validator](images/Dependency-Injection-Validator.png)

![Onion Adapters](images/Onion-Adapters.png)

![Onion Importants Points](images/Onion-Important-Points.png)

![Onion Tests](images/Onion-Tests.png)

- Domain: Testes Unitário são baratos
- Application: Testes de Integração com escopos claros
- Adapters: Testes com mundo externo por ser Mockado

![Onion Layes Flow Example](images/Onion-Layers-Flow-Example.png)


 
 



