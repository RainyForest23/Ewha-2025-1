### Q1.  Packet Swiching delay
We consider sending real-time voice from Host A to Host B over a packet-switched network (VoIP). <span style="background:#b1ffff">Host A converts analog voice to a digital 64 kbps bit stream</span> on the fly. Host A then <span style="background:#b1ffff">groups the bits into 56-byte packets</span>. There is one link between Hosts A and B; <span style="background:#b1ffff">its transmission rate is 2 Mbps</span> and <span style="background:#b1ffff">its propagation delay is 10 msec</span>. As soon as Host A gathers a packet, it sends it to Host B. As soon as Host B receives an entire packet, it converts the packet’s bits to an analog signal. How much time elapses from the time a bit is created (from the original analog signal at Host A) until the bit is decoded (as part of the analog signal at Host B)?

#### A1.1 Summary of Q1
- A – voice → B
- analog → digital (64 kbps bit)
- 56 byte packets grouping
- A ← ``link`` → B
	- transmission rate : 2 Mbps
	- propagation delay: 10 ms
- Process (entire time)
  : A gathers packet → send to B → B receives → convert bit to analog

#### A1.2 Theories from Slide
##### A1.2.1 Delay 
> <font color="#bfbfbf"> Week 1-2 p.35-36</font>
- **전송 지연(Transmission Delay)**: R bps 링크에 L비트 패킷을 전송(밀어내는)하는 데 L/R초가 걸림
- **저장 후 전달(Store and Forward)**: 다음 링크로 전송되기 전에 라우터에 전체 패킷이 도착해야 함
- **종단간 지연(End-to-End Delay)**
- **패킷 대기 및 손실(Packet queuing and loss)**: 링크로의 도착 속도(bps)가 일정시간동안 링크의 전송 속도(bps)를 초과하는 경우에, 패킷은 출력 링크로 전송되기를 기다리며 대기한다. 이때, 라우터의 메모리(버퍼)가 가득 차면 패킷이 손실될 수 있음

#### A1.3 Solution
1. **Transmission Delay** (*Packetizaion Delay가 더 구체적일 수도..?*)
	$$ Transmission \ Delay = {L \over R}
	 $$
- $L$ = 56 ``byte`` × 8(``bits/byte``) = 448 ``bits``
- $R$ = 64 ``kbps`` = 64,000 ``bits/sec``
- *데이터가 패킷으로 모이는 시간(gather)* $={448bits \over 64,000 bit/sec}=7ms$ 

- Transmission rate : 2 Mbps → $R$ = 2,000,000 ``bits/sec``
- $Transmission \ Delay={448bits \over 2,000,000bits/sec}=0.00224sec \approx 0.224 ms$

2. **Propagation Delay**: 10 ms

3. End to End Delay
	$$ End\ to \ End \ Delay = \sum {Delay} = (7+0.224+10)ms=17.224 ms $$

#### A1.4 Etc..
Packetization Delay와 Transmission Delay의 차이??

| 개념                  | 정의                       | 기준 속도     |
| ------------------- | ------------------------ | --------- |
| Packetization Delay | 데이터를 패킷 단위로 모으는 데 걸리는 시간 | 데이터 생성 속도 |
| Transmission Delay  | 패킷을 링크에 밀어 넣는 데 걸리는 시간   | 링크 전송 속도  |
1 byte = 8 bits
k = $10^3$
M = $10^6$
1 sec = $10^2$ ms




### Q2. Circuit Switching vs Packet Switching
Suppose users share a <span style="background:#b1ffff">3 Mbps link</span>. Also suppose each user requires <span style="background:#b1ffff">150 kbps</span> when transmitting, but <span style="background:#b1ffff">each user transmits only 10 percent of the time</span>.
1) When circuit switching is used, how many users can be supported?
2) For the remainder of this problem, suppose packet switching is used. Find the probability that a given user is transmitting.
3) Suppose there are 120 users. Find the probability that at any given time, exactly $n$ users are transmitting simultaneously. $Hint$: Use the binomial distribution.)
4) Find the probability that there are 21 or more users transmitting simultaneously.

