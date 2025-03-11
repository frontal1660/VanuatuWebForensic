# :100: VanuatuWebForensic :100:  
<br/>

![image](https://github.com/user-attachments/assets/09b98e74-d7cb-487b-b7e8-fddd0fd731d0)  
<br/>

## :alien: Action plan
Action list :  
- [ ] [Preamble](#link-preamble)
- [ ] [Get the datetime crushadmin password was changed](#link-adm-changed)
- [ ] [Identify major actions made by 147.45.112.220 under HTTP interface](#link-actions1)
- [ ] [Identify major actions made by 91.191.209.10 under HTTP interface](#link-actions2)
- [ ] [List all actions](#link-actions3)
- [ ] [Get banned IP](#link-banned)
- [ ] [Get intel from Maxmind](#link-geoip)
- [ ] [Get unsuccessfull HTTP login attemps](#link-fail-http)
- [ ] [Get unsuccessfull SFTP login attemps](#link-fail-sftp)
- [ ] [Get unsuccessfull FTP login attemps](#link-fail-ftp)
- [ ] [Get successfull HTTP login attemps](#link-success-http)
  
  <br/>

##  :alien: <a name="link-preamble">Preamble</a>
  
All CrushFTP log files, from 02/09/2025 to 03/07/2025, has been stored to one unique log file.  
This makes analyzes easier.  
<br/>
  
Verdict

- [X] Preamble :sunglasses:
  
  <br/>

##  :alien: <a name="link-adm-changed">Get the datetime when crushadmin password was changed</a>
  
We can extract the datetime when crushadmin password was changed:
  
```
cat crushftp_all.log | grep 'password changed' | awk -F'|' '{print $2}'
```
  
This the result:
    
| # | Date       | Time     | User       |
|---|------------|----------|------------|
| 1 | 03/07/2025 | 16:03:36 | crushadmin |
| 2 | 03/07/2025 | 16:05:43 | crushadmin |
| 3 | 03/07/2025 | 16:07:02 | crushadmin |
| 4 | 03/07/2025 | 16:37:35 | crushadmin |
  
Verdict

- [X] Get the datetime crushadmin when password was changed :sunglasses:
  
  <br/>

##  :alien: <a name="link-actions1">Identify major actions made by 147.45.112.220 under HTTP interface</a>
  
> [!CAUTION]
> These following actions are done in 1.629s!  
> This certainly means that a script/metasploit is behind this behaviour.
<br/>
  
1. Action #1
  
The hacker successfully authenticates with crushadmin user, with the correct password:  
He now has an admin cookie set.
  
```
POST|03/07/2025 16:03:36.641|[147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.643|[147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:36.644|[147.45.112.220] READ: *command:login*
POST|03/07/2025 16:03:36.646|[147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.648|[147.45.112.220] READ: *password:************
POST|03/07/2025 16:03:36.649|[147.45.112.220] READ: *encoded:true*
POST|03/07/2025 16:03:36.650|[147.45.112.220] READ: *language:en*
POST|03/07/2025 16:03:36.652|[147.45.112.220] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:03:36.684|[crushadmin:147.45.112.220] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:03:36.687|SERVER_LOGIN:SUCCESS:541455:MainUsers:crushadmin:HTTP:147.45.112.220:
POST|03/07/2025 16:03:36.688|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:36.689|[crushadmin:147.45.112.220] WROTE: *Set-Cookie: currentAuth=zIpc; path=/
```
<br/>
  
2. Action #2
  
The hacker prompts the list of registered users:
    
```
POST|03/07/2025 16:03:36.720|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.721|[crushadmin:147.45.112.220] READ: *command:getUser*
POST|03/07/2025 16:03:36.723|[crushadmin:147.45.112.220] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:03:36.724|[crushadmin:147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.725|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:36.737|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:03:36.770|[lookup:9090] Accepting connection from: 147.45.112.220:33328
```
<br/>
  
3. Action #3
  
The hacker changes the _crushadmin_ password:
  
```
POST|03/07/2025 16:03:36.772|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.773|[crushadmin:147.45.112.220] READ: *command:setUserItem*
POST|03/07/2025 16:03:36.775|[crushadmin:147.45.112.220] READ: *data_action:replace*
POST|03/07/2025 16:03:36.776|[crushadmin:147.45.112.220] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:03:36.778|[crushadmin:147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.779|[crushadmin:147.45.112.220] READ: *user:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.781|[crushadmin:147.45.112.220] READ: *xmlItem:user*
POST|03/07/2025 16:03:36.783|[crushadmin:147.45.112.220] READ: *vfs_items:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.784|[crushadmin:147.45.112.220] READ: *permissions:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.786|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:36.883|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:03:37.261|[lookup:9090] Accepting connection from: 147.45.112.220:33330
```
<br/>
  
4. Action #4
  
The hacker uploads the file _crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt_ in FTP_ROOT:
  
```
POST|03/07/2025 16:03:37.263|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.265|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.267|[crushadmin:147.45.112.220] READ: *command:openFile*
POST|03/07/2025 16:03:37.268|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:37.270|[crushadmin:147.45.112.220] READ: *upload_path:/crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt*
POST|03/07/2025 16:03:37.271|[crushadmin:147.45.112.220] READ: *upload_size:1003702*
POST|03/07/2025 16:03:37.273|[crushadmin:147.45.112.220] READ: *upload_id:2148654e*
POST|03/07/2025 16:03:37.275|[crushadmin:147.45.112.220] READ: *start_resume_loc:0*
POST|03/07/2025 16:03:37.276|[crushadmin:147.45.112.220] READ: *random:0.345679978990884*
STOR|03/07/2025 16:03:37.287|[crushadmin:147.45.112.220] WROTE: *150 Opening BINARY data connection.  Ready to write file /1871264c-ce01-4270-aef1-6a2f38515ad7.txt. S T O R*
POST|03/07/2025 16:03:37.586|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:37.619|[crushadmin:147.45.112.220] READ: *POST /U/2148654e~1~1003702 HTTP/1.1*
POST|03/07/2025 16:03:37.621|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.727|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
5. Action #5
  
The hacker can see on the screen that the file _crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt_ has been uploaded with success:
  
```
POST|03/07/2025 16:03:37.763|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.764|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.766|[crushadmin:147.45.112.220] READ: *command:closeFile*
POST|03/07/2025 16:03:37.768|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:37.769|[crushadmin:147.45.112.220] READ: *upload_id:2148654e*
POST|03/07/2025 16:03:37.771|[crushadmin:147.45.112.220] READ: *total_chunks:1*
POST|03/07/2025 16:03:37.773|[crushadmin:147.45.112.220] READ: *total_bytes:1003702*
POST|03/07/2025 16:03:37.774|[crushadmin:147.45.112.220] READ: *filePath:/crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt*
POST|03/07/2025 16:03:37.776|[crushadmin:147.45.112.220] READ: *lastModified:1713988562086*
POST|03/07/2025 16:03:37.778|[crushadmin:147.45.112.220] READ: *random:0.10444100243921683*
STOR|03/07/2025 16:03:37.817|[crushadmin:147.45.112.220] WROTE: *226-Upload File Size:1003702 bytes @ 980K/sec. MD5=1945485edcdea03caad347041b7b8a37*
STOR|03/07/2025 16:03:37.819|[crushadmin:147.45.112.220] WROTE: *226 Transfer complete.  MD5=1945485edcdea03caad347041b7b8a37 ("/1871264c-ce01-4270-aef1-6a2f38515ad7.txt" 1003702) STOR*
POST|03/07/2025 16:03:37.838|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
6. Action #6
  
The hacker checks/modifies a setting of a plugin (_server_settings/plugins/5/1_).  
  
It is pretty obvious that :  
1. the file _crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt_ is actually a malicious CrushFTP plugin:
2. the hacker has renamed the plugin with a specific name
  
```
POST|03/07/2025 16:03:37.870|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.872|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.874|[crushadmin:147.45.112.220] READ: *command:getServerItem,c2f:zIpc,key:server_settings*
POST|03/07/2025 16:03:37.941|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.943|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.945|[crushadmin:147.45.112.220] READ: *command:setServerItem*
POST|03/07/2025 16:03:37.947|[crushadmin:147.45.112.220] READ: *key:server_settings/plugins/5/1*
POST|03/07/2025 16:03:37.949|[crushadmin:147.45.112.220] READ: *data_type:vector*
POST|03/07/2025 16:03:37.951|[crushadmin:147.45.112.220] READ: *data_action:change*
POST|03/07/2025 16:03:37.953|[crushadmin:147.45.112.220] READ: *data:<plugins_subitem+type="properties">
POST|03/07/2025 16:03:37.954|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:38.171|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
7. Action #7
  
The hackers calls its plugin now known by the name _CrushSQL_.  
  
The name of the plugin might be a decoy to "hide" this malicious plugin.
  
The plugin is actually a JAR archive.
  
```
POST|03/07/2025 16:03:38.244|[crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:38.246|[crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:38.248|[crushadmin:147.45.112.220] READ: *command:pluginMethodCall*
POST|03/07/2025 16:03:38.250|[crushadmin:147.45.112.220] READ: *method:testSettings*
POST|03/07/2025 16:03:38.252|[crushadmin:147.45.112.220] READ: *pluginName:CrushSQL*
POST|03/07/2025 16:03:38.254|[crushadmin:147.45.112.220] READ: *pluginSubItem:*
POST|03/07/2025 16:03:38.256|[crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:38.267|[crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:38.270|[crushadmin:147.45.112.220] WROTE: *<commandResult><response>java.lang.UnsupportedClassVersionError: com/mysql/jdbc/Driver has been compiled by a more recent version of the Java Runtime (class file version 67.0), this version of the Java Runtime only recognizes class file versions up to 61.0</response></commandResult>*
```
<br/>
  
Verdict

- [X] Identify major actions made by 147.45.112.220  under HTTP interface :sunglasses:
  
  <br/>

##  :alien: <a name="link-actions2">Identify major actions made by 91.191.209.10 under HTTP interface</a>
  
> [!CAUTION]
> Behind this new IP there is the same hacker! 
<br/>
  
1. Action #1
  
The hacker successfully authenticates with crushadmin user, with the correct password:  
He now has an admin cookie set.
  
```
ACCEPT|03/07/2025 16:05:43.273|[HTTP:541458_60784:lookup:9090] Accepting connection from: 91.191.209.10:60784
POST|03/07/2025 16:05:43.277|[HTTP:541458_60784_OjC::91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:43.278|[HTTP:541458_60784_OjC::91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:43.279|[HTTP:541458_60784_OjC::91.191.209.10] READ: *command:login*
POST|03/07/2025 16:05:43.281|[HTTP:541458_60784_OjC::91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:05:43.282|[HTTP:541458_60784_OjC::91.191.209.10] READ: *password:************
POST|03/07/2025 16:05:43.284|[HTTP:541458_60784_OjC::91.191.209.10] READ: *encoded:true*
POST|03/07/2025 16:05:43.285|[HTTP:541458_60784_OjC::91.191.209.10] READ: *language:en*
POST|03/07/2025 16:05:43.286|[HTTP:541458_60784_OjC::91.191.209.10] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:05:43.303|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:05:43.306|SERVER_LOGIN:SUCCESS:541458:MainUsers:crushadmin:HTTP:91.191.209.10:
POST|03/07/2025 16:05:43.306|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:05:43.307|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *Set-Cookie: currentAuth=QhPs; path=
```
<br/>
  
2. Action #2
  
The hacker edits user _crushadmin_ :
    
```
POST|03/07/2025 16:05:43.383|[HTTP:541458_60784_wsV:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:43.384|[HTTP:541458_60784_wsV:crushadmin:91.191.209.10] READ: *command:getUser*
POST|03/07/2025 16:05:43.385|[HTTP:541458_60784_wsV:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:05:43.387|[HTTP:541458_60784_wsV:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:05:43.388|[HTTP:541458_60784_wsV:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:43.400|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:05:43.477|[HTTP:541458_60788:lookup:9090] Accepting connection from: 91.191.209.10:60788
```
<br/>
  
3. Action #3
  
The hacker changes the _crushadmin_ password:
  
```
POST|03/07/2025 16:05:43.479|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:43.480|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *command:setUserItem*
POST|03/07/2025 16:05:43.482|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *data_action:replace*
POST|03/07/2025 16:05:43.483|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:05:43.485|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:05:43.486|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *user:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:05:43.488|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *xmlItem:user*
POST|03/07/2025 16:05:43.489|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *vfs_items:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:05:43.491|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *permissions:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:05:43.493|[HTTP:541458_60784_5bt:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:43.590|[HTTP:541458_60788:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:05:44.265|[HTTP:541458_60804:lookup:9090] Accepting connection from: 91.191.209.10:60804
```
<br/>
  
4. Action #4
  
The hacker uploads the file _crushtmplog/1340597d-f19d-4d5d-8616-3c6293d21895.txt_:
  
```
POST|03/07/2025 16:05:44.267|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:44.269|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:44.270|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *command:openFile*
POST|03/07/2025 16:05:44.272|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:44.274|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *upload_path:/crushtmplog/1340597d-f19d-4d5d-8616-3c6293d21895.txt*
POST|03/07/2025 16:05:44.275|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *upload_size:1005600*
POST|03/07/2025 16:05:44.277|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *upload_id:2d23cdac*
POST|03/07/2025 16:05:44.279|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *start_resume_loc:0*
POST|03/07/2025 16:05:44.280|[HTTP:541458_60784_3N4:crushadmin:91.191.209.10] READ: *random:0.345679978990884*
STOR|03/07/2025 16:05:44.291|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *150 Opening BINARY data connection.  Ready to write file /1340597d-f19d-4d5d-8616-3c6293d21895.txt. S T O R*
POST|03/07/2025 16:05:44.591|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
5. Action #5
  
The hacker probably tries to comminicate with his plugin via the POST query _U/2d23cdac~1~1005600_:  
  
```
POST|03/07/2025 16:05:44.670|[HTTP:541458_60784_QG6:crushadmin:91.191.209.10] READ: *POST /U/2d23cdac~1~1005600 HTTP/1.1*
POST|03/07/2025 16:05:44.672|[HTTP:541458_60784_QG6:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:45.005|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
6. Action #6
  
The hacker can see on the screen that the file _/crushtmplog/1340597d-f19d-4d5d-8616-3c6293d21895.txt_ has been uploaded with success:
  
```
POST|03/07/2025 16:05:45.125|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:45.127|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:45.129|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *command:closeFile*
POST|03/07/2025 16:05:45.131|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:45.133|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *upload_id:2d23cdac*
POST|03/07/2025 16:05:45.134|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *total_chunks:1*
POST|03/07/2025 16:05:45.136|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *total_bytes:1005600*
POST|03/07/2025 16:05:45.138|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *filePath:/crushtmplog/1340597d-f19d-4d5d-8616-3c6293d21895.txt*
POST|03/07/2025 16:05:45.140|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *lastModified:1713988562086*
POST|03/07/2025 16:05:45.141|[HTTP:541458_60784_fdt:crushadmin:91.191.209.10] READ: *random:0.10444100243921683*
STOR|03/07/2025 16:05:45.180|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *226-Upload File Size:1005600 bytes @ 982K/sec. MD5=58185173bfb7aca32183ca25be614bbb*
STOR|03/07/2025 16:05:45.183|[HTTP:541458_60784:crushadmin:91.191.209.10] WROTE: *226 Transfer complete.  MD5=58185173bfb7aca32183ca25be614bbb ("/1340597d-f19d-4d5d-8616-3c6293d21895.txt" 1005600) STOR*
POST|03/07/2025 16:05:45.190|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
7. Action #7
  
The hacker checks/modifies a setting of a plugin (server_settings/plugins/5/1).

It is pretty obvious that :
1. the file _/crushtmplog/1340597d-f19d-4d5d-8616-3c6293d21895.txt_ is actually a malicious CrushFTP plugin:
2. the hacker has renamed the plugin with a specific name
  
```
POST|03/07/2025 16:05:45.309|[HTTP:541458_60784_dXY:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:45.311|[HTTP:541458_60784_dXY:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:45.313|[HTTP:541458_60784_dXY:crushadmin:91.191.209.10] READ: *command:getServerItem,c2f:QhPs,key:server_settings*
POST|03/07/2025 16:05:45.474|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:45.476|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:45.478|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *command:setServerItem*
POST|03/07/2025 16:05:45.480|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *key:server_settings/plugins/5/1*
POST|03/07/2025 16:05:45.482|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *data_type:vector*
POST|03/07/2025 16:05:45.483|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *data_action:change*
POST|03/07/2025 16:05:45.485|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *data:<plugins_subitem+type="properties">
POST|03/07/2025 16:05:45.487|[HTTP:541458_60784_iQK:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:45.528|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
8. Action #8
  
The hackers calls its plugin now known by the name _CrushSQL_.  
  
The name of the plugin might be a decoy to "hide" this malicious plugin.
  
The plugin is actually a JAR archive.  
  
The hacker seems to have a problem (Crowdstrike blocking?):
  
```
POST|03/07/2025 16:05:45.647|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:05:45.651|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:05:45.652|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *command:pluginMethodCall*
POST|03/07/2025 16:05:45.654|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *method:testSettings*
POST|03/07/2025 16:05:45.655|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *pluginName:CrushSQL*
POST|03/07/2025 16:05:45.658|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *pluginSubItem:*
POST|03/07/2025 16:05:45.659|[HTTP:541458_60784_phx:crushadmin:91.191.209.10] READ: *c2f:QhPs*
POST|03/07/2025 16:05:45.773|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:05:45.788|[HTTP:541458_60804:crushadmin:91.191.209.10] WROTE: *<commandResult><response>java.lang.NullPointerException: Cannot invoke "java.sql.Connection.createStatement()" because "conn" is null</response></commandRe
ACCEPT|03/07/2025 16:07:01.962|[HTTP:541461_57084:lookup:9090] Accepting connection from: 91.191.209.10:57084
```
<br/>
  
9. Action #9
  
Again, the hacker successfully authenticates with crushadmin user, with the correct password:
He now has an admin cookie set.
  
```
POST|03/07/2025 16:07:01.965|[HTTP:541461_57084_Ray::91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:01.966|[HTTP:541461_57084_Ray::91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:01.968|[HTTP:541461_57084_Ray::91.191.209.10] READ: *command:login*
POST|03/07/2025 16:07:01.969|[HTTP:541461_57084_Ray::91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:07:01.971|[HTTP:541461_57084_Ray::91.191.209.10] READ: *password:************
POST|03/07/2025 16:07:01.973|[HTTP:541461_57084_Ray::91.191.209.10] READ: *encoded:true*
POST|03/07/2025 16:07:01.974|[HTTP:541461_57084_Ray::91.191.209.10] READ: *language:en*
POST|03/07/2025 16:07:01.975|[HTTP:541461_57084_Ray::91.191.209.10] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:07:01.991|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:07:01.994|SERVER_LOGIN:SUCCESS:541461:MainUsers:crushadmin:HTTP:91.191.209.10:
POST|03/07/2025 16:07:01.994|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:07:01.996|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *Set-Cookie: currentAuth=4lfh; path=/
```
<br/>
  
10. Action #10
  
Once again, the hacker successfully authenticates with crushadmin user, with the correct password:
He now has an admin cookie set.
  
```
POST|03/07/2025 16:07:01.965|[HTTP:541461_57084_Ray::91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:01.966|[HTTP:541461_57084_Ray::91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:01.968|[HTTP:541461_57084_Ray::91.191.209.10] READ: *command:login*
POST|03/07/2025 16:07:01.969|[HTTP:541461_57084_Ray::91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:07:01.971|[HTTP:541461_57084_Ray::91.191.209.10] READ: *password:************
POST|03/07/2025 16:07:01.973|[HTTP:541461_57084_Ray::91.191.209.10] READ: *encoded:true*
POST|03/07/2025 16:07:01.974|[HTTP:541461_57084_Ray::91.191.209.10] READ: *language:en*
POST|03/07/2025 16:07:01.975|[HTTP:541461_57084_Ray::91.191.209.10] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:07:01.991|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:07:01.994|SERVER_LOGIN:SUCCESS:541461:MainUsers:crushadmin:HTTP:91.191.209.10:
POST|03/07/2025 16:07:01.994|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:07:01.996|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *Set-Cookie: currentAuth=4lfh; path=/
```
<br/>
  
11. Action #11
  
The hacker edits user _crushadmin_ :
  
```
POST|03/07/2025 16:07:02.071|[HTTP:541461_57084_L4J:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:02.073|[HTTP:541461_57084_L4J:crushadmin:91.191.209.10] READ: *command:getUser*
POST|03/07/2025 16:07:02.074|[HTTP:541461_57084_L4J:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:07:02.075|[HTTP:541461_57084_L4J:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:07:02.077|[HTTP:541461_57084_L4J:crushadmin:91.191.209.10] READ: *c2f:4lfh*
POST|03/07/2025 16:07:02.089|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:07:02.165|[HTTP:541461_57094:lookup:9090] Accepting connection from: 91.191.209.10:57094
```
<br/>
  
12. Action #12
  
The hacker changes the _crushadmin_ password:
  
```
POST|03/07/2025 16:07:02.168|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:02.169|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *command:setUserItem*
POST|03/07/2025 16:07:02.171|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *data_action:replace*
POST|03/07/2025 16:07:02.172|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:07:02.174|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:07:02.175|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *user:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:07:02.177|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *xmlItem:user*
POST|03/07/2025 16:07:02.178|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *vfs_items:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:07:02.180|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *permissions:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:07:02.181|[HTTP:541461_57084_jNJ:crushadmin:91.191.209.10] READ: *c2f:4lfh*
POST|03/07/2025 16:07:02.291|[HTTP:541461_57094:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:07:02.918|[HTTP:541461_57106:lookup:9090] Accepting connection from: 91.191.209.10:57106
```
<br/>
  
13. Action #13
  
The hacker uploads the file _/crushtmplog/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt_:
  
```
POST|03/07/2025 16:07:02.921|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:02.922|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:02.924|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *command:openFile*
POST|03/07/2025 16:07:02.926|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *c2f:4lfh*
POST|03/07/2025 16:07:02.928|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *upload_path:/crushtmplog/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt*
POST|03/07/2025 16:07:02.929|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *upload_size:1005600*
POST|03/07/2025 16:07:02.931|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *upload_id:9262ffb4*
POST|03/07/2025 16:07:02.933|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *start_resume_loc:0*
POST|03/07/2025 16:07:02.934|[HTTP:541461_57084_CxA:crushadmin:91.191.209.10] READ: *random:0.345679978990884*
STOR|03/07/2025 16:07:02.944|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *150 Opening BINARY data connection.  Ready to write file /9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt. S T O R*
POST|03/07/2025 16:07:03.243|[HTTP:541461_57106:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
14. Action #14
  
The hacker probably tries to comminicate with his plugin via the POST query _/U/9262ffb4~1~1005600_:
  
```
POST|03/07/2025 16:07:03.322|[HTTP:541461_57084_YeY:crushadmin:91.191.209.10] READ: *POST /U/9262ffb4~1~1005600 HTTP/1.1*
POST|03/07/2025 16:07:03.324|[HTTP:541461_57084_YeY:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:03.553|[HTTP:541461_57106:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
15. Action #15
  
The hacker can see on the screen that the file _/crushtmplog/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt_ has been uploaded with success:
  
```
POST|03/07/2025 16:07:03.673|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:03.676|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:03.678|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *command:closeFile*
POST|03/07/2025 16:07:03.679|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *c2f:4lfh*
POST|03/07/2025 16:07:03.681|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *upload_id:9262ffb4*
POST|03/07/2025 16:07:03.683|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *total_chunks:1*
POST|03/07/2025 16:07:03.685|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *total_bytes:1005600*
POST|03/07/2025 16:07:03.686|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *filePath:/crushtmplog/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt*
POST|03/07/2025 16:07:03.688|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *lastModified:1713988562086*
POST|03/07/2025 16:07:03.690|[HTTP:541461_57084_wik:crushadmin:91.191.209.10] READ: *random:0.10444100243921683*
STOR|03/07/2025 16:07:03.727|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *226-Upload File Size:1005600 bytes @ 982K/sec. MD5=4e1f1c551ea6e66050dc4ac30e152c40*
STOR|03/07/2025 16:07:03.729|[HTTP:541461_57084:crushadmin:91.191.209.10] WROTE: *226 Transfer complete.  MD5=4e1f1c551ea6e66050dc4ac30e152c40 ("/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt" 1005600) STOR*
POST|03/07/2025 16:07:03.744|[HTTP:541461_57106:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
16. Action #16
  
The hacker checks/modifies a setting of a plugin (server_settings/plugins/5/1).

It is pretty obvious that :
1. the file _/crushtmplog/9ffe1bc9-2735-4681-b775-3e59483c5dfe.txt_ is actually a malicious CrushFTP plugin:
2. the hacker has renamed the plugin with a specific name
  
```
POST|03/07/2025 16:07:03.861|[HTTP:541461_57084_YIH:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:03.863|[HTTP:541461_57084_YIH:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:03.865|[HTTP:541461_57084_YIH:crushadmin:91.191.209.10] READ: *command:getServerItem,c2f:4lfh,key:server_settings*
POST|03/07/2025 16:07:04.023|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:07:04.026|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:07:04.027|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *command:setServerItem*
POST|03/07/2025 16:07:04.029|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *key:server_settings/plugins/5/1*
POST|03/07/2025 16:07:04.031|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *data_type:vector*
POST|03/07/2025 16:07:04.033|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *data_action:change*
POST|03/07/2025 16:07:04.035|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *data:<plugins_subitem+type="properties">
POST|03/07/2025 16:07:04.037|[HTTP:541461_57084_flQ:crushadmin:91.191.209.10] READ: *c2f:4lfh*
POST|03/07/2025 16:07:04.079|[HTTP:541461_57106:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
17. Action #17
  
Once again, the hacker successfully authenticates with crushadmin user, with the correct password: He now has an admin cookie set.
  
```
POST|03/07/2025 16:37:35.435|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:35.436|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:35.438|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *command:login*
POST|03/07/2025 16:37:35.439|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:37:35.441|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *password:************
POST|03/07/2025 16:37:35.443|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *encoded:true*
POST|03/07/2025 16:37:35.444|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *language:en*
POST|03/07/2025 16:37:35.445|[HTTP:541465_59652_1Oy::91.191.209.10] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:37:35.460|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:37:35.464|SERVER_LOGIN:SUCCESS:541465:MainUsers:crushadmin:HTTP:91.191.209.10:
POST|03/07/2025 16:37:35.464|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:37:35.465|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *Set-Cookie: currentAuth=uvs6; path=/
```
<br/>
  
18. Action #18
  
The hacker edits user crushadmin :
  
```
POST|03/07/2025 16:37:35.540|[HTTP:541465_59652_31R:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:35.542|[HTTP:541465_59652_31R:crushadmin:91.191.209.10] READ: *command:getUser*
POST|03/07/2025 16:37:35.544|[HTTP:541465_59652_31R:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:37:35.545|[HTTP:541465_59652_31R:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:37:35.546|[HTTP:541465_59652_31R:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:35.558|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:37:35.636|[HTTP:541465_59660:lookup:9090] Accepting connection from: 91.191.209.10:59660
```
<br/>
  
19. Action #19
  
The hacker changes the crushadmin password:
  
```
POST|03/07/2025 16:37:35.638|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:35.639|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *command:setUserItem*
POST|03/07/2025 16:37:35.641|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *data_action:replace*
POST|03/07/2025 16:37:35.642|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:37:35.643|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *username:crushadmin*
POST|03/07/2025 16:37:35.645|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *user:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:37:35.646|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *xmlItem:user*
POST|03/07/2025 16:37:35.648|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *vfs_items:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:37:35.650|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *permissions:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:37:35.652|[HTTP:541465_59652_GsR:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:35.767|[HTTP:541465_59660:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:37:36.416|[HTTP:541465_59666:lookup:9090] Accepting connection from: 91.191.209.10:59666
```
<br/>
  
20. Action #20
  
The hacker uploads the file _/crushtmplog/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt_:
  
```
POST|03/07/2025 16:37:36.418|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:36.420|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:36.422|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *command:openFile*
POST|03/07/2025 16:37:36.423|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:36.425|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *upload_path:/crushtmplog/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt*
POST|03/07/2025 16:37:36.426|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *upload_size:1005437*
POST|03/07/2025 16:37:36.428|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *upload_id:2486994b*
POST|03/07/2025 16:37:36.429|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *start_resume_loc:0*
POST|03/07/2025 16:37:36.431|[HTTP:541465_59652_hPY:crushadmin:91.191.209.10] READ: *random:0.345679978990884*
STOR|03/07/2025 16:37:36.441|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *150 Opening BINARY data connection.  Ready to write file /d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt. S T O R*
POST|03/07/2025 16:37:36.740|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
21. Action #21
  
The hacker probably tries to comminicate with his plugin via the POST query /U/9262ffb411005600:
  
```
POST|03/07/2025 16:37:36.818|[HTTP:541465_59652_sG8:crushadmin:91.191.209.10] READ: *POST /U/2486994b~1~1005437 HTTP/1.1*
POST|03/07/2025 16:37:36.821|[HTTP:541465_59652_sG8:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:37.082|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
22. Action #22
  
The hacker can see on the screen that the file _/crushtmplog/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt_ has been uploaded with success:
  
```
POST|03/07/2025 16:37:37.200|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:37.202|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:37.204|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *command:closeFile*
POST|03/07/2025 16:37:37.205|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:37.207|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *upload_id:2486994b*
POST|03/07/2025 16:37:37.209|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *total_chunks:1*
POST|03/07/2025 16:37:37.211|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *total_bytes:1005437*
POST|03/07/2025 16:37:37.212|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *filePath:/crushtmplog/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt*
POST|03/07/2025 16:37:37.214|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *lastModified:1713988562086*
POST|03/07/2025 16:37:37.216|[HTTP:541465_59652_kyr:crushadmin:91.191.209.10] READ: *random:0.10444100243921683*
STOR|03/07/2025 16:37:37.255|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *226-Upload File Size:1005437 bytes @ 981K/sec. MD5=d69f4f7b365c1d90884035059eae50ec*
STOR|03/07/2025 16:37:37.257|[HTTP:541465_59652:crushadmin:91.191.209.10] WROTE: *226 Transfer complete.  MD5=d69f4f7b365c1d90884035059eae50ec ("/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt" 1005437) STOR*
POST|03/07/2025 16:37:37.271|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
23. Action #23
  
The hacker checks/modifies a setting of a plugin (server_settings/plugins/5/1).

It is pretty obvious that :

1. the file _/crushtmplog/d0525c81-ab12-46d3-88b1-5ce0e3991bd3.txt_ is actually a malicious CrushFTP plugin:
2. the hacker has renamed the plugin with a specific name
  
```
POST|03/07/2025 16:37:37.389|[HTTP:541465_59652_WS1:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:37.390|[HTTP:541465_59652_WS1:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:37.392|[HTTP:541465_59652_WS1:crushadmin:91.191.209.10] READ: *command:getServerItem,c2f:uvs6,key:server_settings*
POST|03/07/2025 16:37:37.550|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:37.552|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:37.554|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *command:setServerItem*
POST|03/07/2025 16:37:37.555|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *key:server_settings/plugins/5/1*
POST|03/07/2025 16:37:37.557|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *data_type:vector*
POST|03/07/2025 16:37:37.559|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *data_action:change*
POST|03/07/2025 16:37:37.561|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *data:<plugins_subitem+type="properties">
POST|03/07/2025 16:37:37.563|[HTTP:541465_59652_sdJ:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:37.786|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
```
<br/>
  
24. Action #24
  
The hackers calls its plugin now known by the name _CrushSQL_.  
  
The name of the plugin might be a decoy to "hide" this malicious plugin.
  
The plugin is actually a JAR archive.
  
```
POST|03/07/2025 16:37:37.904|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:37:37.906|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:37:37.908|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *command:pluginMethodCall*
POST|03/07/2025 16:37:37.910|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *method:testSettings*
POST|03/07/2025 16:37:37.912|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *pluginName:CrushSQL*
POST|03/07/2025 16:37:37.914|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *pluginSubItem:*
POST|03/07/2025 16:37:37.916|[HTTP:541465_59652_tK8:crushadmin:91.191.209.10] READ: *c2f:uvs6*
POST|03/07/2025 16:37:37.947|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:37:37.976|[HTTP:541465_59666:crushadmin:91.191.209.10] WROTE: *<commandResult><response>java.lang.NullPointerException: Cannot invoke "java.sql.Connection.createStatement()" because "conn" is null</response></commandRe
```
<br/>
  
Verdict

- [X] Identify major actions made by 91.191.209.10  under HTTP interface :sunglasses:
  
  <br/>

##  :alien: <a name="link-banned">Get banned IP</a>

Here comes the lsite of all actions made by :  



Here comes the list of all actions made by 91.191.209.10:  



##  :alien: <a name="link-banned">Get banned IP</a>
  
The following command can be used to get some kind of banned IP list:  
  
```
bash# cat crushftp_all.log | grep DENIAL | awk '{print $6}' | awk -F':' '{print $2}' | sort | uniq -c | sort -nr
```
<br/>
  
Voici le résultat final :
  
| Adresse IP       | Requêtes | Adresse IP        | Requêtes | Adresse IP        | Requêtes |
|------------------|----------|-------------------|----------|-------------------|----------|
| 51.79.192.93     | 1919     | 202.4.115.172     | 33       | 121.41.40.116     | 4        |
| 4.4.66.84        | 441      | 167.71.49.0       | 33       | 101.126.149.19    | 4        |
| 41.111.183.173   | 441      | 172.245.177.158   | 31       | 154.83.86.4       | 3        |
| 203.253.70.213   | 441      | 101.89.148.206    | 31       | 61.32.184.198     | 2        |
| 182.184.65.70    | 441      | 95.70.220.109     | 30       | 182.223.17.187    | 2        |
| 164.128.142.212  | 441      | 221.120.56.171    | 27       | 93.84.100.70      | 1        |
| 107.150.119.158  | 441      | 107.173.30.227    | 27       | 84.82.213.72      | 1        |
| 104.248.63.189   | 441      | 36.133.139.254    | 24       | 81.26.255.63      | 1        |
| 20.102.89.253    | 411      | 182.151.13.134    | 21       | 68.78.33.105      | 1        |
| 91.171.4.7       | 287      | 183.47.36.3       | 19       | 49.162.158.25     | 1        |
| 119.1.156.50     | 269      | 117.146.28.174    | 19       | 47.153.83.39      | 1        |
| 125.124.99.83    | 247      | 175.205.191.27    | 16       | 36.137.109.39     | 1        |
| 60.31.215.246    | 207      | 121.229.58.86     | 15       | 222.79.105.211    | 1        |
| 182.61.11.84     | 131      | 45.130.148.244    | 14       | 211.187.29.12     | 1        |
| 36.108.170.78    | 107      | 80.11.197.243     | 13       | 211.168.246.181   | 1        |
| 111.43.14.230    | 79       | 59.53.92.190      | 13       | 210.92.162.139    | 1        |
| 119.204.199.162  | 77       | 117.80.234.78     | 10       | 210.207.221.212   | 1        |
| 138.68.88.167    | 69       | 218.92.0.195      | 9        | 193.254.225.100   | 1        |
| 125.87.84.110    | 68       | 203.34.48.55      | 9        | 186.224.174.105   | 1        |
| 125.80.219.127   | 61       | 131.239.167.122   | 9        | 180.225.93.149    | 1        |
| 125.87.90.207    | 56       | 124.226.219.102   | 9        | 178.205.6.184     | 1        |
| 58.49.59.33      | 47       | 42.51.38.187      | 8        | 178.204.38.41     | 1        |
| 114.143.74.50    | 42       | 175.6.99.202      | 8        | 172.101.35.31     | 1        |
| 203.6.231.136    | 41       | 78.186.248.212    | 7        | 140.119.212.160   | 1        |
| 211.115.190.135  | 40       | 59.22.181.250     | 7        | 1.32.122.29       | 1        |
| 190.181.17.7     | 40       | 47.20.248.179     | 7        | 124.56.225.254    | 1        |
| 101.89.148.7     | 40       | 14.103.127.80     | 7        | 124.56.225.242    | 1        |
| 79.61.217.135    | 38       | 59.51.114.77      | 6        | 122.41.8.165      | 1        |
| 111.67.203.28    | 38       | 218.92.0.245      | 6        | 122.33.147.235    | 1        |
| 62.171.175.198   | 36       | 92.255.57.132     | 4        | 121.188.242.103   | 1        |
| 223.240.79.237   | 36       | 8.152.201.211     | 4        | 120.194.62.119    | 1        |
| 107.173.213.30   | 36       | 47.236.97.125     | 4        | 115.141.226.179   | 1        |
| 61.7.145.116     | 34       | 185.42.12.242     | 4        | 105.101.222.200   | 1        |
| 212.83.189.230   | 34       | 163.44.118.104    | 4        | 102.152.176.5     | 1        |
<br/>
  
One IP is out of the box : 51.79.192.93.  
<br/>
  
Verdict

- [X] Get banned IP :sunglasses:
  
  <br/>

##  :alien: <a name="link-geoip">Get intel from Maxmind</a>
  
Let's use Maxmind to get intel for the head of the stack:   

| IP Address      | Location                                                    | ISP / Organization                                      |
|-----------------|-------------------------------------------------------------|---------------------------------------------------------|
| 51.79.192.93    | Singapore, Singapore (SG), Asia                             | OVH Hosting                                             |
| 4.4.66.84       | Scottsdale, Arizona, United States (US), North America      | Lumen                                                   |
| 41.111.183.173  | Tizi Ouzou, Tizi Ouzou, Algeria (DZ), Africa                | Algerie Telecom                                         |
| 203.253.70.213  | Yongin-si, Gyeonggi-do, South Korea (KR), Asia              | Hankuk University of Foreign Studies Computer Cent      |
| 182.184.65.70   | Gujrat, Punjab, Pakistan (PK), Asia                         | PTCL                                                    |
| 164.128.142.212 | Geneva, Geneva, Switzerland (CH), Europe                    | Swisscom                                                |
| 107.150.119.158 | Hong Kong, Hong Kong (HK), Asia                             | Ucloud Information Technology Hk                        |
| 104.248.63.189  | North Bergen, New Jersey, United States (US), North America | Digital Ocean                                           |
| 20.102.89.253   | Washington, Virginia, United States (US), North America     | Microsoft Azure                                         |
| 91.171.4.7      | Mantes-la-Ville, Île-de-France, France (FR), Europe         | Free SAS                                                |
| 119.1.156.50    | China (CN), Asia                                            | China Telecom                                           |
| 125.124.99.83   | Hangzhou, Zhejiang, China (CN), Asia                        | China Telecom                                           |
| 60.31.215.246   | China (CN), Asia                                            | China Unicom                                            |
| 182.61.11.84    | China (CN), Asia                                            | Beijing Baidu Netcom Science and Technology Co.         |
| 36.108.170.78   | China (CN), Asia                                            | China Telecom                                           |
| 111.43.14.230   | Harbin, Heilongjiang, China (CN), Asia                      | China Mobile, HeiLongJiang Mobile Communication Company |
| 119.204.199.162 | Chungju, North Chungcheong, South Korea (KR), Asia          | KT                                                      |
| 138.68.88.167   | Frankfurt am Main, Hesse, Germany (DE), Europe              | Digital Ocean                                           |
| 125.87.84.110   | Shanghai, Shanghai, China (CN), Asia                        | China Telecom                                           |
| 125.80.219.127  | Chongqing, Chongqing, China (CN), Asia                      | China Telecom                                           |
| 125.87.90.207   | Chongqing, China (CN), Asia                                 | China Telecom                                           |
| 58.49.59.33     | Wuhan, Hubei, China (CN), Asia                              | China Telecom                                           |
| 114.143.74.50   | Pune, Maharashtra, India (IN), Asia                         | Tata Teleservices Maharashtra                           |
| 203.6.231.136   | China (CN), Asia                                            | Cloud Computing Corporation                             |
| 211.115.190.135 | Seogwipo, Jeju-do, South Korea (KR), Asia                   | KT                                                      |
<br/>
  
China litteraly pops out!  
<br/>
  
Verdict

- [X] Get intel from Maxmind :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-http">Get unsuccessfull HTTP login attemps</a>
  
It's time to extrat the unsuccessfull HTTP login attempts : 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':HTTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
<br/>
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| X          | 6        |
| anonymous  | 4        |
| a274abc8e2 | 2        |
<br/>
  
Verdict

- [X] Get unsuccessfull HTTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-sftp">Get unsuccessfull SFTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull SFTP login attempts. 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':SFTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
<br/>
  
This the result:
  
| Username  | Attempts | Username   | Attempts | Username | Attempts |
|-----------|----------|------------|----------|----------|----------|
| user      | 22       | qemu       | 2       | live      | 1        |
| pi        | 10       | odoo       | 2       | kubelet   | 1        |
| minecraft | 7        | metricbeat | 2       | hduser    | 1        |
| ubnt      | 6        | mcserver   | 2       | groupe    | 1        |
| oracle    | 6        | es         | 2       | games     | 1        |
| a         | 6        | dspace     | 2       | ftuser    | 1        |
| postgres  | 4        | zjw        | 1       | ftp       | 1        |
| hadoop    | 4        | user1      | 1       | fa        | 1        |
| ansible   | 4        | ubuntu     | 1       | esuser    | 1        |
| nagios    | 3        | support    | 1       | devops    | 1        |
| kafka     | 3        | steam      | 1       | craft     | 1        |
| guest     | 3        | samba      | 1       | cluster   | 1        |
| vyos      | 2        | prometheus | 1       | centos    | 1        |
| usr       | 2        | posiflex   | 1       | b         | 1        |
| test      | 2        | olm        | 1       | ansadmin  | 1        |
<br/>
  
Verdict

- [X] Get unsuccessfull SFTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-ftp">Get unsuccessfull FTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull FTP login attempts : 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':FTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
<br/>
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| anonymous  | 37       |
<br/>
  
Verdict

- [X] Get unsuccessfull FTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-success-http">Get successfull HTTP login attemps</a>
  
Let's switch to successfull HTTP login attemps :  
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:SUCCESS' |  awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
<br/>
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| crushadmin | 37       |
<br/>
  
Verdict

- [X] Get successfull HTTP login attempss :sunglasses:
  
  <br/>



  
