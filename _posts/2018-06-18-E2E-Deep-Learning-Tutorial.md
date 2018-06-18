---
layout: post
title:  "End-to-End Deep Learning Tutorial"
date:   2018-06-18 12:58:00
categories: Tutorial
---

이 페이지는 아래 사이트의 Tutorial을 위한 설명서이다.  
https://github.com/Microsoft/AutonomousDrivingCookbook/tree/master/AirSimE2EDeepLearning

## AirSim 설치  
윈도우의 경우 Binary파일을 다운로드하여 압축을 푼다.  
Build Package : https://airsimtutorialdataset.blob.core.windows.net/e2edl/AD_Cookbook_AirSim.7z  

## AirSim 실행
'AD_Cookbook_Start_AirSim.ps1' 에서 우측클릭하여 'Powershell에서 실행' 을 클릭한다.  
Power Shell에서 Scenario: 가 나타나면 'landscape'를 입력하면 Airsim이 실행된다.  
또는  
PowerShell에서 다음과 같이 실행해도 된다.  
.\AD_Cookbook_Start_AirSim.ps1 landscape
  
## GitHub 소스코드 가져오기
git 명령어를 이용하거나 gitHub Desktop을 이용해 소스코드를 가져온다.  
(소스코드 주소 : https://github.com/Microsoft/AutonomousDrivingCookbook.git)  

## 데이터 세트 준비하기 
1. 데이터 세트(3.2GB)를 다운로드한다. (주소 : https://aka.ms/AirSimTutorialDataset)  
2. data_raw 폴더, data_cooked 폴더, model 폴더를 새로 만든다. 이 폴더는 스크립트에서 데이터를 가져오고 저장하는 경로로 사용된다.  
   ex. AirSimE2EDeepLearning/data_cooked, ~/data_raw, ~/model  
3. 데이터 세트 압축을 해제하여 data_raw 폴더에 넣는다.  
   ex. data_raw/normal_1, ~/normal_2,...

## Jupyter Notebook 실행
Jupyter Notebook을 실행하고 git 소스코드 폴더를 선택한다.  

## STEP1. Date Exploration and Preparation
: 데이터를 확인하고 .h5 파일로 변환함.  
- RAW_DATA_DIR과 COOKED_DATA_DIR 폴더 경로를 확인하고 경로가 다른 경우, 위에서 만든 폴더 경로를 지정한다.  
- DATA_FOLDERS도 확인한다.  
- 순서대로 실행한다. 마지막 단계에서 ~/data_cooked 폴더에 .h5 파일이 생성되는 것을 확인한다.  

## STEP2. Train Model
: Dataset으로부터 모델을 훈련시킴.  
- COOKED_DATA_DIR 폴더와 MODEL_OUTPUT_DIR 폴더 확인하고 다른 경우 해당 폴더를 지정한다.  
- 훈련시간은 1060 기준 약 5시간 소요.  

## STEP3. Test Model
: 훈련된 모델을 이용해 Airsim에서 자율 주행을 테스트함.  
- model폴더에서 Loss 크기가 가장 작은 모델파일(.h5)을 골라 MODEL_PATH로 설정한다.  
- 메모리 관련 오류가 발생할 경우는 MODEL_PATH 다음 줄에 아래와 같은 코드를 추가한다.
`import tensorflow as tf`  
`config = tf.ConfigProto()`    
`config.gpu_options.allow_growth = True`    
`sess = tf.Session(config=config)`  
- 다음 스크립트를 순서대로 실행하면 AirSim이 동작하면서 자율 주행을 볼 수 있다.  
