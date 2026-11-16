@startuml
left to right direction

actor "Sensor" as Sensor
actor "Operador" as Operador

rectangle "Sistema mini-SCADA" {
  usecase "Recolher leitura\nde sensor" as UC01
  usecase "Validar leitura\nrecebida" as UC02
  usecase "Verificar limites\nda leitura" as UC03
  usecase "Gerar alarme por\nlimite ultrapassado" as UC04
  usecase "Consultar alarmes\nativos" as UC05
  usecase "Reconhecer alarme" as UC06
  usecase "Consultar histórico\nde leituras" as UC07
  usecase "Configurar limites\nde sensores" as UC08
}

Sensor --> UC01
UC01 --> UC02 : <<include>>
UC02 --> UC03 : <<include>>
UC03 --> UC04 : <<extend>>

Operador --> UC05
Operador --> UC06
Operador --> UC07
Operador --> UC08

UC06 --> UC05 : <<include>>

@enduml
