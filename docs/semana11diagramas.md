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
