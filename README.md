# Scrape Abgeordnetenwatch.de
Die einzelnen Scripte laden verschiedene Informationen über die in Deutschland gewählten Politiker:innen auf Bundes-, Landes- und Europaebene herunter. Die Scripte wurden am 14.08.2024 das letzte Mal getestet. Hinweise, wenn sich der Seitenaufbau von Abgeordnetenwatch.de verändert, Hinweise auf Bugs, Fragen oder Verbesserungsvorschläge sind gerne willkommen! :)

## Welche Informationen werden genau gesammelt?
Es werden der volle Name, Vor- und Nachname, Zahl der gestellten und beantworteten Fragen, die Partei, das gewählte Parlament, das Geburtsjahr (sofern Informationen vorhanden sind), das Geschlecht (sofern Informationen vohanden sind), der Wohnort (sofern Informationen vorhanden sind) und Informationen zu den einzelnen Fragen gesammelt. Den einzelnen Politiker:innen wird eine ID zugewiesen, welche von Abgeordnetenwatch.de übernommen wurde. Zu den Informationen die für die einzelnen Fragen gesammelt werden, zählen das Datum der Fragestellung, der Frageteaser, der Fragetext (sofern vorhanden), der Antworttext (sofern vorhanden), das Fragethema, das Parlament in dem die Frage gestellt wurde sowie eine individuelle Frage-ID. 

## Wie sind die gesammelten Informationen aufgebaut?
In den ersten beiden Scripten (Scrape_Abgeordnetenwatch_1.qmd, Scrape_Abgeordnetenwatch_2.qmd) werden die Informationen tabellarisch in gespeichert. Jede:r Politiker:in stellt eine eigene Reihe dar und in den Spalten werden die einzelnen Informationen gespeichert. In Script 3 und 4 (Scrape_Abgeordnetenwatch_3.qmd, Scrape_Abgeordnetenwatch_4.qmd) werden die die einzelnen Fragen den entsprechenden Politiker:innen hinzugefügt. Da mehrere Fragen an eine:n Politiker:in gestellt werden kann, wird der tabellarische Aufbau in das JSON-Format überführt, um Verschachtelungen zu erlauben. 
Im Folgenden wird beispielhaft dargestellt, wie der Aufbau der Datei am Ende des vierten Scripts aussehen sollte:
```
[
  {
    Name: str,
    Party: str,
    Parliament: str,
    Q_A_Link: str,
    ID: int,
    Q_asked: int,
    Q_answered: int,
    No_of_pages: int,
    QA_Information: [
      {
        Date_of_Question: date,
        Question: str,
        Teaser_of_Question: str,
        Answer: str,
        Question_ID: str,
        Topic: str,
        Parliament: str
      },
      ...
      
    ],
    First_Name: str,
    Last_Name: str,
    Gender: str,
    Year_of_birth: int,
    Residence: str
  },
  ...

]
```
## Informationen und Hinweise zu den einzelnen Scripten
Im Folgenden wird genauer auf die einzelnen Scripte eingegangen, was sie tun, warum sie was tun und welche Limitationen es gibt.

### Scrape_Abgeordnetenwatch_1.qmd