#### A2.1 Summary of Q2
- User shares 3 Mbps
- 150 kbps
- transmits 10%

1) Circuit Switching : 회선 독점
2) Packet Switching
3) 120명 중 $n$명이 전송 중일 확률 → Binomial Distribution (이항 분포)로 구할 수 있다.

#### A2.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.38-41</font>

네트워크 상에서 host 간 정보를 주고받는 Transmission 방식에는 두가지의 방식이 존재한다.
- Circuit Switching
- Packet Switching

1. **Circuit Switching**
- 하나의 회선을 할당받아 데이터 교환
- 한번 연결하면 회선 전체를 독점
- 속도와 성능이 일정
- 회선 분할 방식에 두가지 존재
	- FDM : 할당된 대역폭을 나누어 사용
	  → time(x), frequency(y) 축에서 y축 분할
	- TDM : 할당된 대역폭을 시간단위로 나누어 번갈아가며 사용
	   → time(x), frequency(y) 축에서 x축 분할
- 10%의 활성 확률을 가지고 있는 User의 경우 최대 10명까지 수용가능하다.

1. Packet Switching
- 데이터를 Packet 단위로 쪼개어 전송
- 대역폭이 동적으로 공유되기 때문에 이산확률분포함수에 따라 수용가능인원이 Circuit Switching 방식보다 많아진다.


#### A2.3 Solution
##### A2.3.1) 20명
- Circuit Switching : 사용 여부와 관계없이 각 사용자가 전용 150 kbps를 할당받음
$$Users={entire \ bandwidth \over required \ bandwidth}= {3Mbps \over 150kbps}={3,000 bps \over 150kbps}=20  $$
##### A2.3.2) 10% (0.1)
- Packet Switching 에서, 각 사용자는 10%의 시간 동안만 전송
   = 한 사용자가 임의의 순간에 전송 중일 확률 = 10%

##### A2.3.3) 풀이 과정 참고
- 전체 User : 120명
- $p=0.1$(전송 중일 확률)
- $1-p=0.9$(전송 중이지 않을 확률)
$$ P(n) = \binom{120}{n} (0.1)^n (0.9)^{120-n} $$

##### A2.3.4) 약 0.27%
- 21명 이상이 전송 중일 확률 $P(X \geq 21)=1-P(X \leq 20)$
- 이항 분포 공식을 활용한다면,
$$
P(X\geq 21) = 1 - \sum_{k=0}^{20} \binom{120}{k} (0.1)^k (0.9)^{120-k} \approx0.0027=0.27 \%
$$


#### A2.4 Etc..
- +) 이항분포 vs 정규분포 → $n$이 충분히 커지면 정규분포로도 계산할 수 있지 않을까?
	- 이항분포 : 이산확률분포
	  → 확률변수 $X$는 시행 횟수인 $n$이 충분히 커지면, 근사적으로 **정규분포**를 따른다.
	- 정규분포 : 연속확률분포
	  → $N(np,npq)=N(np,(\sqrt{npq})^2)$
	- 이 상황에서 정규분포 공식을 활용하여 근사치를 구해본다면,
	$$P(X \geq 21) ≈ 1 - P(X \leq 20) = 1 - P\left(Z \leq \frac{20.5 - 12}{3.28} \right)= 1 - P(Z \leq 2.59) ≈ 1 - 0.9952 = 0.0048 =0.48\% $$

	→ 즉 0.48%.. 인데, 왜 2배정도 차이가 나는 걸까?

