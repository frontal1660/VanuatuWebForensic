# :100: VanuatuForensic :100:  
<br/>

![image](https://github.com/user-attachments/assets/09b98e74-d7cb-487b-b7e8-fddd0fd731d0)  
<br/>

## :alien: Action plan
Action list :  
- [ ] [Get banned IP](#link-banned)
  
  <br/>

##  :alien: <a name="link-banned">Get banned IP</a>
  
The following command can be used to get some kind of banned IP list :  
  
```
bash# cat crushftp_all.log | grep DENIAL | awk '{print $6}' | awk -F':' '{print $2}' | sort | uniq -c | sort -nr
```
  
Voici le résultat final :
  
| Adresse IP       | Requêtes | Adresse IP        | Requêtes | Adresse IP        | Requêtes |
|------------------|----------|-------------------|----------|-------------------|----------|
| 51.79.192.93     | 1919     | 91.171.4.7        | 287      | 125.87.84.110     | 68       |
| 4.4.66.84        | 441      | 119.1.156.50      | 269      | 125.80.219.127    | 61       |
| 41.111.183.173   | 441      | 125.124.99.83     | 247      | 125.87.90.207     | 56       |
| 203.253.70.213   | 441      | 60.31.215.246     | 207      | 58.49.59.33       | 47       |
| 182.184.65.70    | 441      | 182.61.11.84      | 131      | 114.143.74.50     | 42       |
| 164.128.142.212  | 441      | 36.108.170.78     | 107      | 203.6.231.136     | 41       |
| 107.150.119.158  | 441      | 111.43.14.230     | 79       | 211.115.190.135   | 40       |
| 104.248.63.189   | 441      | 119.204.199.162   | 77       | 190.181.17.7      | 40       |
| 20.102.89.253    | 411      | 138.68.88.167     | 69       | 101.89.148.7      | 40       |
  
One IP is out of the box : 51.79.192.93.
  
Verdict

- [X] Get banned IP :sunglasses:
  
  <br/>

##  :alien: <a name="link-geoip"></a>









