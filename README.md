# I. Introduction

<br />

## 1) 농구의 포지션 이란? 스탯?

- 포지션

![position](https://static1.squarespace.com/static/561a6270e4b0cbb5768713d9/t/575ec9db2b8ddeb3fba7d478/1465829885170/Basketball+Positions)<br />

모든 NBA 선수들은 플레이하는 역할에 따른 '포지션'이라는 라벨을 가지고 있다.<br />
 전통적인 포지션은 다음과 같다<br />
  * **포인트 가드(PG)** - 팀의 **사령탑** 역할을 하며 보통 팀에서 가장 **전술적 이해**가 좋은 선수가 맡는다. 
  * **슈팅 가드(SG)** - **3PT** 등 장거리에서 슛을 하여 점수를 얻는 것을 주역할로 한다.
  * **스몰 포워드(SF)** - 점수를 얻는 것을 주된 역할로 한다. 외곽 슛, 속공 및 리바운드 싸움에도 참여할 수 있는 **올라운드 능력**이 요구됨.
  * **파워 포워드(PF)** - 코트 골밑에서 수비, 득점을 주요 역할로 하고 **리바운드**와 **골밑에서의 몸싸움 및 득점 능력** 등 파워풀한 플레이가 요구됨.
  * **센터(C)** - 골밑 중앙에서 활동하는 포지션. 공격에서는 **골밑슛**을 책임지고 수비에서는 가장  **페인트존을 책임지며** 상대의 슛을 블로킹으로 차단하는 역할까지 한다.<br />

- 스탯

![position](https://github.com/DSS5NBA/NBA_position_clustering/blob/master/tiled_image.jpg?raw=true)<br />

- 왼쪽 위부터 **리바운드**, **3점슛**, **블로킹**, **스틸**

리바운드 : 슈팅이 성공하지 못하고 **튕겨 나왔을 때** 잡는 것  
3점슛 : **24피트** 밖에서 던지는 슈팅  
블로킹 : 상대가 슛한 공을 수비가 반칙이 아닌 선에서 **쳐내는 것**  
스틸 : 상대가 가지고 있는 공을 반칙이 아닌 선에서 **가로채는 것**

   **이 밖에도 득점, 어시스트, 슛 성공율, 파울, 자유투 등 다양한 스탯들이 존재**

## 2) Motivation

하지만 오늘날의 게임 방식은 크게 달라졌다. 선수들의 **장거리 슛 성공률**이 높아짐에 따라 팀들의 3점 활용이 늘었고, 그에 따라 3점 슛을 방어하기 위해 바스켓에서 더 멀리 수비라인을 넓혀갔다. 이에 따라 수비라인 간격이 벌어지며 다른 플레이어가 3점 슛 라인 안쪽에서 활약할 수 있는 공간이 훨씬 넓어졌다. 이전에는 주로 3점 슛을 던지는 포지션이 **가드**였다면 현재는 모든 포지션에서 **3점슛의 점유율이 증가**하였다.<br />
 
![position](https://cdn-images-1.medium.com/max/800/1*V2oTbyr5gBcmEr_qAxEliw.jpeg)<br />


이 분석은 현대 농구의 플레이 스타일이 전통적인 방법으로 나눈 5개의 포지션 구분을 무너뜨렸다 생각하여 시작하게 되었다. 우리가 선택한 이 주제는 **전통적인 포지션 분류를 재정의** 하며 선수의 플레이 스타일에 따른 포지션의 재정의, 선수의 구분 그리고 그에 따른 **인사이트 발견을 통해 심도있는 선수분석**을 목적으로 한다.<br />

## 3) 데이터 수집 및 전처리

### - 데이터 출처

 * NBA.com
 * NBAminer.com
 * Basketball-reference
 * ESPN.com
 * Elias Sports Bureau
 * Spotrac.com  
 
### - 데이터 전처리
####  *이상치의 발생 및 처리
![position](http://cfile4.uf.tistory.com/image/2491B8335980818825F66C)
<br />
 
- 위의 그림에서 보다시피 **출전 경기가 적고, 출장시간이 적은 선수**들은 비율 스탯 등이 이상치로 나타날 수 있다. **ex)슛 성공율 100%, 0% 나타남**  
 이런 이상치를 제거하기 위해 **출전 경기 30경기 이상, 경기당 평균 출전시간 10분 이상**의 선수만 선택하여 진행하였다.
 
  각종 논문 및 리포트에서도 클러스터 분석 등에 총 한시즌 출전 시간 500분 이상, 30경기 이상 출전,   
  평균 출전시간 10분 이상 등을 기준으로 하여 사용한 것을 볼 때 위의 기준이 **사용 가능**하다는 것을 알 수 있다.

#### *30게임 이상, 평균출전시간 10분 이상인 선수 추출

#### *변수 정리

col = [**Basic stats**
 : Games, Min, Pts, Reb, Ast .......  
**Clutch Time stats**
 : Total Points, FG% Diff, 3FG Diff .......  
**Advanced stats**
 : Total Plus/Minus, Ts%, Triple Doubles .......   
**Nasty stats**
 : Ejections, Blocks Against, Defensive 3Secs .......  
**Shot Distances**
 : Less than 8ft. %, Back Court Shots %, Avg. Shot Dis.(ft.) .......  
**Shot types**
 : Dunks, Jump Shot %, Assisted FGM %,  .......  
**Shot zones**
 : Above the Break 3-Usage, Right Corner 3-Usage, Restriced Area % .......  
**Assist Details**
 : Assted FG%, Avg. Assisted Shot Distance, Assisted Jump Shot %.......  
**Turnover Details**
 : Lost Ball TO PG, Bad Pass TO PG, Traveling PG.......  
**Foul Details**
 : Off.Fouls Drawn, Shooting Fouls Committed, Lost Ball Fouls.......  
**Four Point & And One**
 : Four Point Plays, And One, Extra Free Throw % .......]
 
 - 이번 분석에서는 총 **152개의 변수에서 실제 NBA 기록의 중요도 및 중복되는 부분을 감안하여 90개의 변수를 사용하여 분석**하였다.  
90개의 경우 농구 기록의 범위를 살펴볼 때 많은 것으로 여겨질 수 있지만,  
다른 논문에서 변수 각각이 설명할 수 있는 범위를 넓히기 위하여 **총 80개의 변수를 사용하였던 예**를 볼 때, **분류 정확도**를 높이기 위하여 90개의 변수를 사용하는 것은 무리가 없다고 가정하고 진행하였다.

<br />
<br />
<br />

# 2. Model setup
1) Classification 모델 선택
* (1) K-means(K-means++)
* (2) Hierarchical Clustering
* (3) EM Clustering
* (4) 가장 결과가 좋은 것? K-means++
2)  클러스터 분석
![position](https://github.com/DSS5NBA/NBA_position_clustering/blob/master/cluster_by_stats_all.png?raw=true)
클러스터에 높은 값을 가진 feature 순위를 매겨 중요속성을 골라내었고, 선수의 플레이스타일을 정의하여 클러스터에 새롭게 라벨링을 해주었다.
* Classic big : 골밑에서의 **득점, 공격 및 수비 리바운드**와 **블록**에 능한 선수 #0
* Aggressive big : **공격 리바운드와 블록, 득점력**이 강한 선수  # 7
* Non-scoring Big : **리바운드와 블록에 강점**이 있지만 득점력이 약한 선수  #8
* Midrange Stopper : **필드골 득점력과 리바운드** 및 **블록샷 등 수비**에 강점이 있는 선수 #3
* Balanced wing scorer : **측면 공격, 3점슛, 패스를 받아 넣는 필드골**에 강점이 있는 선수 #6
* Ball Handler : 돌파 등을 통해서 **본인이 만들어서 득점을 하며 2차 어시스트**에 강점이 있는 선수 #4
* Long shooter : **3점 슛 득점력이 가장 뛰어난** 선수 #1
* All-Round Player : **득점, 어시스트, 리바운드, 3점 슛 성공률**등 여러 스탯에 강점이 있는 선수 #5
* Defensive passer : **어시스트와 스틸에 강점**이 있고 **수비적**인 성향이 강한 선수 #2
* Commander : **어시스트를 주력**으로 하는 **득점력**을 겸비한 **플레이메이커** #9

<br />
<br />
<br />

# 3. Apply basketball analysis by clustering data

## 농구 흐름에 따른 1998-2017 포지션 변화 추세 분석 <br />  
### -- 전체 기간, 전체 클러스터
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/1.png?raw=true)  
#### 1. Balanced wing scorer , Long shooter는 증가의 추세를 가지며  
#### 2. Midrange stopper는 감소의 추세를 가진다.
#### 3. 하지만 나머지 포지션 같은 경우에는 시즌별 편차가 있어서 시대별 흐름에 따라 이를 더 자세히 검토하도록 하겠다.
- 1990 ~ 1999 : 센터의 시대(4대 센터)
- 2000 ~ 2009 : 슈팅가드의 전성시대
- 2010 ~ 2017 : 스몰볼 시대

(출처 : http://www.rookie.co.kr/news/articleView.html?idxno=6126)


## -- 1996 ~ 2017 추세
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/3.png?raw=true)  
 #### 위에서 확인한 바와 같이,  Defensive passer, Long shooter,  Midrange stopper는 전체 연도별 흐름에서 일정한 추세를 가지고 있는 것을 알 수 있었다. 이는 점점 90년대에는 센터 위주의 농구 였지만 점점 가드 위주의 농구로 전환됨에 따라 이런 추세를 띈 것으로 보인다.  


## -- 1999년 이전 추세
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/4.png?raw=true)