### Q3. End-to-End Packet Delay
Consider a packet of length $L$ that begins at end system $A$ and <span style="background:#b1ffff">travels over three links to a destination end system</span>. These<span style="background:#b1ffff"> three links are connected by two packet switches</span>. Let $d_i,s_i$, and $R_i$ denote the length, propagation speed, and the transmission rate of link $I$, for $i=1, 2, 3$. The packet switch delays each packet by $d_{proc}$. <span style="background:#b1ffff">Assuming no queueing delays</span>, in terms of $d_i, s_i, R_i, (i = 1, 2, 3)$, and $L$, <span style="background:#b1ffff">what is the total end-to-end delay for the packet</span>? Suppose now the packet is 1,500 bytes, the propagation speed on <span style="background:#b1ffff">all three links is 2.5 x 108 m/s</span>, <span style="background:#b1ffff">the transmission rates of all three links are 2 Mbps</span>, <span style="background:#b1ffff">the packet switch processing delay is 3 ms</span>,<span style="background:#b1ffff"> the length of the first link is 5,000 km</span>, <span style="background:#b1ffff">the length of the second link is 4,000 km</span>, and <span style="background:#b1ffff">the length of the last link is 1,000 km</span>. For these values, what is the end-to-end delay?

#### A3.1 Summary of Q3
- Length of Packets : $L$
- 3 Links are connected with 2 packet switch
- each link $i$ has $s_i$(propagation velocity) and $R_i$(transmission velosity)
- Processing Delay of each packet switches : $d_{proc}$
- there is no queueing delay
#### A3.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.34-35</font>
- **전송 지연(Transmission Delay)**: $R$ bps 링크에 $L$ bits 패킷을 밀어넣는데 $L\over R$초 소요
- **종단간 지연(End-to-End Delay)**: $\sum {Delay}$
- **전파 지연(Propagation Delay)**: $length \ of \ link \over {v}$
- **처리 지연(Processing Delay)**: Packet 헤더를 검사하고, 경로를 결정하는데 소요되는 시간
#### A3.3 Solution

##### A3.3.1 Fomula
- End to End delay는 일반적으로 모든 delay의 합으로 계산된다. 
- 패킷 크기가 $L$인 각 링크에 걸리는 시간은 아래와 같다. 
  (\*단 switch가 2개이므로, processing delay는 2번 발생한다.)
$$ {\sum_{i=3}^3}\Big( {L \over R_i}+{d_i \over s_i} \Big) +2d_{proc} $$

##### A3.3.2 64ms
- $L = 1500byte = 1500 \times 8 = 12,000 bits$
- $s_i=2.5\times 10^8 m/s$
- $R_i=2Mbps=2 \times 10^6bps$
- $d_1=5,000,000m$
- $d_2=4,000,000m$
- $d_3=1,000,000m$
- $d_{proc}=3ms$

$$ {\sum_{i=3}^3}\Big( {L \over R_i}+{d_i \over s_i} \Big) +2d_{proc} = \Big( {L \over R_1}+{d_1 \over s_1} \Big) +2d_{proc}+\Big( {L \over R_2}+{d_2 \over s_2} \Big) +2d_{proc}+\Big( {L \over R_3}+{d_3 \over s_3} \Big) +2d_{proc} \newline = (6 \times 3 ) +20+16+4+ (6 \times 3 )=64 $$

#### A3.4 Etc..



### Q4. Router Buffer & Little's Formula
Consider a router buffer preceding an outbound link. In this problem, you will use $Little’s \ formula$, a famous formula from queueing theory. Let $N$ <span style="background:#b1ffff">denote the average number of packets in the buffer plus the packet being transmitted</span>. Let $a$<span style="background:#b1ffff"> denote the rate of packets arriving at the link</span>. Let $d$ <span style="background:#b1ffff">denote the average total delay</span> (i.e., the queueing delay plus the transmission delay) experienced by a packet. $Little’s formula$ is $N = a \times d$. Suppose that on average, <span style="background:#d3f8b6">the buffer contains 10 packets</span>, and <span style="background:#d3f8b6">the average packet queueing delay is 10 ms</span>. The link’s transmission rate is <span style="background:#d3f8b6">100 packets/sec</span>. Using $Little’s formula$, what is the average packet arrival rate, assuming there is no packet loss?
#### 4.1 Summary of Q4
- $N$: 시스템 내 평균 패킷 수 (버퍼에 있는 패킷 + 전송중인 패킷)
  → 10개
