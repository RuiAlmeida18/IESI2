```mermaid
```plantuml
@startuml

enum EstadoSensor {
  ATIVO
  INATIVO
  SEM_SINAL
}

enum EstadoAlarme {
  ATIVO
  RECONHECIDO
  RESOLVIDO
}

enum EstadoLeitura {
  VALIDA
  INVALIDA
  SUSPEITA
}

class Utilizador {
  - id: int
  - nome: String
  - email: String
  - passwordHash: String
  + autenticar(): bool
}

class Administrador {
  + registarSensor(sensor: Sensor): void
  + configurarLimites(sensor: Sensor, limite: Limite): void
}

class Operador {
  + consultarAlarmesAtivos(): List
  + consultarHistorico(dataInicio: DateTime, dataFim: DateTime): List
  + consultarEstadoSensores(): List
  + reconhecerAlarme(alarme: Alarme): Reconhecimento
  + comunicarAnomalia(descricao: String): void
}

class Sensor {
  - id: int
  - nome: String
  - tipo: String
  - localizacao: String
  - unidadeMedida: String
  - estado: EstadoSensor
  - ultimaComunicacao: DateTime
  + receberLeitura(valor: float, dataHora: DateTime): Leitura
  + atualizarEstado(estado: EstadoSensor): void
}

class Leitura {
  - id: int
  - valor: float
  - unidade: String
  - dataHora: DateTime
  - estado: EstadoLeitura
  + validarFormato(): bool
  + classificar(): void
}

class Limite {
  - id: int
  - valorMinimo: float
  - valorMaximo: float
  - dataAtualizacao: DateTime
  + estaForaDosLimites(valor: float): bool
}

class Alarme {
  - id: int
  - tipoProblema: String
  - valorRegistado: float
  - limiteUltrapassado: String
  - dataHoraCriacao: DateTime
  - dataHoraAtualizacao: DateTime
  - estado: EstadoAlarme
  + atualizarEstado(estado: EstadoAlarme): void
  + marcarComoReconhecido(): void
}

class Reconhecimento {
  - id: int
  - dataHora: DateTime
  - observacao: String
  + registar(): void
}

Utilizador <|-- Administrador
Utilizador <|-- Operador

Administrador "1" -- "0..*" Sensor : gere
Sensor "1" -- "0..*" Leitura : regista
Sensor "1" -- "0..*" Limite : possui
Leitura "1" -- "0..1" Alarme : gera
Alarme "1" -- "0..1" Reconhecimento : tem
Operador "1" -- "0..*" Reconhecimento : efetua

Sensor --> EstadoSensor
Leitura --> EstadoLeitura
Alarme --> EstadoAlarme

@enduml

























































