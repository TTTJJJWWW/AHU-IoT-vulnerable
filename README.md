# AHU-IoT-vulnerable

- [Tenda Vulnerabilities](#Tenda-Vulnerabilities)
- [TOTOLINK Vulnerabilities](#TOTOLINK-Vulnerabilities)

## Tenda Vulnerabilities
In 2024, our team discovered vulnerabilities in 6 different router products of Tenda, revealed 44 vulnerabilities and obtained 40 CVEs, which is listed below.

|     Tenda Routers      |   Vulnerable function    |              CVE               | Type of vulnerability |
| :--------------------: | :----------------------: | :----------------------------: | :-------------------: |
| FH1201 v1.2.0.14 (408) |    fromP2pListFilter     |         CVE-2024-42940         |    Buffer Overflow    |
|                        |      fromAdvSetWan       | CVE-2024-42941、CVE-2024-42943 |    Buffer Overflow    |
|                        |       frmL7ImForm        |         CVE-2024-42942         |    Buffer Overflow    |
|                        |       fromNatlimit       |         CVE-2024-42944         |    Buffer Overflow    |
|                        |      fromAddressNat      |         CVE-2024-42945         |    Buffer Overflow    |
|                        |      fromVirtualSer      |         CVE-2024-42946         |    Buffer Overflow    |
|                        |          telnet          |         CVE-2024-42947         |   Command Injection   |
|                        |   fromPptpUserSetting    |         CVE-2024-42948         |    Buffer Overflow    |
|                        |      fromqossetting      | CVE-2024-42949、CVE-2024-42952 |    Buffer Overflow    |
|                        |   fromSafeClientFilter   | CVE-2024-42950、CVE-2024-42955 |    Buffer Overflow    |
|                        |     fromWizardHandle     | CVE-2024-42951、CVE-2024-42953 |    Buffer Overflow    |
|                        | fromwebExcptypemanFilter |         CVE-2024-42954         |    Buffer Overflow    |
|  FH1206 v02.03.01.35   |    fromSafeUrlFilter     | CVE-2024-42968、CVE-2024-42969 |    Buffer Overflow    |
|                        |      fromSetlpBind       |         CVE-2024-42973         |    Buffer Overflow    |
|                        | fromwebExcptypemanFilter |         CVE-2024-42974         |    Buffer Overflow    |
|                        |   fromSafeClientFilter   |         CVE-2024-42976         |    Buffer Overflow    |
|                        |      fromqossetting      |         CVE-2024-42977         |    Buffer Overflow    |
|                        |          telnet          |         CVE-2024-42978         |   Command Injection   |
|                        |      frmL7ProtForm       |         CVE-2024-42979         |    Buffer Overflow    |
|                        |       frmL7ImForm        |         CVE-2024-42980         |    Buffer Overflow    |
|                        |   fromPptpUserSetting    |         CVE-2024-42981         |    Buffer Overflow    |
|                        |      fromVirtualSer      |         CVE-2024-42982         |    Buffer Overflow    |
|                        |      fromAdvSetWan       |         CVE-2024-42983         |    Buffer Overflow    |
|                        |    fromP2pListFilter     |         CVE-2024-42984         |    Buffer Overflow    |
|                        |       fromNatlimit       |         CVE-2024-42985         |    Buffer Overflow    |
|                        |      fromAdvSetWan       |         CVE-2024-42986         |    Buffer Overflow    |
|                        |     fromPptpUserAdd      |         CVE-2024-42987         |    Buffer Overflow    |
|   O1 1.0.0.7(10648)    |        formSetCfm        |         CVE-2024-8226          |    Buffer Overflow    |
|                        |      fromDhcpSetSer      |         CVE-2024-8227          |    Buffer Overflow    |
| O5V1.0 V1.0.0.8(5017)  |   fromSafeSetMacFilter   |         CVE-2024-8228          |    Buffer Overflow    |
|    O6 1.0.0.7(2054)    |   frommacFilterModify    |         CVE-2024-8229          |    Buffer Overflow    |
|                        |   fromSafeSetMacFilter   |         CVE-2024-8230          |    Buffer Overflow    |
|                        |      fromVirtualSet      |         CVE-2024-8231          |    Buffer Overflow    |
|     G3 15.11.0.20      |     formSetDebugCfg      |         CVE-2024-8224          |    Buffer Overflow    |
|                        |      formSetSysTime      |         CVE-2024-8225          |    Buffer Overflow    |

## TOTOLINK Vulnerabilities
In 2024, our team discovered vulnerabilities in 3 different router products of TOTOLINK, revealed 6 vulnerabilities and obtained 4 CVEs, which is listed below.

|       TOTOLINK Routers        |    Vulnerable  function    |      CVE       |  Type  of vulnerability  |
| :---------------------------: | :------------------------: | :------------: | :----------------------: |
| N350RT V9.3.5u.6139_B20201216 | /cgi-bin/ExportSettings.sh | CVE-2024-42966 | Incorrect access control |
|                               |      setParentalRules      | CVE-2024-7333  |     Buffer Overflow      |
| LR350 V9.3.5u.6369_B20220309  | /cgi-bin/ExportSettings.sh | CVE-2024-42967 | Incorrect access control |
| EX1200L 9.3.5u.6146_B20201023 |     UploadCustomModule     | CVE-2024-7334  |     Buffer Overflow      |

