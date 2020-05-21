# Dodo Gallery
## Motivation
The world is moving fast, and so are we. With it, incredible civilization succeeds. But with it, spiritual value's left behind. Family, considered vital part of our life, is no doubt victim of the fast-moving modern world. *Dodo Gallery* was created to solve this problem. By letting each and every person go through three stages of interactive experience, the project aims to remind the user of family, urging him/her to take action and spend time to what is meant to value most.

## About
*Dodo Gallery* is a collaborated graduation project of six undergraduates from two departments of National Taipei University of Technology:
* Department of Interaction Design
* Department of Computer Science and Information Technology

The project was initiated in September 2019 and is expected to end in June 2021.
### Our Team
Our team name is [Dodo Cafe](https://github.com/DodoCafe).
#### Department of Interaction Design
* [106ac2016 王品筑](https://github.com/kai85559)
* 106ac1023 林秀靜
* 106ac2007 林恩雅

#### Department of Computer Science and Information Technology
* [106590040 温致綱](https://github.com/gougon)
* [106590048 陳風平](https://github.com/phogbinh)
* [106590026 高楷杰](https://github.com/mdvv85009)
* 106590018 廖彥澤 (Contract)

### Collaboration Story
Currently N/A.

### Interactive Experiences
Our main presentation method is to use the projection screen to project 3 pictures, just like a gallery.
* **First picture**<br>
When user walk close to the picture, the cellphone will start ring. Then user can pick up the cellphone and listen to the phonograph.  When the phonograph finished, the picture enter standby screen.
* **Second picture**<br>
User can use walking device(pressure sensor/macky macky) to moving for 15 seconds. After 15 seconds, the picture shows slogan and moving speed decrease to 0 in 5 seconds and enter standby screen.
* **Third picture**<br>
The picture is the foggy window. User can use hand to wipe the window.

### Implementation
Our main platform is PC and other device(pressure detect device, cellphone, infrared detect device, Kinect...).
* **First picture**<br>
We use infrared detect user's entering and inform the cellphone. The cellphone then start ringing. After user pick up the phone and listen to the phonograph, the cellphone will inform the PC. Then, PC goes to the second picture.
* **Second picture**<br>
When the first picture end, the second picture shows up. The picture prompts the user to tread on the walking device(pressure sensor/macky macky) which under his feet. User can move by tread the walking device, then computer will start count for 15 seconds. After 15 seconds, the picture shows slogan and moving speed decrease to 0 in 5 seconds and enter standby screen.
* **Third picture**<br>
When second picture over, the third picture start. We use Kinect to implement touch detection within a certain distance of the projection screen. User use this technic to wipe the fog out.
* **The skill in whole experience**<br>
We use face emotion recognition to dynamically detect user's emotion. Next picture will be affected by user's emotion.

#### Technologies
Currently N/A.

#### Design Patterns
Currently N/A.

### Contributions
Currently N/A.

### Source Codes
* [DodoCafe](https://github.com/DodoCafe/DodoCafe)
* [DodoCafePluginTest](https://github.com/DodoCafe/DodoCafePluginTest)
* [Raspberry Pi TCP Infrared Motion Detection](https://github.com/DodoCafe/raspberry-pi-tcp-infrared-motion-detection)