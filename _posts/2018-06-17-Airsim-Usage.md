---
layout: post
title:  "Airsim 사용법"
date:   2018-06-17 11:58:00 +0900
categories: Airsim
---

## 단축키  
'F1': Keyboard shortcuts  
'F' : FPV View  
'B' : Fly-with-me View  
'/' : Chasing from back view   
'\' : Ground Observer View   
0 : 모든 뷰 ON/OFF  
1 : Dept 윈도우 On/Off   
2 : Segmentation 윈도우 On/Off   
3 : Scene 윈도우 On/Off   
T : Trace Line On/Off   
'Backspace' : Reset   

## AirSim Cookbook  
MitchellSpryn사이트 : http://www.mitchellspryn.com/  

## 명령어
client.confirmConnection();  
client.enableApiControl(True)  
client.reset();  재실행  
client.getCollisionInfo(); 충돌 정보 가져오기  
client.simGetImage(0, cameraTypeMap[cameraType]); AirSim 영상 가져오기  
client.simGetImages([ImageRequest(0, AirSimImageType.DepthPerspective, True, False)]) ; AirSim 영상 가져오기   
client.simPrintLogMessage("Hello", "345", 2)   
client.simGetPose(); 위치 가져오기  
client.simSetPose(Pose(Vector3r(0, 0, 0), AirSimClientBase.toQuaternion(0, 0, 0)), True)   
AirSimClientBase.wait_key('Press any key to set camera-0 gimble to 15-degree pitch')  
client.setCameraOrientation(0, AirSimClientBase.toQuaternion(0.261799, 0, 0)); #radians  
client.getCameraInfo(camera_id); 카메라 정보 가져오기  


#### 차량 모델
client = CarClient() ; 차량 모델 접속  
client.getCarState(); 차량 상태 가져오기  
client.setCarControls(car_controls);  차량 명령  
 - car_controls.throttle = 0.5  
 - car_controls.steering = 0  

#### 드론 모델
client = MultirotorClient() ; 드론 모델 접속  
client.getVelocity(); 드론 속도 가져오기  
client.getPosition(); 드론 위치 가져오기  
client.getMultirotorState(); 드론 상태 정보 가져오기  
client.getLandedState(); 드론 착륙 상태 가져오기  
client.getPitchRollYaw(); 드론 피치,롤,요 정보 가져오기  
client.armDisarm(True); 드론 활성화/비활성화  
client.takeoff(); 이륙 명령  
client.land(); 착륙 명령   
client.hover(); 호버 명령  
client.moveToPosition(initX, initY, initZ, 5); 드론 위치 명령  
client.moveByVelocity(1, -0.67, -0.8, 5); 드론 속도 명령   
client.moveByManual(vx_max = 1E6, vy_max = 1E6, z_min = -1E6, duration = 1E10); 수동 명령
client.moveOnPath([Vector3r(0,-253,z),Vector3r(125,-253,z),Vector3r(125,0,z),Vector3r(0,0,z),Vector3r(0,0,-20)],  
                        12, 120, DrivetrainType.ForwardOnly, YawMode(False,0), 20, 1)  
client.setRCData(rcdata = RCData(pitch = 0.0, throttle = 1.0, is_initialized = True, is_valid = True))


#### Camera Type  
0: "depth": AirSimImageType.DepthVis  
1: "segmentation": AirSimImageType.Segmentation  
2: "seg": AirSimImageType.Segmentation  
3: "scene": AirSimImageType.Scene  
4: "disparity": AirSimImageType.DisparityNormalized  
5: "normals": AirSimImageType.SurfaceNormals  
