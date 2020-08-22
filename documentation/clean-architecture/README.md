# Clean Architecture

1. [ ] [Chapter 1 What Is Design and Architecture?](Chapter-1-What-Is-Design-and-Architecture.md)


22. [ ] [Chapter 22 The Clean Architecture](Chapter-22-The-Clean-Architecture.md)
23. [ ] [Chapter 23 Presenters and Humble Objects](Chapter-23-Presenters-and-Humble-Objects.md)
24. [ ] [Chapter 24 Partial Boundaries](Chapter-24-Partial-Boundaries.md)
25. [ ] [Chapter 25 Layers and Boundaries](Chapter-25-Layers-and-Boundaries.md)


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



 
 



