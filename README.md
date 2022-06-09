# TP_KafkaBrokers
TP_KafkaBrokers


Pour demarer kafka on a besion tout d'abord de demarer un utile qui s'appel zookeeper qui permet de faire la coordination entre les defirente instance du brokers kafka.

![image](https://user-images.githubusercontent.com/102295113/172881882-da8948f5-41f5-412b-af43-7784dcfa5d41.png)

-->alors zookeeper est demarer sur le port 2181.

 ![image](https://user-images.githubusercontent.com/102295113/172882014-ab755cc6-1ad1-4fae-a7d2-cab2ce8736aa.png)
 
 - une fois que zookeeper demarer en peut par suite demarer le server kafka en utilisant kafka-server-start :
 
 ![image](https://user-images.githubusercontent.com/102295113/172883791-a69fddf6-3cea-4d4d-949a-27ff08a055ce.png)
 
 -->Alors kafka est demarer par defaut sur le porte 9092 :
 
 ![image](https://user-images.githubusercontent.com/102295113/172888547-c8c9401c-594a-4b7a-9206-00ff74a0b11b.png)

 -Et pour faire des teste on a besion de demarer :
 
     - kafka-console-consumer: qui permet à n'importe quel application(java,c++,..) de faire une s'abscribe vers le topic R1 pour consommer les messages  qui arive apres ma subscribtion :
     
![image](https://user-images.githubusercontent.com/102295113/172930702-202c3ddb-012b-44a6-9c69-ed7ff0891410.png)


      
     -kafka-console-producer: qui permet de produire des messages vers le topic qui s'appel R1:
     
     ![image](https://user-images.githubusercontent.com/102295113/172934761-ab499a05-e443-4ecc-854a-01b60c15832b.png)

    
![image](https://user-images.githubusercontent.com/102295113/172933966-a4f8e440-d218-4ac0-a106-36c928d0681b.png)

- Et pour consommer tout les donnees qui se trouve ds le topic en ajeut --from-beginning:

![image](https://user-images.githubusercontent.com/102295113/172934489-91e3a338-57d9-4790-92bf-2f57c207ffde.png)

![image](https://user-images.githubusercontent.com/102295113/172934296-829c38b7-47d9-4b4d-8ea6-c1cd1890991f.png)




     
     
     


 