- $a$: 패킷 도착 정도
  → 구해야 할 것
- $d$: 평균 전체 지연 시간 (Queueing delay + Transmission delay)
  → Queuing delay : 10 ms = 0.01 sec
  → Transmission rate : 0.01 sec
  → $d=Queueing \ delay + transmission \ delay = 0.01+0.01=0.02$
- $Little’s \ formula$
  $$ N=a \times d $$



#### A4.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.36</font>
#### A4.3 Solution 
$$N=a \cdot d \Longrightarrow a = {N \over d} = {10 \over 0.02} = 500 \ packet/sec $$




### Q5. Bandwidth-Delay Product (BDP)
Suppose two hosts, A and B, are <span style="background:#b1ffff">separated by 20,000 km</span> and are connected by a direct link of $R$ = 2 Mbps. Suppose the propagation speed over the link is $2.5 \times 10^8$ m/s.
1) Calculate the bandwidth-delay product, ($R \times d_{prop}$).
2) Consider sending a file of<span style="background:#b1ffff"> 800,000 bits</span> from Host A to Host B. Suppose the file is sent continuously as one large message. What is the maximum number of bits that will be in the link at any given time?
3) Provide an interpretation of the bandwidth-delay product.
4) What is the width (in meters) of a bit in the link? Is it longer than a football field?
5) Derive a general expression for <span style="background:#b1ffff">the width of a bit</span> in terms of the propagation speed $s$, the transmission rate $R$, and the length of the link $m$.
#### A5.1 Summary of Q5
- 두 호스트는 20,000 km 떨어져 있고, 2 Mbps(2,000,000 bps) 링크로 연결됨
- Propagation speed = $2.5 \times 10^8$ ms
- $BDP = R \times d_{prop}$
	- $R$ : Bandwidh

#### A5.2 Theories from Slide
> <font color="#bfbfbf"> Week 3-2 p.38-41</font>
- Bandwidth-Delay Product, BDP(대역폭 지연 곱) : 링크에서 이동중인 최대 데이터 양
	-  파일을 연속적으로 전송할 떄, 어느 시점에서든 링크에 있는 최대 비트 수는 BDP에 의해 제한된다.
	- 데이터를 전송했는데, Reciever가 아직 받지 않은 상태인 즉, 링크에서 이동할 수 있는(in flight) 데이터의 최대 양
	- Protocol (i.e. TCP)에서 최대 처리량을 위해 필요한 buffer 크기
- Bit Width : 1 bit 전송에 걸리는 시간 동안 비트가 이동하는 거리

#### A5.3 Solution
##### A5.3.1) 160,000 bits
$$ d_{prop}={distance \over v_{prop} } = {20,000 km \over (2.5 \times 10^8)m/s}=80 \ ms$$
$$BDP = R \times d_{prop}=2Mbps \times 80 ms = {(2\times 10^6) bits \times 00.8 sec \over sec }= 16\times 10^4 \ bits$$
##### A5.3.2) (*A5.3.3 참고*) 160,000 bits
- 파일을 연속적으로 전송할 떄, 어느 시점에서든 링크에 있는 최대 비트 수는 BDP에 의해 제한된다.
  → 160,000 bits
##### A5.3.3) 풀이 과정 참고
- Bandwidth-Delay Product, BDP(대역폭 지연 곱) : 링크에서 이동중인 최대 데이터 양
	-  파일을 연속적으로 전송할 떄, 어느 시점에서든 링크에 있는 최대 비트 수는 BDP에 의해 제한된다.
	- 데이터를 전송했는데, Reciever가 아직 받지 않은 상태인 즉, 링크에서 이동할 수 있는(in flight) 데이터의 최대 양
	- Protocol (i.e. TCP)에서 최대 처리량을 위해 필요한 buffer 크기