#### 센터의 시대가 끝나감에 따라서  Aggressive big의 감소추세가 나타나며, Defensive passer가 증가추세가 나타난다.  


## -- 1999 ~ 2009년 추세
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/5.png?raw=true) 
#### 슈팅가드의 시대가 시작됨에 따라, shooter와 관련된 포지션의 증가를 확인할 수 있다.  


## -- 2010년 이후 추세
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/6.png?raw=true) 
#### 스몰볼의 흐름에 따라서  Long shooter, Ball Handler등의 증가를 확인 할 수 있었다.  
#### 위에서 조사한 것은 연도별 선형관계가 있는 증가와 감소만을 확인할 수 있으므로 각 포지션별의 상관관계에 대해서 살펴보도록 하겠다.

<br />
<br />
<br />

# 각 포지션끼리의 상관관계 
### 전체 시즌에 대한 상관관계
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/7.png?raw=true) 

### 1999년도 까지의 상관관계
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/8.png?raw=true) 

### 1999-2009년도의 상관관계
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/9.png?raw=true) 

### 2009년도 이후의 상관관계
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/10.png?raw=true) 
#### 모든 상관관계 값을 받아들이기 보다는, p_value값을 구해서 상관관계에 대한 검증을 해보도록 하겠다.

<br />
<br />

