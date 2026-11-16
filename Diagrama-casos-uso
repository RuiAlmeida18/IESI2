```mermaid
classDiagram
    class Utilizador {
        -int id
        -String nome
        -String email
        -String passwordHash
        +autenticar() bool
    }

    class Operador {
        +consultarAlarmesAtivos() List~Alarme~
        +consultarHistoricoLeituras(int sensorId, DateTime inicio, DateTime fim) List~Leitura~
        +consultarEstadoSensores() List~Sensor~
    }

    class Administrador {
        +registarSensor(String nome, String tipo, String localizacao, String unidade) Sensor
        +configurarLimites(int sensorId, float min, float max) Limite
    }

    class Sensor {
        -int id
        -String nome
        -String tipo
        -String localizacao
        -String unidadeMedida
        -EstadoSensor estado
        -DateTime ultimaComunicacao
        +receberLeitura(float valor, String unidade, DateTime dataHora) Leitura
        +atualizarEstado(EstadoSensor novoEstado) void
    }

    class Limite {
        -int id
        -float valorMinimo
        -float valorMaximo
        -DateTime dataAtualizacao
        +validarLimites(float min, float max) bool
        +estaForaDosLimites(float valor) bool
    }

    class Leitura {
        -int id
        -float valor
        -String unidade
        -DateTime dataHora
        -bool valida
        -bool foraDosLimites
        +validarFormato() bool
        +classificar() void
    }

    class Alarme {
        -int id
        -String tipoProblema
        -float valorRegistado
        -float limiteUltrapassado
        -DateTime dataHoraCriacao
        -DateTime dataHoraAtualizacao
        -EstadoAlarme estado
        +atualizarOcorrencia(float novoValor) void
        +marcarComoReconhecido() void
    }

    class Reconhecimento {
        -int id
        -DateTime dataHora
        -String observacoes
        +registar(Alarme alarme, Operador operador) void
    }

    class EstadoSensor {
        <<enumeration>>
        ATIVO
        INATIVO
        SEM_SINAL
    }

    class EstadoAlarme {
        <<enumeration>>
        ATIVO
        RECONHECIDO
        RESOLVIDO
    }

    %% Herança
    Utilizador <|-- Operador
    Utilizador <|-- Administrador

    %% Relações principais
    Sensor "1" *-- "0..1" Limite : possui >
    Sensor "1" *-- "0..*" Leitura : regista >
    Sensor "1" -- "0..*" Alarme : gera >
    Leitura "1" -- "0..1" Alarme : origina >
    Alarme "1" -- "0..1" Reconhecimento : tem >
    Operador "1" -- "0..*" Reconhecimento : efetua >
    Administrador "1" -- "0..*" Sensor : gere >
    Administrador "1" -- "0..*" Limite : define >
}
```
