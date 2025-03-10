# :100: VanuatuWebForensic :100:  
<br/>

![image](https://github.com/user-attachments/assets/09b98e74-d7cb-487b-b7e8-fddd0fd731d0)  
<br/>

## :alien: Action plan
Action list :  
- [ ] [Get the datetime crushadmin password was changed](#link-adm-changed)
- [ ] [Identify major actions made by 147.45.112.220 under HTTP interface](#link-actions)
- [ ] [Get banned IP](#link-banned)
- [ ] [Get intel from Maxmind](#link-geoip)
- [ ] [Get unsuccessfull HTTP login attemps](#link-fail-http)
- [ ] [Get unsuccessfull SFTP login attemps](#link-fail-sftp)
- [ ] [Get unsuccessfull FTP login attemps](#link-fail-ftp)
- [ ] [Get successfull HTTP login attemps](#link-success-http)


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

- [X] >Get the datetime crushadmin when password was changed :sunglasses:
  
  <br/>

##  :alien: <a name="link-actions">Identify major actions made by 147.45.112.220 under HTTP interface</a>
  
1. Action #1
  

```
POST|03/07/2025 16:03:36.641|[HTTP:541455_33326_8sB::147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.643|[HTTP:541455_33326_8sB::147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:36.644|[HTTP:541455_33326_8sB::147.45.112.220] READ: *command:login*
POST|03/07/2025 16:03:36.646|[HTTP:541455_33326_8sB::147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.648|[HTTP:541455_33326_8sB::147.45.112.220] READ: *password:************
POST|03/07/2025 16:03:36.649|[HTTP:541455_33326_8sB::147.45.112.220] READ: *encoded:true*
POST|03/07/2025 16:03:36.650|[HTTP:541455_33326_8sB::147.45.112.220] READ: *language:en*
POST|03/07/2025 16:03:36.652|[HTTP:541455_33326_8sB::147.45.112.220] READ: *random:0.5784904717377481*
STOR|03/07/2025 16:03:36.684|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *230 Password OK.  Connected.*
SERVER|03/07/2025 16:03:36.687|SERVER_LOGIN:SUCCESS:541455:MainUsers:crushadmin:HTTP:147.45.112.220:
POST|03/07/2025 16:03:36.688|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:36.689|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *Set-Cookie: currentAuth=zIpc; path=/
```
  
2. Action #2
  

```
POST|03/07/2025 16:03:36.720|[HTTP:541455_33326_fhu:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.721|[HTTP:541455_33326_fhu:crushadmin:147.45.112.220] READ: *command:getUser*
POST|03/07/2025 16:03:36.723|[HTTP:541455_33326_fhu:crushadmin:147.45.112.220] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:03:36.724|[HTTP:541455_33326_fhu:crushadmin:147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.725|[HTTP:541455_33326_fhu:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:36.737|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:03:36.770|[HTTP:541455_33328:lookup:9090] Accepting connection from: 147.45.112.220:33328
```

3. Action #3
  

```
POST|03/07/2025 16:03:36.772|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:36.773|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *command:setUserItem*
POST|03/07/2025 16:03:36.775|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *data_action:replace*
POST|03/07/2025 16:03:36.776|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *serverGroup:MainUsers*
POST|03/07/2025 16:03:36.778|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *username:crushadmin*
POST|03/07/2025 16:03:36.779|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *user:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.781|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *xmlItem:user*
POST|03/07/2025 16:03:36.783|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *vfs_items:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.784|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *permissions:<?xml+version="1.0"+encoding="utf-8"?>
POST|03/07/2025 16:03:36.786|[HTTP:541455_33326_Bj7:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:36.883|[HTTP:541455_33328:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
ACCEPT|03/07/2025 16:03:37.261|[HTTP:541455_33330:lookup:9090] Accepting connection from: 147.45.112.220:33330
```
  
4. Action #4
  

```
POST|03/07/2025 16:03:37.263|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.265|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.267|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *command:openFile*
POST|03/07/2025 16:03:37.268|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:37.270|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *upload_path:/crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt*
POST|03/07/2025 16:03:37.271|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *upload_size:1003702*
POST|03/07/2025 16:03:37.273|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *upload_id:2148654e*
POST|03/07/2025 16:03:37.275|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *start_resume_loc:0*
POST|03/07/2025 16:03:37.276|[HTTP:541455_33326_kOR:crushadmin:147.45.112.220] READ: *random:0.345679978990884*
STOR|03/07/2025 16:03:37.287|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *150 Opening BINARY data connection.  Ready to write file /1871264c-ce01-4270-aef1-6a2f38515ad7.txt. S T O R*
POST|03/07/2025 16:03:37.586|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:37.619|[HTTP:541455_33326_rur:crushadmin:147.45.112.220] READ: *POST /U/2148654e~1~1003702 HTTP/1.1*
POST|03/07/2025 16:03:37.621|[HTTP:541455_33326_rur:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.727|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
  
5. Action #5
  

```
POST|03/07/2025 16:03:37.763|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.764|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.766|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *command:closeFile*
POST|03/07/2025 16:03:37.768|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:37.769|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *upload_id:2148654e*
POST|03/07/2025 16:03:37.771|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *total_chunks:1*
POST|03/07/2025 16:03:37.773|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *total_bytes:1003702*
POST|03/07/2025 16:03:37.774|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *filePath:/crushtmplog/1871264c-ce01-4270-aef1-6a2f38515ad7.txt*
POST|03/07/2025 16:03:37.776|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *lastModified:1713988562086*
POST|03/07/2025 16:03:37.778|[HTTP:541455_33326_57F:crushadmin:147.45.112.220] READ: *random:0.10444100243921683*
STOR|03/07/2025 16:03:37.817|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *226-Upload File Size:1003702 bytes @ 980K/sec. MD5=1945485edcdea03caad347041b7b8a37*
STOR|03/07/2025 16:03:37.819|[HTTP:541455_33326:crushadmin:147.45.112.220] WROTE: *226 Transfer complete.  MD5=1945485edcdea03caad347041b7b8a37 ("/1871264c-ce01-4270-aef1-6a2f38515ad7.txt" 1003702) STOR*
POST|03/07/2025 16:03:37.838|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
  
6. Action #6
  

```
POST|03/07/2025 16:03:37.870|[HTTP:541455_33326_6n8:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.872|[HTTP:541455_33326_6n8:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.874|[HTTP:541455_33326_6n8:crushadmin:147.45.112.220] READ: *command:getServerItem,c2f:zIpc,key:server_settings*
POST|03/07/2025 16:03:37.941|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:37.943|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:37.945|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *command:setServerItem*
POST|03/07/2025 16:03:37.947|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *key:server_settings/plugins/5/1*
POST|03/07/2025 16:03:37.949|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *data_type:vector*
POST|03/07/2025 16:03:37.951|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *data_action:change*
POST|03/07/2025 16:03:37.953|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *data:<plugins_subitem+type="properties">
POST|03/07/2025 16:03:37.954|[HTTP:541455_33326_EOg:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:38.171|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
```
  
7. Action #7
  

```
POST|03/07/2025 16:03:38.244|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *POST /WebInterface/function/ HTTP/1.1*
POST|03/07/2025 16:03:38.246|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *user_ip: 127.0.0.1*
POST|03/07/2025 16:03:38.248|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *command:pluginMethodCall*
POST|03/07/2025 16:03:38.250|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *method:testSettings*
POST|03/07/2025 16:03:38.252|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *pluginName:CrushSQL*
POST|03/07/2025 16:03:38.254|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *pluginSubItem:*
POST|03/07/2025 16:03:38.256|[HTTP:541455_33326_mky:crushadmin:147.45.112.220] READ: *c2f:zIpc*
POST|03/07/2025 16:03:38.267|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *HTTP/1.1 200 OK*
POST|03/07/2025 16:03:38.270|[HTTP:541455_33330:crushadmin:147.45.112.220] WROTE: *<commandResult><response>java.lang.UnsupportedClassVersionError: com/mysql/jdbc/Driver has been compiled by a more recent version of the Java Runtime (class file version 67.0), this version of the Java Runtime only recognizes class file versions up to 61.0</response></commandResult>*
```

         
  
Verdict

- [X] Identify major actions made by 147.45.112.220  under HTTP interface :sunglasses:
  
  <br/>

##  :alien: <a name="link-banned">Get banned IP</a>
  
The following command can be used to get some kind of banned IP list:  
  
```
bash# cat crushftp_all.log | grep DENIAL | awk '{print $6}' | awk -F':' '{print $2}' | sort | uniq -c | sort -nr
```
  
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
  
One IP is out of the box : 51.79.192.93.
  
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
  
China litteraly pops out!
  
Verdict

- [X] Get intel from Maxmind :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-http">Get unsuccessfull HTTP login attemps</a>
  
It's time to extrat the unsuccessfull HTTP login attempts : 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':HTTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| X          | 6        |
| anonymous  | 4        |
| a274abc8e2 | 2        |
  
Verdict

- [X] Get unsuccessfull HTTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-sftp">Get unsuccessfull SFTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull SFTP login attempts. 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':SFTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
  
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
  
Verdict

- [X] Get unsuccessfull SFTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-ftp">Get unsuccessfull FTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull FTP login attempts : 
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:FAIL' | grep ':FTP' | awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| anonymous  | 37       |
  
Verdict

- [X] Get unsuccessfull FTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-success-http">Get successfull HTTP login attemps</a>
  
Let's switch to successfull HTTP login attemps :  
  
```
cat crushftp_all.log | grep 'SERVER_LOGIN:SUCCESS' |  awk -F':' '{print $7}' | sort | uniq -c | sort -nr
```
  
This the result:
  
| Username   | Attempts |
|------------|----------|
| crushadmin | 37       |
  
Verdict

- [X] Get successfull HTTP login attempss :sunglasses:
  
  <br/>



  
