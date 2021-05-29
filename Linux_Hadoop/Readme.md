# 1. 주요 질문 :  2020년, 전세계인들의 행복은 무엇과 가장 관련이 있을까?
### 1.1 데이터 분석 질문 선정 이유:

2021년, 올해 나의 모토는 행복이다. 그래서인지 문득 '사람들은 무엇에 행복할까?'라는 궁금증이 생겼다.
또한 2020년, 코로나 전염병 덕에 전 세계가 심하게 앓았다. 이런 상황에서 사람들의 행복에 영향을 주는 요인은 무엇일까 궁금했다.  
<br>
<br>
<br>
# 2.  데이터
### 2.1 데이터 출처

https://www.kaggle.com/mathurinache/world-happiness-report 

<br>

__참조 문헌 (References)__ :
Helliwell, John F., Richard Layard, Jeffrey Sachs, and Jan-Emmanuel De Neve, eds. 2020. World Happiness Report 2020. New York: Sustainable Development Solutions Network
<br>
<br>
### 2.2 데이터와 데이터정보
**업로드 날짜** : 2020년 7월 1일
**크기** : 약 17KB
**데이터 조사 대상국** : 대한민국 포함 153개국

[2020.csv](https://github.com/suntoday123/Portfolio/files/6564526/2020.csv)

<br>

### 2.3 데이터 분석에 사용된 변수(컬럼)들

**독립변수** :  
**GDP per capita** : 나라의 국내 총생산을 총 인구로 나눈 값, 경제 지표 중 하나  
**Social support** : 위기나 힘든 상황 속에서 기댈만한 사람들이 있는가에 대한 자각  
**Healthy Life Expectancy** : 건강 기대수명 ( WHO 기준 )  
**Freedom to make life choices** : 외부 압력 없는 선택의 자유  
**Generosity** : 베푸는 삶(선한 행위)에 대한 미덕  
**Corruption Perception** : 나라의 부정부패에 대한 인식  

<br>

**종속변수** :  
**Ladder_score** : 행복지수

<br>

### 2.4 파일 위치

/home/scott/project/  

원할한 데이터 분석을 위해 /home/scott에 project 폴더를 생성하고 해당 폴더에 데이터 압축을 풀었다.  
$ cd
$ mkdir project
$ mv ./archive.zip ./project/archive.zip
$ unzip archive.zip
$ rm -rf archive.zip

<br>
<br>
<br>

# 3. 테이블 생성과 데이터로드

### 3.1 테이블생성

drop  table  happiness;

 

 create table happiness

 ( Country varchar(60),

Regional varchar(60),

Ladder_score varchar(60),

Stadard_error_of_ladder varchar(60),

upperwhisker varchar(60),

lowerwhisker varchar(60),

Logged_GDP_per_capita varchar(60),

Social_support varchar(60),

Healthy_life_expectancy varchar(60),

Freedom varchar(60),

Genorosity varchar(60),

Perceptions_of_corruption varchar(60),

Ladder_score_Dystopia varchar(60),

Explained_by_Log_GDP_per_capita varchar(60),

Explained_by_Social_support varchar(60),

Explained_by_Healthy_life_expectancy varchar(60),

Explained_by_Freedom varchar(60),

Explained_by_Genorosity varchar(60),

Explained_by_Perceptions_of_corruption varchar(60),

Dystopi_residual varchar(60)

 ) ;

<br>

### 3.2 데이터 로드

LOAD DATA LOCAL INFILE '/home/scott/project/2020.csv'

REPLACE

INTO TABLE  orcl.happiness

fields TERMINATED BY ','

ENCLOSED BY '"'

LINES TERMINATED BY '\n'
IGNORE 1 LINES    
(Country, Regional, Ladder_score, Stadard_error_of_ladder, upperwhisker, lowerwhisker, Logged_GDP_per_capita, Social_support, Healthy_life_expectancy, Freedom, Genorosity, Perceptions_of_corruption, Ladder_score_Dystopia,  Explained_by_Log_GDP_per_capita, Explained_by_Social_support, Explained_by_Healthy_life_expectancy, Explained_by_Freedom, Explained_by_Genorosity, Explained_by_Perceptions_of_corruption, Dystopi_residual
);

<br>
<br>
<br>

# 4. 데이터 시각화
[data_visualization_code.txt](https://github.com/suntoday123/Portfolio/files/6564560/data_visualization_code.txt)

<br>
<br>
<br>

# 5. 시각화 설명

53개국 기준의 데이터를 바탕으로 행복에 영향을 주는 요인들( 독립변수 )과 행복지수( 종속변수 ) 사이의 상관관계를 보다 명확하게 파악하기 위하여 데이터 시각화를 산점도(scatter plot)로 하였다.

<br>

											

![image](https://user-images.githubusercontent.com/79921374/120068019-8521ce00-c0b9-11eb-8f07-3e84d82495b3.png)

<br>

산점도는 그래프의 점들이 한데 뭉쳐 있을수록 상관관계가 높은 것으로 분석된다.

분석된 그래프들을 보면 대부분의 그래프의 점들이 여기저기 흩어진 모습을 보이지만, Social support와 Happiness의 관계, Healthy life expectancy와 Happiness의 관계를 나타낸 그래프의 점들이 서로 뭉쳐서 오른쪽 위로 향한 대각선을 그리며 나아가는 것을 볼 수 있다.
이로써 그 두 독립변수들이 행복과 비교적 강한 양의 상관관계를 보인다고 결론지을 수 있다.

다시 해석해보면, 다른 어떤 요인들보다도 **힘든 상황 속에서 의존을 할 만한 사람이 주위에 존재하는지를 강하게 느낄수록** , 자신이 **건강한 삶을 살 날이 많이 남아 있다고 강하게 느낄수록** 사람들의 **행복지수가 높아지는 것과 관계가 있다**는 것을 알 수 있다.
그리고 미세하지만, Social support와 Happiness의 산점도가 Healthy life expectancy와 Happiness의 산점도보다 강한 상관관계를 보이는 것을 알 수 있다.

GDP나 사회적 불안이 생각보다 행복과 상관관계가 높지 않다는 점이 흥미롭다. 

요즘 코로나 영향인지 우울증을 겪는 사람이 점점 많아지고 있다고 하는데 자신의 주변의 힘든 일을 겪고 있는 사람들이 있다면 그 사람들에게 한 줄기의 힘이 되어주는 건 어떨까 하는 생각이 든다.

#
### 번외:

**한국의 행복지수 순위는?**

<br>

**153개국 기준**  
![image](https://user-images.githubusercontent.com/79921374/120068161-3cb6e000-c0ba-11eb-9eb9-f8448ee317f0.png)

<br>

**동아시아 6개국 기준**

<br>

![image](https://user-images.githubusercontent.com/79921374/120068175-51937380-c0ba-11eb-9095-36f75a5527c6.png)
