# Dodo Gallery
## **Motivation**
The world is moving fast, and so are we. With it, incredible civilization succeeds. But with it, spiritual value's left behind. Family, considered vital part of our life, is no doubt victim of the fast-moving modern world. *Dodo Gallery* was created to solve this problem. By letting each and every person go through three stages of interactive experience, the project aims to remind the user of family, urging him/her to take action and spend time to what is meant to value most.

## **About**
*Dodo Gallery* is a collaborated graduation project of six undergraduates from two departments of National Taipei University of Technology:
* Department of Interaction Design
* Department of Computer Science and Information Technology

The project was initiated in September 2019 and is expected to end in June 2021.
## **Our Team**
Our team name is [Dodo Cafe](https://github.com/DodoCafe).
#### Department of Interaction Design
* [106ac2016 王品筑](https://github.com/kai85559)
* 106ac1023 林秀靜
* 106ac2007 林恩雅

#### Department of Computer Science and Information Technology
* [106590040 温致綱](https://github.com/gougon)
* [106590048 陳風平](https://github.com/phogbinh)
* [106590026 高楷杰](https://github.com/mdvv85009)
* [106590018 廖彥澤](https://github.com/s88037zz) (Contract)

## **Interactive Experiences**
Our main presentation method is to use the projection screen to project 4 pictures, just like a gallery.
#### First picture<br>
* When user walk close to the picture, the cellphone will start ring. Then user can pick up the cellphone and listen to the phonograph.  When the phonograph finished, the picture enter standby screen.
#### Second picture<br>
* User can use walking device(pressure sensor/macky macky) to moving for 15 seconds. After 15 seconds, the picture shows slogan and moving speed decrease to 0 in 5 seconds and enter standby screen.
#### Third picture<br>
* The picture is the foggy window. User can use hand to wipe the window.<br>
* User will sit on the chair and the projection screen will show him and his mother (fictional) sitting on the chair and eating together.<br>
#### Fourth picture<br>
* Each user's emotions during the experience will be synthesized into a color and become square in a Montage painting.

## **Implementation**
Our main platform is PC and other device(pressure detect device, cellphone, infrared detect device, Kinect...).
#### First picture<br>
* We use infrared detect user's entering and inform the cellphone. The cellphone then start ringing. After user pick up the phone and listen to the phonograph, the cellphone will inform the PC. Then, PC goes to the second picture.
#### Second picture<br>
* When the first picture end, the second picture shows up. The picture prompts the user to tread on the walking device(pressure sensor/macky macky) which under his feet. User can move by tread the walking device, then computer will start count for 15 seconds. After 15 seconds, the picture shows slogan and moving speed decrease to 0 in 5 seconds and enter standby screen.
#### Third picture<br>
* When second picture end, the third picture start. We use Kinect to implement touch detection within a certain distance of the projection screen. User use this technic to wipe the fog out.
* When the user wipes off the fog, the user needs to sit on the chair, and kinect will detect his sitting position and we will merge it into the picture.
#### Fourth picture<br>
* When third picture end, the fourth picture start. We just calculate the emotions and put it into random square on Montage painting.
#### The skill in whole experience<br>
* We use face emotion recognition to dynamically detect user's emotion. Next picture will be affected by user's emotion.


## **Technologies**
### Android Unity Communication<br>
* We use Socket to accomplish this feature. The server and client use particular message to inform each other.
### Kinect Depth Trigger<br>
* We use Kinect to get depth information and use median filter to reduce the noise.
### 3D FER<br>
* We use Kernel method + SVM and LSTM to recognize emotion.
### Raspberry Pi TCP Infrared Motion Detection<br>
* We architect and implement infrared sensor multithreaded system which employs TCP socket to send sensor motion signal from Raspberry Pi to Unity desktop app.

## Demo
#### Dodo Gallery - Progress<br>
* https://www.youtube.com/watch?v=awNf7QXRdYw
#### Raspberry Pi TCP Infrared Motion Detection with Unity<br>
* https://www.youtube.com/watch?v=_uFyIu8G5lA&feature=youtu.be
#### Kinect Depth Trigger - Unfilter
![Kinect Depth Trigger Unfilter Demo](./image_demo_kinect_depth_trigger-unfilter.png)<br>
#### Kinect Depth Trigger - Untrigger
![Kinect Depth Trigger Untrigger Demo](./image_demo_kinect_depth_trigger-untrigget.png)<br>
#### Kinect Depth Trigger - Unfilter
![Kinect Depth Trigger Trigger Demo](./image_demo_kinect_depth_trigger-trigget.png)<br>
#### 3D FER - Preprocessing<br>
![3D FER Preprocessing Demo](./image_demo_3D_FER_preprocessing.png)<br>

## Design Patterns
### Force
![Force diagram](./image_force.png)
### MVC
* We use this pattern in whole project
* Motivation : We want to decoupling classes, keep code clean, and easy to read
* Solution : MVC can accomplish these all factors
* Consequence : 
    * Easy to maintain
    * Decoupling classes
    * The code need to go through multiple layer from base class to view
    * Decrease the efficiency
### `Android Unity Communication`
#### Observer
* Motivation : We need a mechanism to that socket thread inform main thread what message it receive
* Solution : Observer can avoid main thread busy wating
* Consequense : 
    * Avoid busy waiting
    * Follow by MVC pattern, the observer need to go through multiple layer and generate readers and news
* Class Diagram：<br>
![Android Observer Class Diagram](./image_class_diagram_Android_observer.png)<br><br>
### `3D FER`<br>
#### Repository (Patterns of Enterprise Application Architecture)
* Motivation : We have a lot of vertices, boundary vertices, and holes data. Sinve we are constantly changing these data during AFM algorithm, we hope that these data are shared so that datas will be changed while single component change these datas
* Solution : Repository pattern can see vertices, boundary vertices, and holes as different tables, and all components can access these tables
* Consequence : 
    * Encapsulate data so that client doesn't have to know the implementation details
    * Make the components independent of each other, no need to transmit the data changed information
    * Split domain model and data model
    * Each access to data, we need to pass by repository, resulting in performance decreased
* Class Diagram : <br>
![Android Ring Class Diagram](./image_class_diagram_3D FER_Repository.png)<br>
#### Unit Of Work (Patterns of Enterprise Application Architecture)
* Motivation : We already have different repositories, but we usually use different repositories when doing algorithms. When we modified single repository will affect other repositories
* Solution : Unit Of Work can be like Database, let us wrap the operations of operating different repository into one operation. We can implement the logic of operations by Unit Of Work so that client can only focus on the operation
* Consequence : 
    * Increase the reliability of the entire data system
    * Decrease repetitive codes that affect each other (Repository)
    * Can implement the rule of database (ex. cascade)
    * Because we need to cross Unit Of Work and repository when we need to use data, it is difficult to optimize the operation of data
* Class Diagram : <br>
![Android Ring Class Diagram](./image_class_diagram_3D FER_UOW.png)<br>
#### Pipe And Filter
* Motivation : We have different algorithm for the face preprocessing (even some of them are the same algorithm family), and we need to combination different algorithms when training the model to find the best solution. Therefore, we hope to replace the algorithm easily and don't need to pay a lot of effort
* Solution : Pipe And Filter can split different algorithms, and use pipe to determine algorithm steps
* Consequence : 
    * Due to the large amount of data to be trained, if it is found to be too slow in the future, we can easily change it to parallel computing
    * Easy to understand each step of algorithm
    * Replace algorithm is easy because they have the same interface
    * Because of the existence of pipe, it increases the time to process single mesh
    * Error handling and rescovery is difficult to implement
* Class Diagram : <br>
![Android Ring Class Diagram](./image_class_diagram_3D FER_PipeAndFilter.png)<br>
#### Strategy
* Motivation : We would try using the different algorithm in feature selection. We need to let object with more flexible in order to compare the effect in each algorithm.
* Soution : We can let object have abilty of alternative in a member function by using Strategy pattern.
* Consequence:
    * Inheritance can help factor out common functionality of the algorithm.
    * It offers an alternative to conditional statements for selecting desired behavior.
    * The client need to know how Stragegy differ before it select the appropriate one.
    * Strategies increase the number of onjects in an application.
* Class Diagram : <br>
![Android Ring Class Diagram](./image_class_diagram_3D FER_Strategy.png)<br>

### `Signal Receiving TCP Socket`<br>
#### State
* Motivation：The socket is designed to have two states - Connecting and Disconnecting - and thus needs a mechanism to handle state transitions
* Solution：State Pattern prevails the method of scattering state conditional statement across the class methods in tackling the proposed problem
* Consequence：
    * It localizes state-specific behavior and partitions behavior for different states
    * It makes state transitions explicit
* Class Diagram：<br>![Signal Receiving TCP Socket Class Diagram](./image_class_diagram_signal_receiving_tcp_socket.jpg)
* Object Diagram：<br>![Signal Receiving TCP Socket Object Diagram](./image_object_diagram_signal_receiving_tcp_socket.jpg)
### `Unity`
#### State
* Motivation：We want the state of process can dynamic transfer to another
* Solution：State Pattern can help us manage the transition of state easily.
* Consequense：
    * Easy to manage code in each state
    * Easy to change the transitions of each state
    * Need to control the amount of state, because each addtional state must add a new class
    * Hard to limit "How to use" in program, each developer of group must follow the state machine rules
* Class Diagram : <br>
![Unity GameState Class Diagram](./image_class_diagram_Unity_GameState.png)<br>
#### Singleton
* Motivation：We only need one instance, which could let whole system can visit it.
* Solution：Let the logic more clearly, don't need to care if the object is constructed. 
* Consequense：
    * Provide only one method to create the singleton object, avoid a lot of mess.
    * Increase readability.
    * Increase debug difficulty, because everyone can access the object.
* Class Diagram : <br>
![Unity UItexture Class Diagram](./image_class_diagram_Unity_UItextureSingleton.png)<br>


# Contributions
### 陳風平
* Initiate collab with 3 Design Dept undergrads to form team of 6 creating an interactive experience themed home.
* Architect and implement infrared sensor multithreaded system which employs TCP socket to send sensor motion signal from Raspberry Pi to Unity desktop app.
* Technologies: C#, Python, UWP, MSTest, Unity 3D, Git, Asana.

### 高楷杰
* Disign and implement main process logical architecture by using unity 3D.
* Technologies: Unity 3D.

### 溫致綱
* Implement socket communication between Android & Unity
* Implement Kinect depth trigger
* Participate in 3D FER and implement preprocessing
* Technologies: C#, Java, Python, Socket, Kinect.

## Source Codes
* [DodoCafe](https://github.com/DodoCafe/DodoCafe)
    * State
        * CSignalReceivingTcpSocket.cs
        * ISignalReceivingTcpSocketState.cs
        * CSignalReceivingTcpSocketConnectingState.cs
        * CSignalReceivingTcpSocketDisconnectingState.cs
* [DodoCafePluginTest](https://github.com/DodoCafe/DodoCafePluginTest)
* [Raspberry Pi TCP Infrared Motion Detection](https://github.com/DodoCafe/raspberry-pi-tcp-infrared-motion-detection)
* [DodoGalleryUnity](https://github.com/mdvv85009/DodoGalleryUnity)
    * State
        * ISceneState.cs
        * SceneStateController.cs
        * FirstSceneState.cs
        * SecondSceneState.cs
        * ThirdSceneState.cs
    * Singleton
        * UITexture.cs   
* [Android communication with Unity](https://github.com/Gougon-Side-Project/Android-DodoCagePhonograph)
    * Observer
        * IObserver.java
        * ISubject.java
        * Client.java
        * MainActivity.java
        * MainPM.java
        * MusicPlayer.java
        * TimeHandler.java
        * TimeRunnable.java
* [3D FER](https://github.com/3D-face-recognition/3D-Face-Recongnition)<br>
    * Repository
        * interface_repository.py
        * vertex_repository
        * boundary_vertex_repository.py
        * hole_repository.py
    * Unit of Work
        * unit_of_work.py
    * Pipe and Filter
        * interface_pipe_and_sink.py
        * preprocessing_pipe.py
        * preprocessing_sink.py
        * interface_precessing_filter.py
        * taubin_smoothing_filter.py
        * humphrey_smoothing_filter.py
        * z_circle_cropping_filter.py
        * afm_filling_hole_filter.py