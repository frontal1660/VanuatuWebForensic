# :100: VanuatuForensic :100:  
<br/>

![image](https://github.com/user-attachments/assets/09b98e74-d7cb-487b-b7e8-fddd0fd731d0)  
<br/>

## :alien: Action plan
Action list :  
- [ ] [Get banned IP](#link-banned)
  
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
  
It's time to extrat the unsuccessfull HTTP login attempts. 
  
TABLEAU
  
Verdict

- [X] Get intel from Maxmind :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-sftp">Get unsuccessfull SFTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull SFTP login attempts. 
  
TABLEAU
  
Verdict

- [X] Get unsuccessfull SFTP login attemps :sunglasses:
  
  <br/>

##  :alien: <a name="link-fail-sftp">Get unsuccessfull FTP login attemps</a>
  
We can continue with the extraction of the unsuccessfull FTP login attempts. 
  
TABLEAU
  
Verdict

- [X] Get unsuccessfull FTP login attemps :sunglasses:
  
  <br/>





  