# p_value값을 구하기
### p_value값이 0.05미만인 것들의 표
![position](https://github.com/gogoj5896/3_teamproject_nba_player_clustering/blob/master/image_file/11.png?raw=true) 

<br />

### 전체시즌의 상관관계에서 나눠서 살펴보면,
<시대별 농구 흐름>
- 1990 ~ 1999 : 센터의 시대(4대 센터)(센터 위주의 농구로, 빠른 공격보다는 지공을 위주로 공격을 하는 팀이 많았다.)
- 2000 ~ 2009 : 슈팅가드의 전성시대(슈팅가드 들이 본인이 직접 득점을 하는 식으로 공격을 마무리 짓는 팀이 많았다.)
- 2010 ~ 2017 : 스몰볼 시대(스몰볼은 라인업 사이즈를 작게 함으로써, 공격속도 등을 빠르게 가져가는 농구를 의미한다.)


<시대별 흐름에 따른 포지션 분석>
- 포지션별 이동이 가능하며 음의 관계,

 Balanced wing scorer, Midrange Stopper<br />
 Midrange Stopper, Long shooter<br />
<br />

- 포지션별 이동이 가능하나 양의관계

 Defensive passer, Long shooter<br />
 Commander, Long shooter<br />
<br />	

- 포지션별 이동이 불가능하나 음의관계

 Defensive passer, Ball Handler<br />
 Defensive passer, Midrange Stopper<br />
 Ball Handler, Classic big<br />
 Long shooter, Classic big<br />
 Non-scoring Big, Long shooter<br />
 Defensive passer,  Non-scoring Big<br />


<br />
1. 포지션별 이동이 가능하며 음의 관계를 갖는 것은, 서로가 대체 관계를 갖는 것으로 예상되며,
<br />
2. 포지션별 이동이 가능하나 양의관계를 갖거나 포지션별 이동이 불가능하나 음의관계를 갖는 것은,
   다른 요인(농구 전략의 변화)등으로 인해 같이 증가되는 것으로 예상된다.

<br />

3점을 많이 던지는 2000년 대부터는 Long shooter 및 Midrange Stopper들이 꾸준히 증가함을 회귀선 등을 통해 알 수 있었는데, 그에 따라서 3점슛보다 가까운 거리에서 던지는 Midrange Stopper는 감소하고 있음을 알 수 있다.

<br />

포지션별 이동이 불가능하나 음의관계를 갖는 것 중에서는 Long shooter와 Non-scoring Big,Classic big 등이 있는데,
이는 기존 센터 위주의 농구에서 벗어나서 슈터 및 3점위주의 농구로의 전환되었음을 의미한다.

<br />
<br />
<br />

# 4. Conclusion & further research
### Conclusion

- **K-Means 클러스터링**을 이용하여 NBA Position에 대해 기존의 5가지의 분류와는 다른 **새로운 10가지 포지션으로의 분류**를 시행함

- **새롭게 정의한 포지션** 별 년도별 흐름 파악 및 포지션별 관계 

### further research
- 수비에 관한 구체적인 기록들이 클러스터링 부분에 많이 반영되지 않아 향후 **수비 관련 지표들에 대해 더 추가하여 반영할 필요**가 있음

- **2차 스탯 및 플레이오프 스탯** 등을 반영할 수 있는 더 정교한 모델 및 클러스터링 작업과 추가적 데이터 확보

<br />
<br />
<br />

# 5. References

1. A new perspective on positions in baskerball players using cluster analysis
http://www.sloansportsconference.com/wp-content/uploads/2012/02/44-Lutz_cluster_analysis_NBA.pdf

2. Modern NBA player positions - using Unsupervised clustering to uncover Functional Roles in Basketball도 참고)
https://medium.com/hanman/the-evolution-of-nba-player-positions-using-unsupervised-clustering-to-uncover-functional-roles-a1d07089935c

3. A New Perspective On Positions In Basketball Players Using Cluster Analysis
http://www.academia.edu/28430572/A_New_Perspective_On_Positions_In_Basketball_Players_Using_Cluster_Analysis

4. NBA.com Player, Combination, Team stats
5. NBAminer Player stats
6. http:// Basketball-reference.com
<br />



[김기욱](https://github.com/mikoms911), [변치웅](https://github.com/overgroove), [신상훈](https://github.com/s132048), [하태준](https://github.com/gogoj5896)
