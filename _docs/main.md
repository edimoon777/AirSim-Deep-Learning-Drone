딥러닝을 연구 및 스터디를 위한 AirSim 활용 방법에 대한 설명입니다.

# AirSim 소개

# AirSim 설치
## 윈도우
## 리눅스

# AirSim 실행
## 단축키
-
-

# AirSim 연동
## Python 함수

# 딥러닝 예제
1. Autonomous Driving Cookbook (_by Microsoft Deep Learning and Robotics Garage Chapter_)  
 1-1. End-to-End Learning (시너리 : Landscape)  
 1-2. Distributed Deep Reinforced Learning (시너리 : Neighborhood)  

2. Reinforced Learning with AirSim (_by Microsoft Ashish Kapoor_)  
CNTK 라이브러리를 이용한 강화학습 예제입니다.  
https://github.com/Microsoft/AirSim/blob/master/docs/reinforcement_learning.md   

**2-1. RL with Car**         
      Neighborhood 시너리에서 자동차를 이용해 충돌을 회피하며 도로 주행을 하는 예제입니다.  
      딥러닝 모델은 6가지 액션을 출력합니다.  
     - action 0 : 정지  
     - action 1 : 스티어링 = 0  
     - action 2 : 스티어링 = 0.5    
     - action 3 : 스티어링 = -0.5  
     - action 4 : 스티어링 = 0.25  
     - action n : 스티어링 = -0.25  

**2-2. RL with Quadrotor**  
      Landscape 시너리에서 쿼드콥터를 이용해서 송전선과 일정한 거리를 유지하며 비행하는 예제입니다.  
      딥러닝 모델은 7가지 액션을 출력합니다.  
      - action 0 : 정지(호버)  
      - action 1 : 전진비행 (quad_offset = 1,0,0)  
      - action 2 : 우측비행 (quad_offset = 0,1,0)  
      - action 3 : 상승비행 (quad_offset = 0,0,1)  
      - action 4 : 후진비행 (quad_offset = -1,0,0)  
      - action 5 : 좌측비행 (quad_offset = 0,-1,0)  
      - action 6 : 하강비행 (quad_offset = 0,0,-1)  

>    Reward 함수는 송전선과의 거리로 계산합니다.  
>    송전선과 송전탑 시너리는 별도 추가해야 합니다. (확인 중)          

3. Simple collision avoidance (_by Simon Levy and WLU team_)