##### A5.3.4) Larger than Football field ($125 \geq 100$)
- **Bit Width** : 1 bit 전송에 걸리는 시간 동안 비트가 이동하는 거리
- Propagation speed : $2.5 \times 10^8$ m/s
- Transmission rate($R$) : 2 Mbps = $2 \times 10^8$ bps
$$Bit \ Width = {2.5 \times 10^8 \over 2 \times 10^8}=125  \ meters$$


##### A5.3.5) 풀이 과정 참고
$$ Bit \ Width(meter) = {{{meter \over sec} \over  {bit \over sec}}}={meter \over 1 bit}={Propagation \ Speed \over Transmission \ Rate }={s \over R}$$


#### A5.4 Etc..
- Propagation Speed (전파 속도) (m/s)
  : 전기 신호가 전선, 광섬유 등을 통해 이동하는 속도
- Transmission Rate (전송 속도) (bps)
  : 데이터 전송 속도 “초당 몇 비트를 링크에 밀어넣을 수 있는가?”
- Bit Width (meters)
  : 전송 중인(in Flight) 한 비트가 차지하는 공간 상의 길이
  : 하나의 비트가 링크 위에서 실제로 차지하는 길이
$$ Bit \ Width(meter) = {{{meter \over sec} \over  {bit \over sec}}}={meter \over 1 bit}={Propagation \ Speed \over Transmission \ Rate }$$
- 길이가 $m$ 인 링크 위에 존재하는 bit 개수, 링크 상의 비트 수
$$ m\times {1\over Bit \ Width(meter) } = {R \over s}\times m $$


### Q6. Message Segmentation
 In modern packet-switched networks, including the Internet, the source host segments long, application-layer messages (for example, an image or a music file into smaller packets and sends the packets into the network. The receiver then reassembles the packets back into the original message. We refer to this process as $message segmentation$. The figure below illustrates the end-to-end transport of a message with and without message segmentation. Consider a message that is $8 \cdot 10^6$ bits long that is to be sent from source to destination in the figure. Suppose each link in the figure is 2 ``Mbps``. Ignore propagation, queuing, and processing delays.
 1) Consider sending the message from source to destination <span style="background:#b1ffff">without message segmentation</span>. How long does it take to move the message from the source host to the first packet switch? Keeping in mind that <span style="background:#b1ffff">each switch uses store-and-forward packet switching</span>, what is the total time to move the message from source host to destination host? 
 2) Now suppose that <span style="background:#b1ffff">the message is segmented into 800 packets</span>, with <span style="background:#b1ffff">each packet being 10,000 bits long</span>. How long does it take to move the first packet from source host to the first switch? When the first packet is being sent from the first switch to the second switch, the second packet is being sent from the source host to the first switch. At what time will the second packet be fully received at the first switch? 
 3) How long does it take to move the file from source host to destination host when message segmentation is used? Compare this result with your answer in part (a) and comment.

#### A6.1 Summary of Q6
- message : $8 \cdot 10^8$ bits 
- transmission rate of each link : 2 Mbps = $2 \cdot 10^6$ bps
- Host  A –(link 1)→ switch –(link 2)→ switch –(link 3)→ Host B
- Store-and-Forward 방식
  : 데이터가 링크에 전송된 후, 첫번째 스위치가 전체 데이터를 다 받아야 다음 스위치로 전송할 수 있다.
- segmented into 800 packets
	- Length of each packet : 10,000 bits


#### A6.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.38-41</font>
-  **저장 후 전달(Store and Forward)**: 다음 링크로 전송되기 전에 라우터에 전체 패킷이 도착해야 함
#### A6.3 Solution
##### A6.3.1) 12 sec
- 각 링크에 전송되는 시간 : 4 ms
$${message \over R}= {8 \cdot10^6 \over 2 \cdot 10^6}=4 \ sec$$
- Store-and-Forward 방식으로 인해, 3개의 링크를 거치며 총 3번의 Delay 발생
  → 4 ms $\times$ 3 = 12 sec

