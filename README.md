# TP_KafkaBrokers
TP_KafkaBrokers

##Parte 1 : Even driven distributed processing with spring cloud stream function- KAFKA Broker:

#Démarage de serveur Zookeeper:

Pour demarer kafka on a besion tout d'abord de demarer un utile qui s'appel zookeeper qui permet de faire la coordination entre les defirente instance du brokers kafka.

![image](https://user-images.githubusercontent.com/102295113/172881882-da8948f5-41f5-412b-af43-7784dcfa5d41.png)

-->alors zookeeper est demarer sur le port 2181.

 ![image](https://user-images.githubusercontent.com/102295113/172882014-ab755cc6-1ad1-4fae-a7d2-cab2ce8736aa.png)
 
 #Démarage de serveur kafka:
 
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

- Et si on ajoute --from-beginning :

![image](https://user-images.githubusercontent.com/102295113/172934489-91e3a338-57d9-4790-92bf-2f57c207ffde.png)

--> On remarque que le comsomateur consommer  tout les donnees qui se trouve dans le topic :

![image](https://user-images.githubusercontent.com/102295113/172934296-829c38b7-47d9-4b4d-8ea6-c1cd1890991f.png)

##1- Application spring boot with kafka-console-consumer :

- On commance par creer une classe PageEvent qui definier par:
     -nom de page.
     -nom de l'utilisateur qui visite la page .
      - la date de visite de la page
      -  la duree passer par la page.
 ce classe permet de gerer des evenoment qui sont produisse dans les page visiter par les utilisateur
 
 -Puis creer une RestController dans le paquage web qui appeler PageEventRestController et pour envoyer une msg au lieu d'utiliser kafkaTemplate ou JMSTemplate il suffit d'utiliser un objet  StreamBridge qui permet d'envoyer un msg mais  indepandament des brokers (kafka,jms rabbitMQ..) , et pour envoyer ce msg en utilise StreamBridge.send . et ce msg et par defaut serealiser en format Json
 
![image](https://user-images.githubusercontent.com/102295113/172953780-1827de39-1e39-45a3-a9de-70015e14f757.png)

##2-Creation d'un  consumer avec Spring cloud Streams :

-Il suffit de creer une classe PageEventService(un service) dans lequel on creer une methode pageEventConsumer avec la notation Bean qui permet de retourner un objet de type consumer et apres autoumatiquement spring cloud streams fait une subscribe vers un topic kafka et il va attentre le msg qui arive il va etre recuperer et finallement afficher.

- Et pour le consomateur qu'on a creer consommer des msg a partire d'un topic R1 et non pas le chnnel pageEventConsumer-in-0 qui choisir par defaut par spring cloud streams on a besoin d'ajouter cette ligne ds le fichier de configuration application.properties:

![image](https://user-images.githubusercontent.com/102295113/172955134-b8d6d6b7-49fb-49b1-9f18-b46c1e94bf9d.png)

![image](https://user-images.githubusercontent.com/102295113/172956236-74b95494-e3c0-422c-b8c7-d82e50e3dd81.png)
 
 ##3-creation un supplier avec Spring cloud Streams :
 
 - Il suffit d'ajouter une fonction de type supplier qui s'appel pageEventSupplier ds lequel pour chaque seconde je voudrait envoyer un ms page event et publier ds un topic kafka.
 
 - une fonction de type supplier produit des msg ds un topic par defaut qui appel le meme nomde fonction.out-0 et pour utiliser un autre topic on a besion d'ajouter cette ligne ds le fichier de configuration application.properties , et pour utiliser plusieur fonction on mem application on a besion de declare et pour .
 
 ![image](https://user-images.githubusercontent.com/102295113/172959298-1e55d467-becc-442b-a586-00061bdd75ad.png)

![image](https://user-images.githubusercontent.com/102295113/172961987-d674cf93-d278-4a8e-9903-a0ec125b7829.png)



![image](https://user-images.githubusercontent.com/102295113/172959886-009d5237-f5b8-44ea-8ca8-77d5a3c282e1.png)

##5-kafka Streams :

- Il suffit d'ajouter une fonction pageEventFunction de type Function qui permet de traiter un flux d'enregistrement du topic R2 en temps real pour prendre des decision et produit un resultat  qui va vers un autre topic qui appel R3.

>>>>>>>>

##Partie2
- Dans ce partien , on traiter que les evenement de visite de page ds la duree de     visite passe 100 ms et je produit vers un topic R4 un stream ds lequel la clee  c   est le nom de la page et le valeur c'est le nbr de fois que la page a ete           visiter.
- Et pour demander a kafka-conole-consumer pour afficher que le kley et valeur on a utiliser la commande suivant :

>>>>>>>>>
- Et pour applique la fonction d'agregation Count() uniquement sur l'ensemble des enregistrement qui observer pendant le 5 dernier second on a utiliser l'operation de fenêtrage .windowdBy et ds ce cas on a retourner un objet de type KTable au lieu de KStream

>>>>>>>>30min 

- Apres les resultats de count stocker ds un store (KTable )qui s'appel page-count ds lequel kafkaStreams va stocker a chaque fois les eregistrement qui represente les dernier calcule qui effectue et apres pour chaque second evoyer ces resultat calculer vers le client qui établir une connexion http.

>>>>>>34min

- Puis on a creer une simple page html ds laquel on a utiliser une librere qui s'apple smothie.js qui permet de representer les graphique dynamique(les donnees recuperer en temps real) 

>>>>>1h:07min

















 





     
     
     


 

