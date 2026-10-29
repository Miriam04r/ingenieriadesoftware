``` mermaid
flowchart TD
    cliente([Cliente])
    owner([Owner])
    emp([Employee])
    sis[Sistema EmpeñoControl]

    cliente <-->|solicita préstamos, deja garantías y paga en efectivo| emp
    cliente <-->|solicita préstamos, deja garantías y paga en efectivo| owner

    owner -->|supervisa, autoriza préstamos > $50k y consulta balances| sis
    emp -->|registra clientes, empeños y pagos manuales| sis

    style sis fill:#ff5d00,color:#fff
``` 
``` mermaidflowchart TD
    owner([Owner])
    emp([Employee])

    subgraph sistema[Sistema EmpeñoControl]
        web[App web<br/>React]
        api[API Monolito Modular<br/>Node.js]
        db[(Base de datos<br/>PostgreSQL)]
    end

    owner -->|usa| web
    emp -->|usa| web
    web -->|HTTPS/JSON| api
    api -->|lee y escribe| db

    style api fill:#ff5d00,color:#fff
```


```mermaid
flowchart TD
    web[App web]

    subgraph api[API del sistema]
        clientes[Clientes<br/>registro e informacion]
        empenos[Empeños<br/>prestamos y garantias]
        finanzas[Finanzas<br/>pagos y balances]
    end

    db[(Base de datos)]

    web --> clientes
    web --> empenos
    web --> finanzas

    empenos -->|asocia prestamo a persona especifica| clientes
    finanzas -->|revisa prestamos y avisa de pago| empenos

    clientes --> db
    empenos --> db
    finanzas --> db

    style finanzas fill:#ff5d00,color:#fff
```