##### A6.3.2) 4.01 sec
- 800개의 Packet 중 첫번째 Packet이 전송되는 시간
  : Transmission Rate 는 “초당 몇 비트를 링크에 밀어넣을 수 있는가?” 이고, 하나의 packet은 10,000 bit로 구성되어 있기 때문에, 전송되는 ‘시간’을 구하기 위해서는 $t={d \over v}$ 를 생각하면 된다!
  
$${Length_{packet} \over R} = {10,000 \ bit  \over 8,000,000 }=0.005 \ sec = 5 \ ms$$
- Store-and-Forward 방식으로 인해, 3개의 링크를 거치며 총 3번의 Delay 발생
  → 5 ms $\times$ 3 = 15 sec = 첫번째 패킷이 Host B 에 도달하는 시간

- 800개의 packet은 pipeline 구조를 따를 것

| time     | Host A | link 1  | switch             | link 2      | switch         | link 3  | Host B |
| -------- | ------ | ------- | ------------------ | ----------- | -------------- | ------- | ------ |
| 0-5 ms   | p1 전송  | p1 전송 중 | p1 도착              |             |                |         |        |
| 5-10 ms  | p2 전송  | p2 전송 중 | p1 전송<br>p2 도착<br> | p1 전송 중     | p1 도착          |         |        |
| 10-15 ms | p3 전송  | p3 전송 중 | p2 전송<br>p3 도착     | p2 전송 중<br> | p1 전송<br>p2 도착 | p1 전송 중 | p1 도착  |
| 15-20 ms | p4 전송  |         |                    |             | p2 전송          | p2 전송 중 | p2 도착  |
- 즉 다음 패킷이 5ms 간격으로 도착
$$ 총 \ 시간 = 15ms + (799 \times 5 ms)=15+3395=4010ms=4.01sec $$

##### A6.3.3) 풀이 참고

| 방식             | 전송 시간    |
| -------------- | -------- |
| segmentation X | 12 sec   |
| segmentation O | 4.01 sec |


#### A6.4 Etc..



### Q7. 
Consider the following string of ASCII characters that were captured by Wireshark when the browser sent an HTTP GET message (i.e., this is the actual content of an HTTP GET message). The characters <_cr_><_lf_> are carriage return and line-feed characters (that is, the italized character string <_cr_> in the text below represents the single carriage-return character that was contained at that point in the HTTP header). Answer the following questions, indicating where in the HTTP GET message below you find the answer.

