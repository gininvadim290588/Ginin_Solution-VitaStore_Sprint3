@startuml

!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

Person(cashier,"Кассир")

System_Boundary(store,"Store Edge"){

Container(webpos,"Cloud POS","Web / Tablet","Тонкий клиент")

Container(edge,"Store Edge Agent","Hardware Abstraction Layer","Работа с оборудованием и офлайн")

Container(localcache,"Offline Cache","SQLite","Кэш чеков и каталога")

Container(kkt,"Fiscal Printer")

Container(bank,"Payment Terminal")

}

System_Boundary(cloud,"Cloud Backend"){

Container(apigw,"API Gateway")

Container(possvc,"POS Service")

Container(product,"Product Catalog")

Container(pricing,"Pricing Service")

Container(loyalty,"Loyalty Service")

Container(payment,"Payment Gateway")

Container(sync,"Synchronization Service")

ContainerDb(db,"Cloud Database")

Container(sap,"SAP ERP")

}

Rel(cashier,webpos,"Работает")

Rel(webpos,apigw,"HTTPS")

Rel(apigw,possvc,"REST")

Rel(possvc,product,"API")

Rel(possvc,pricing,"API")

Rel(possvc,loyalty,"API")

Rel(possvc,payment,"API")

Rel(payment,edge,"Единый протокол")

Rel(edge,bank,"Драйвер устройства")

Rel(edge,kkt,"Драйвер устройства")

Rel(edge,localcache,"Offline Storage")

Rel(webpos,edge,"Local API")

Rel(sync,localcache,"Синхронизация")

Rel(sync,db,"Upload")

Rel(product,sap,"Интеграция")

@enduml
