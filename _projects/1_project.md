---
layout: page
title: Data Models
description: Designs dos dados do App
img: assets/img/data-modeling.jpeg
importance: 1
category: demo
mermaid: true
---


<pre class="mermaid">
erDiagram

     TENANT ||--o{ PRODUCT :has
     TENANT ||--o{ SHOP :has     
     TENANT ||--o{ SERVICE :has
     TENANT ||--o{ USER :has
     SHOP ||--o{ CAIXA :has
     CAIXA ||--o{ COMANDA :has
     COMANDA ||--o{ COMANDA_ITEM :has
     COMANDA ||--o{ COMANDA_PAYMENT :has
     SHOP ||--o{ INVOICE :has
     INVOICE ||--o{ INVOICE_ITEM :has
     SHOP ||--o{ BOOKING :has
     
     USER ||--o{ USER_SERVICES :has
    TENANT {
        integer id PK "Tenant Identifier"
        string subdomain "Subdomain"
        string logo "Path containing logo"
    }
    SUPERADMIN {
        integer id PK
        string email
        string password
    }
    SHOP {
        integer id PK
        integer tenantId FK
    }
    PRODUCT {
        integer id PK
        integer tenantId FK
        string name  "Product name"
    }
    SERVICE {
        integer id PK
        integer tenantId FK
        double price 
        integer duration "Service duration time"
    }
    USER {
        integer id PK
        integer tenantId FK
    }
    USER_SERVICES {
        integer id PK
        integer tenantId FK
        integer userId  FK "User ID"
        integer serviceId FK "Service ID"
        double price "Service value"
        integer duration "Service duration time"
    }
    INVOICE {
        integer id PK
        integer tenantId FK 
        shopId id FK "Shop ID"
    }
    INVOICE_ITEM {
        integer id PK
        integer tenantId FK
        integer invoiceId FK
    }
    BOOKING {
        integer id PK
        integer tenantId FK
        integer shopId FK
        integer userId FK
        integer serviceId FK
        date date
        time startTime
        time endTime
    }
    CAIXA {
        integer id PK
        integer tenantId FK
        integer shopId FK
        datetime open_at "Data de abertura"
        datetime closed_at "Data do fechamento"
    }
    COMANDA {
        integer id PK
        integer tenantId FK
        integer shopId FK
        integer caixaId FK
        double total "Valor total da comanda"
    }
    COMANDA_ITEM {
        integer id PK
        integer comandaId FK
        double price "Valor do item"
    }
    COMANDA_PAYMENT {
        integer id PK
        integer comandaId FK
        double value "Valor do pagamento"
    }
</pre>
