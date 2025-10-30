# ER Dijagram Fakultet

```mermaid
classDiagram
    class Fakultet {
        -String id
        -String naziv
        +dodajKatedru()
        +ukloniKatedru()
    }
    
    class Katedra {
        -String id
        -String naziv
        +dodajPredavaca()
        +dodajKurs()
    }
    
    class Kurs {
        -String id
        -String naziv
        -String opis
    }
    
    class Predavac {
        -String id
        -String ime
        -String prezime
        -String zvanje
        +dodajKurs()
        +ukloniKurs()
    }
    
    class Student {
        -String brojIndeksa
        -String ime
        -String prezime
        +upisiKurs()
        +ispisiKurs()
    }
    
    %% Kompozicija - Fakultet se sastoji od Katedri
    Fakultet "1" *-- "1..*" Katedra : sadrži
    
    %% Agregacija - Katedra pripada Fakultetu
    Fakultet "1" o-- "1..*" Katedra : ima
    
    %% Asocijacije
    Katedra "1" --> "1..*" Kurs : drži kurseve
    Katedra "1" --> "1..*" Predavac : zaposleni
    Predavac "1" --> "0..*" Kurs : može predavati
    Student "1..*" --> "1..*" Fakultet : pohađa
    Student "1..*" --> "0..*" Kurs : sluša kurseve
    
    %% Specifične veze
    Katedra "1" --> "0..1" Predavac : šef katedre
    Predavac "1" --> "1" Katedra : pripada katedri
    
    %% Napomene za poslovna pravila
    note for Fakultet "Ne postoji fakultet bez katedri"
    note for Katedra "Mora držati bar jedan kurs"
    note for Predavac "Mora predavati bar jedan kurs"
    note for Student "Mora pohađati bar jedan fakultet\nMora imati bar jednog upisanog kursa"
