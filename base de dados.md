```mermaid
erDiagram
    UTILIZADOR {
        int id PK
        varchar nome
        varchar email UK
        varchar password_hash
        enum perfil "OPERADOR, ADMINISTRADOR"
        datetime criado_em
    }

    SENSOR {
        int id PK
        int administrador_id FK
        varchar nome
        varchar tipo
        varchar localizacao
        varchar unidade_medida
        enum estado "ATIVO, INATIVO, SEM_SINAL"
        datetime ultima_comunicacao
    }

    LIMITE {
        int id PK
        int sensor_id FK, UK
        int administrador_id FK
        decimal valor_minimo
        decimal valor_maximo
        datetime data_atualizacao
    }

    LEITURA {
        int id PK
        int sensor_id FK
        decimal valor
        varchar unidade
        datetime data_hora
        boolean valida
        boolean fora_dos_limites
    }

    ALARME {
        int id PK
        int sensor_id FK
        int leitura_id FK
        varchar tipo_problema
        decimal valor_registado
        decimal limite_ultrapassado
        datetime data_hora_criacao
        datetime data_hora_atualizacao
        enum estado "ATIVO, RECONHECIDO, RESOLVIDO"
    }

    RECONHECIMENTO {
        int id PK
        int alarme_id FK, UK
        int operador_id FK
        datetime data_hora
        text observacoes
    }

    UTILIZADOR ||--o{ SENSOR : "regista (admin)"
    UTILIZADOR ||--o{ LIMITE : "configura (admin)"
    UTILIZADOR ||--o{ RECONHECIMENTO : "efetua (operador)"
    SENSOR ||--o| LIMITE : "possui"
    SENSOR ||--o{ LEITURA : "envia"
    SENSOR ||--o{ ALARME : "gera"
    LEITURA ||--o| ALARME : "origina"
    ALARME ||--o| RECONHECIMENTO : "tem"
```