> GET /cs453/index.html HTTP/1.1 <_cr_><_lf_>Host: gaia.cs.umass.edu<_cr_><_lf_>
> User-Agent: Mozilla/5.0 (Windows;U; Windows NT 5.1; en-US; rv: 1.7.2)
> Gecko/20040804 Netscape/7.2 (ax) <_cr_><_lf_>Accept:ext/xmI, application/xmI,
> application/×html+xml, text /html;q=0.9, text/plain; q=0.8, image/png, */*; q=0.5
> <_cr_><_If_>Accept-Language: en-us, en; q=0.5<_cr_><_If_>Accept-Encoding: zip,
> deflate<_cr_><_If_>Accept-Charset: ISO-8859-1, utf-8;9=0.7, \*; 9=0. 7<_cr_><_If_>Keep-Alive: 300<_cr_><_If_>Connection: keep-alive<_cr_><_If_><_cr_><_If_>

1) What is the URL of the document requested by the browser?
2) What version of HTTP is the browser running?
3) Does the browser request a non-persistent or a persistent connection?
4) What is the IP address of the host on which the browser is running?
5) What type of browser initiates this message? Why is the browser type needed in an HTTP request message?

#### A7.1 Summary of Q7
#### A7.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.38-41</font>
#### A7.3 Solution
##### A7.3.1) ``http://gaia.cs.umass.edu/cs453/index.html``
- ``/cs453/index.html`` : 요청된 경로
- ``Host: gaia.cs.umass.edu`` : 호스트


##### A7.3.2) ``HTTP/1.1``
##### A7.3.3) Browser request persistent connection
- `Connection: keep-alive`: 지속적인 연결 요청
- `Keep-Alive: 300`: 연결을 300초 동안 유지
##### A7.3.4) 확인할 수 없음
- IP 주소 정보는 HTTP 메시지 자체에 포함되지 않으며, 하위 TCP/IP 계층에서 처리됨
##### A7.3.5) Netscape 7.2
- `User-Agent: Mozilla/5.0 (Windows;U; Windows NT 5.1; en-US; rv: 1.7.2) Gecko/20040804 Netscape/7.2 (ax)`
- 브라우저 유형이 필요한 이유
   i. 서버가 클라이언트의 브라우저 유형에 따라 최적화된 콘텐츠를 제공
   ii. 다양한 브라우저가 웹 표준을 다르게 구현하므로 호환성을 확보
#### A7.4 Etc..

### Q8.
 The text below shows the reply sent from the server in response to the HTTP GET message in the question above. Answer the following questions, indicating where in the message below you find the answer.

> HTTP/1.1 200 OK<_cr_><_If_>Date: Tue, 07 Mar 2008
> 12:39:45GMT<_cr_><_If_>Server: Apache/2.0.52 (Fedora)
> <_cr_><_If_>Last-Modified: Sat, 10 Dec2005 18:27:46
> 3GMT<_cr_><_If_>ETag: "526c3-f22-a88a4c80" <_cr_><_If_>Accept-Ranges:
> bytes<_cr_><_If_>Content-Length: 3874<_cr_><_If_>
> Keep-Alive: timeout=max=100 <_cr_><_If_>Connection:
> Keep-Alive<_cr_><_If_>Content-Type: text/html; charset=
> ISO-8859-1<_cr_><_If_><_cr_><_If_><!doctype html public "-//w3c//dtd html
> 4.0transitional//en"><_If_>\<html><_lf_> \<head><_lf_> \<meta http-equiv="Content-Type"
> content="text/html; charset=iso-8859-1"><_lf_> \<meta name="GENERATOR"
> content="Mozilla/4.79 [en] (Windows NT5.0; U) Netscape]"><_lf_>\<title>CMPSCI 453 /
> 591 /NTU-ST550ASpring 2005 homepage\</title><_If_>\</head><_If_> <_much more_
> _document text following here (not shown)_>

1) Was the server able to successfully find the document or not? What time was the document reply provided?
2) When was the document last modified?
3) How many bytes are there in the document being returned?
4) What are the first 5 bytes of the document being returned? Did the server agree to a persistent connection?

#### A8.1 Summary of Q8
#### A8.2 Theories from Slide
> <font color="#bfbfbf"> Week 1-2 p.38-41</font>
#### A8.3 Solution
##### A8.3.1) Successfully find. Tue, 07 Mar 2008 12:39:45GMT
- `HTTP/1.1 200 OK`: 성공적으로 문서를 찾았음을 나타내는 상태 코드
- `Date: Tue, 07 Mar 2008 12:39:45GMT`: 응답 제공 시간
##### A8.3.2) Sat, 10 Dec2005 18:27:46 GMT
- ``Last-Modified: Sat, 10 Dec2005 18:27:46 GMT``
##### A8.3.3) 3,874 byte
- `Content-Length: 3874`
##### A8.3.4) “<!doc”, Agree
-  `<!doctype html public "-//w3c//dtd html 4.0transitional//en">`으로 시작
- `Connection: Keep-Alive`와 `Keep-Alive: timeout=max=100` : 지속 연결 동의

#### A8.4 Etc..