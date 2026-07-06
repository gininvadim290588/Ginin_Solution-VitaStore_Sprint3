@startuml

!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

Person(cashier,"Кассир")

System_Boundary(store,"Store Edge"){

Container(pos,"POS App","Windows Desktop","Толстый клиент кассы")

Container(localdb,"Local DB","MS SQL / PostgreSQL","Локальная база магазина")

Container(kkt,"Fiscal Printer")

Container(bank,"Payment Terminal")

}

System_Boundary(hq,"HQ"){

Container(sap,"SAP ERP")

}

Rel(cashier,pos,"Работает")

Rel(pos,localdb,"Чтение/запись")

Rel(pos,kkt,"COM Driver")

Rel(pos,bank,"USB Driver")

Rel(localdb,sap,"Ночной XML/FTP","Batch")

@enduml
