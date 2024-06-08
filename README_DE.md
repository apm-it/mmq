# mmq - manager mail queue von Postfix

## Beschreibung

mmq ist ein nützliches Tool, um die Verwendung von Postfix mailq zu vereinfachen. Mit mmq können E-Mails gefiltert und als Tabelle oder Liste ausgegeben werden. So kann sofort ein Überblick über die Mail-Warteschlange erhalten werden.

Es ist auch möglich, E-Mails aus der Warteschlange zu löschen oder einen individuellen Postfix-Befehl in Kombination mit der Queue-ID auszuführen.

**Weitere Informationen über den Erwerb der Software finden Sie auf <https://yellowcow.ch/produkt/mmq/>**

## Befehle

Aktionen für die ausgewählten Einträge:
Standardmäßig wird die Mail-Warteschlange als Tabelle ausgegeben.

**list**
Zeigt (über postqueue -p) eine detaillierte Auflistung der ausgewählten Einträge an.

**del**
Löscht (über postsuper -d) die ausgewählten Einträge.

## Optionen

**-t PATTERN, --timestamp PATTERN**
Filtert den Ankunftszeitstempel mit PATTERN (Platzhalter erlaubt).

**-s PATTERN, --source PATTERN**
Filtert die Quelle mit PATTERN (Platzhalter erlaubt).

**-d PATTERN, --destination PATTERN**
Filtert das Ziel mit PATTERN (Platzhalter erlaubt).

**-m PATTERN, --msg PATTERN**
Filtert die Fehlermeldung mit PATTERN (Platzhalter erlaubt).

**-l SIZE, --size-lower SIZE**
Filtert die Größe kleiner als GRÖßE Bytes.

**-u SIZE, --size-upper SIZE**
Filtert die Größe größer als GRÖßE Bytes.

**-a, --active**
Wählen Sie "aktive" Einträge in der Warteschlange aus

**-o, --hold**
Wählen Sie "gehaltene" Einträge in der Warteschlange aus

**--sort**
Sortieren Sie nach dem Zeitstempel in umgekehrter reienfolge

**-c COMMAND, --command COMMAND**
Verwenden Sie einen individuellen Befehl mit Query-ID als Eingabe z.B. mmq -c "postsuper -h"

**--version**
Zeigt die Versionsnummer des Programms an und beenden es

**-h, --help**
Zeigt die Hilfemeldung an und beenden das Programm

## Beispiele

**Beispiel 1:** Zeigen Sie alle Einträge in der Warteschlange, die an eine Empfängeradresse gesendet wurden, die "@example.com" entspricht im Format:

     > mmq -t "Jun 5 14:*"-d "*@example.com"
          
          Queue ID:      Arrival Time:   activ|hold  Size:     source:               destination:                  error-msg:
          B84979DF4      Jun 5 14:03:14      0|0     380       berd@test.de          bernd.albert@example.com      (connect to example.com[86.105.235.169]:25: Connection refused)
          637999E47      Jun 5 14:15:55      0|0     380       hallo@abc-xyz.de      kontakt@example.com           (connect to example.com[86.103.245.69]:25: Connection refused)
          F412BED6B      Jun 5 14:45:25      0|0     481       test@test.com         no-reply@example.com          (connect to example.com[3.18.255.247]:25: Connection timed out)
          0504AED77      Jun 5 14:50:55      0|0     481       test@test.com         order@example.com             (delivery temporarily suspended: connect to example.com[34.224.149.186]:25: Connection timed out)
          03C67ED74      Jun 5 14:53:26      0|0     481       test@test.com         bernd.albert@example.com      (delivery temporarily suspended: connect to example.com[34.224.143.186]:25: Connection timed out)
          00F1A9E9D      Jun 5 14:55:56      0|0     380       paul@firma.de         hans-gustaf@example.com       (connect to example.com[86.105.243.69]:25: Connection refused)

**Beispiel 2:** Entfernen Sie alle E-Mails in der Warteschlange, die aufgrund eines Verbindungsabbruchs nicht gesendet wurden:

     > mmq -m "*connection*timed*out" del

          deleting 00CF514616D3 [OK]
          deleting 12D911461924 [OK]
          deleting 269EF1461CA9 [OK]
          deleting 288DF1461CA0 [OK]
          deleting 3B3901460F62 [OK]
          deleting 3AE58147019F [OK]

**Beispiel 3:** Reihen Sie alle E-Mails neu ein, deren Quelladresse mit "test*" übereinstimmt:

     > mmq -s "test*" -c "postsuper -r"
          
          1C73FEF18: (postsuper: 1C73FEF18: requeued postsuper: Requeued: 1 message)
          F278EED67: (postsuper: F278EED67: requeued postsuper: Requeued: 1 message)
          F19CAED65: (postsuper: F19CAED65: requeued postsuper: Requeued: 1 message)
          F04A6ED62: (postsuper: F04A6ED62: requeued postsuper: Requeued: 1 message)
          F2DECED68: (postsuper: F2DECED68: requeued postsuper: Requeued: 1 message)
          F412BED6B: (postsuper: F412BED6B: requeued postsuper: Requeued: 1 message)
          F20D3ED66: (postsuper: F20D3ED66: requeued postsuper: Requeued: 1 message)
          F1297ED64: (postsuper: F1297ED64: requeued postsuper: Requeued: 1 message)

## Autor

APM-IT <mmq@apm-it.eu>

## Copyright and license

Copyright (c) 2024 APM-IT. All rights reserved.

This software is protected by copyright and may not be reproduced, distributed or modified without the express permission of the author.

To purchase a licence to use this software, please visit the website <https://yellowcow.ch/produkt/mmq/>.

Unauthorised use, duplication or distribution of this software is prohibited and may have legal consequences.
