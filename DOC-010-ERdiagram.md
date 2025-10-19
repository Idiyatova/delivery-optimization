# Документ ER-диаграммы (ER Diagram)  
**Проект:** Оптимизация системы доставки  
**ID документа:** DOC-010-ERDiagram  
**Версия:** 1.0  
**Связанные документы:** [DOC-001-Preparation](DOC-001-Preparation.md), [DOC-007-EntityModel](DOC-007-EntityModel.md), [DOC-009-DataDict](DOC-009-DataDict.md)  

## 1. Введение  
Данный документ описывает ER-диаграмму базы данных системы доставки, основанную на сущностях и словаре данных. Диаграмма визуализирует связи между таблицами для обеспечения целостности данных.  

## 2. ER-диаграмма  


```mermaid
erDiagram
    ORD ||--o{ PAYOUT : "начисляет"
    ORD ||--o{ SUPP_PAY : "формирует"
    ORD }|--|| CUST : "для"
    ORD }|--|| PICK_POINT : "из"
    ORD }|--|| ADDR : "на"
    ORD }|--|| COUR_PROF : "исполняет"
    ORD }|--|| ORD_STATUS : "имеет"
    EMP ||--o{ COUR_PROF : "расширяет"
    SUPP ||--o{ PICK_POINT : "имеет"
    CUST ||--o{ ADDR : "имеет"
    ADDR ||--o{ PICK_POINT : "связан"

    ORD {
        INT ORD_ID PK
        INT CUST_ID FK
        INT PICK_ID FK
        INT ADDR_ID FK
        INT COUR_ID FK
        INT STAT_ID FK
        DateTime CR_DATE
        DateTime DELIV_TIME
        DateTime ACT_TIME
    }

    EMP {
        INT EMP_ID PK
        String F_NAME
        String PHONE
        String ROLE
        String LOGIN
        String PWD_HASH
        DateTime REG_DATE
    }

    COUR_PROF {
        INT EMP_ID PK
        Enum C_STATUS
        Decimal BALANCE
    }

    CUST {
        INT CUST_ID PK
        String F_NAME
        String PHONE
    }

    SUPP {
        INT SUPP_ID PK
        String S_NAME
        String PHONE
        Text BANK_DET
    }

    ADDR {
        INT CUST_ID FK
        String CITY
        String STREET
        String BUILDING
        String APARTMENT
    }

    PICK_POINT {
        INT PICK_ID PK
        INT SUPP_ID FK
        String ADDR
        String WORK_HRS
    }

    ORD_STATUS {
        INT STAT_ID PK
        String STAT_NAME
    }

    PAYOUT {
        INT PAY_ID PK
        INT ORD_ID FK
        INT COUR_ID FK
        Decimal AMOUNT
        Enum PAY_STAT
        DateTime ACC_DATE
    }

    SUPP_PAY {
        INT SP_ID PK
        INT ORD_ID FK
        INT SUPP_ID FK
        Decimal AMOUNT
        Enum PAY_STAT
        DateTime CR_DATE
    }