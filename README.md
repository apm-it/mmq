# mmq - manager mail queue for Postfix 

## Description

mmq is a useful tool to simplify the use of Postfix mailq.
With mmq, e-mails can be filtered (with wildcards) and output as a table or list.
So that an overview of the mailq can be obtained immediately.

It is also possible to delete emails from the queue or execute an individual Postfix command in combination with the queue ID.

**For more information on how to purchase the software visit <https://yellowcow.ch/produkt/mmq/>**

## Commands

Action to be performed for the selected entries:
By default, the mailq is output as a table.

**list**
Show (via ***postqueue -p***)a detailed listing of the selected entries.

**del** Delete (via ***postsuper -d***) the selected entries.

## Options

**-t PATTERN, --timestamp PATTERN**
Filters the Arrival Timestamp with PATTERN (wildcards allowed).
 
**-s PATTERN, --source PATTERN**
Filters the source with PATTERN (wildcards allowed)
  
**-d PATTERN, --destination PATTERN**
Filters the destination with PATTERN (wildcards allowed)

**-m PATTERN, --msg PATTERN**
Filters the error message with PATTERN (wildcards allowed)
  
**-l SIZE, --size-lower SIZE**
Filters the size lower than SIZE bytes
  
**-u SIZE, --size-upper SIZE**
Filters the size upper than SIZE bytes
  
**-a, --active**          
Select "active" entries in queue (default: no)
  
**-o, --hold**           
Select "on hold" entries in queue (default: no)
  
**--sort**
Sort timestamp reverse
  
**-c COMMAND, --command COMMAND**
Use an individual command with Query ID as input e.g. mmq -c "postsuper -h"

**--version**
Show program's version number and exit

**-h, --help**
Show help message and exit

## Examples

**Example 1:** display all the entries in queue sent to an recipient address match "*@example.com*"

    > mmq -t "Jun 5 14:*"-d "*@example.com"
     
     Queue ID:      Arrival Time:   activ|hold  Size:     source:               destination:                  error-msg:
     B84979DF4      Jun 5 14:03:14      0|0     380       berd@test.de          bernd.albert@example.com      (connect to example.com[86.105.235.169]:25: Connection refused)
     637999E47      Jun 5 14:15:55      0|0     380       hallo@abc-xyz.de      kontakt@example.com           (connect to example.com[86.103.245.69]:25: Connection refused)
     F412BED6B      Jun 5 14:45:25      0|0     481       test@test.com         no-reply@example.com          (connect to example.com[3.18.255.247]:25: Connection timed out)
     0504AED77      Jun 5 14:50:55      0|0     481       test@test.com         order@example.com             (delivery temporarily suspended: connect to example.com[34.224.149.186]:25: Connection timed out)
     03C67ED74      Jun 5 14:53:26      0|0     481       test@test.com         bernd.albert@example.com      (delivery temporarily suspended: connect to example.com[34.224.143.186]:25: Connection timed out)
     00F1A9E9D      Jun 5 14:55:56      0|0     380       paul@firma.de         hans-gustaf@example.com       (connect to example.com[86.105.243.69]:25: Connection refused)

**Example 2:** remove all mails in queue not sent because of a connection timeout:

    > mmq -m "*connection*timed*out" del

     deleting 00CF514616D3 [OK]
     deleting 12D911461924 [OK]
     deleting 269EF1461CA9 [OK]
     deleting 288DF1461CA0 [OK]
     deleting 3B3901460F62 [OK]
     deleting 3AE58147019F [OK]

**Example 3:** Requeue all mails source address match "test*"

    > mmq -s "test*" -c "postsuper -r"
     
     1C73FEF18: (postsuper: 1C73FEF18: requeued postsuper: Requeued: 1 message)
     F278EED67: (postsuper: F278EED67: requeued postsuper: Requeued: 1 message)
     F19CAED65: (postsuper: F19CAED65: requeued postsuper: Requeued: 1 message)
     F04A6ED62: (postsuper: F04A6ED62: requeued postsuper: Requeued: 1 message)
     F2DECED68: (postsuper: F2DECED68: requeued postsuper: Requeued: 1 message)
     F412BED6B: (postsuper: F412BED6B: requeued postsuper: Requeued: 1 message)
     F20D3ED66: (postsuper: F20D3ED66: requeued postsuper: Requeued: 1 message)
     F1297ED64: (postsuper: F1297ED64: requeued postsuper: Requeued: 1 message)

## Author

APM-IT <mmq@apm-it.eu>

## Copyright and license

Copyright (c) 2024 APM-IT. All rights reserved.

This software is protected by copyright and may not be reproduced, distributed or modified without the express permission of the author.

To purchase a licence to use this software, please visit the website <https://yellowcow.ch/produkt/mmq/>.

Unauthorised use, duplication or distribution of this software is prohibited and may have legal consequences.
