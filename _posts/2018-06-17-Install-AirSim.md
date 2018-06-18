---
layout: post
title:  "AirSim 설치 방법"
date:   2018-06-17 11:58:00 +0900
categories: Airsim
---

제가 테스트한 컴퓨터 환경은 아래와 같습니다.  
> Lenovo X1 Carbon : i7-5600U 2.6GHz, RAM 8GB, intel HD5500 (내장형 그래픽) =>약10 fps      
> DELL 7577 : i7-7700HQ 2.8GHz, RAM 16GB, nVidia 1060 (6GB) => 잘 돌아감

# 리눅스 설치 방법 (Ubuntu 16.04 LTS 기준)

### 1. Epic Game 사이트 등록 [(링크)](https://docs.unrealengine.com/latest/INT/Platforms/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/1/index.html)   
먼저, Epic Games 사이트에 등록하고 ID와 PW를 기억해둡니다.   

### 2. Unreal Engine 설치 [(링크)](https://docs.unrealengine.com/latest/INT/Platforms/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/index.html)  
AirSim은 Unreal Engine에서 동작하기 때문에 Unreal Engine을 먼저 설치합니다.  
```
# go to the folder where you clone GitHub projects
git clone -b 4.18 https://github.com/EpicGames/UnrealEngine.git
cd UnrealEngine
./Setup.sh
./GenerateProjectFiles.sh
make ## 1시간 이상 소요됨.
```

### 3. AirSim 설치 [(링크)](https://github.com/Microsoft/AirSim/blob/master/docs/build_linux.md)  
이제 AirSim을 다운로드(git)하고 빌드를 합니다.
```
# go to folder where you clone GitHub projects
git clone https://github.com/Microsoft/AirSim.git
cd AirSim
./setup.sh
./build.sh
```

### 4. Unreal 실행 [(링크)](https://docs.unrealengine.com/latest/INT/Platforms/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/4/index.html)  
`~/UnrealEngine/Engine/Binaries/Linux/$ ./UE4Editor`

### 5. AirSim 실행 [(링크)](https://github.com/Microsoft/AirSim/blob/master/docs/unreal_blocks.md)  
Unreal에서 Blocks 프로젝트를 선택합니다.  
(프로젝트 파일은 `AirSim/Unreal/Environments/Blocks/Blocks.uproject` 입니다.)  
'플레이' 버튼을 선택하면 시뮬레이션이 시작됩니다.   
  

# 윈도우 설치 방법  
**※ AirSim도 MS꺼라 윈도우가 호환성이 좋고 대부분 예제도 윈도우 중심으로 이뤄져 있습니다.**  
Unreal Engine과 AirSim을 빌드해서 사용하기 위해서는 Visual Studio와 cmake 설치가 필요합니다.  
*빌드하지 않고 AirSim만 실행하는 경우는 바이너리 실행파일만 다운받으면 됩니다. ([AirSim 실행파일](https://github.com/Microsoft/AirSim/releases))

### 1. 빌드 환경 준비
   * Visual Studio Community 2017을 설치합니다. [(다운로드 링크)](https://my.visualstudio.com/Downloads?PId=2226)  
     EXE파일을 다운받아 실행하는 경우는 약 4GB의 설치파일이 다운로드 됩니다.  
   * cmake 설치 [(다운로드 링크)](https://cmake.org/download/)  
     : rpclib 서브모듈을 빌드하기 위해 필요하다고 한다. 테스트한 버전은 3.11.3입니다.   
     ※ 반드시 'Add CMake to the system PATH for all users"로 선택한다. 그렇지 않으면 PATH를 별도로 추가해줘야 한다.

### 2. Unreal 설치 [(원문 링크)](https://github.com/Microsoft/AirSim/blob/master/docs/build_windows.md)  
   * Epic game launcher 설치 [(다운로드 링크)](https://www.unrealengine.com/download)
   * Unreal Engine 4.18 설치 (약 4GB 다운로드 필요)  
     ※ 공식적으로 4.18버전을 지원하고, 다른 버전은 테스트가 필요합니다.

### 3. AirSim git Clone하기
   * 윈도우에서 cmd를 입력하여 명령 프롬프트를 열고, 아래 명령을 실행해서 AirSim 파일을 동기화한다.  
     C:\ 에서 아래 명령어를 실행하면 C:\AirSim 폴더가 생성된다. (약 400MB)  
     `git clone https://github.com/Microsoft/AirSim.git`
   * git이 설치되지 않은 경우 git scm을 설치한다. [(git사이트)](https://git-scm.com/)  

### 4. 빌드하기
   * Visual studio x64 Native Tools Command Prompt를 실행한 후,  
     ~AirSim 폴더 경로에서 명령창에 `build.cmd`를 실행해 빌드한다.

> Windows SDK 에러 처리 방법   
  메시지 : error MSB8036: Windows SDK 버전 8.1을(를) 찾을 수 없습니다. 필요한 버전의 Windows SDK를 설치하거나, 솔루션을 마우스 오른쪽 단추로 클릭하고 [솔루션 대상 변경]을 선택하거나 프로젝트 속성 페이지에서 SDK 버전을 변경하세요.   
  해결법1 : AirSim.sln 프로젝트를 열고 솔루션탐색기에서 MavLinkCom의 속성에서 Windows SDK 버전을 8.1이 아닌 다른 버전으로 선택한다.    
  해결법2 : Windows SDK를 다운받아 설치한다. [(링크)](https://developer.microsoft.com/ko-kr/windows/downloads/windows-10-sdk)   

> mavlink_sha256.h 에러 처리 방법  
  메시지 : 데이터가 손실되지 않게 하려면 해당 파일을 유니코드 형식으로 저장하십시오.  
  해결법 : 해당하는 파일을 Visual Studio에서 열어서 다시 저장한다. (UTF-8으로 저장)  
  
> Half.h 에러 처리 방법  
  메시지 : 데이터가 손실되지 않게 하려면 해당 파일을 유니코드 형식으로 저장하십시오.   
  해결법 : Half.h 파일을 열어서 "AS IS" 의 "를 삭제한다. (유니코드 문제 원인) [(링크)](https://github.com/Microsoft/AirSim/issues/76)  

빌드가 완료되면 `AirSim\Unreal\Plugins` 폴더를 Unreal 프로젝트로 옮길 준비가 된것이다.

### 5. 라이브러리 추가 [(원문 링크)](https://github.com/Microsoft/AirSim/blob/master/docs/unreal_custenv.md)
   * 주의) 프로젝트 생성 전에 Unreal 언어 설정을 English로 수정해야 합니다.  
     한글로 설정되어 있는 경우, 프로젝트 이름이 한글로 생성되어 컴파일 과정에서 에러 발생합니다.  
   * 학습(Learn) 탭에서 'Landscape Mountains' 를 찾은 후 프로젝트를 생성한다. (1.4GB 다운로드 필요)
   * Landscape Mountains 프로젝트를 연다. (언리얼 에디터가 실행된다.)      
   * Unreal Editor의 `File menu`에서 `New C++ class`를 클릭하고 기본 옵션으로 두고, 이름도 `MyClass`로 하고 `Create Class`를 눌러 프로젝트를 생성한다.   C++클래스를 만드는 이유는 언리얼 프로젝트를 위해서는 최소 1개 이상의 클래스가 있어야 하기 때문이다.
> VS14 에러가 발생하는 경우는 프로젝트 설정에서 컴파일 환경을 Visual Studio 2017로 선택한다. 프로젝트 세팅>플랫폼>윈도우>Toolchain   

   * AirSim 폴더 내의 `Unreal\Plugins` 폴더를 `LandscapeMountains` 폴더로 복사한다.
     이렇게 하면 Unreal project가 AirSim plugin을 사용할 수 있게 된다.
   * `LandscapeMountains.uproject`를 아래와 같이 수정한다.  
<pre><code>
{
	"FileVersion": 3,
	"EngineAssociation": "4.18",
	"Category": "Samples",
	"Description": "",
	"Modules": [
		{
			"Name": "LandscapeMountains",
			"Type": "Runtime",
			"LoadingPhase": "Default",
			"AdditionalDependencies": [
				"AirSim"
			]
		}
	],
	"TargetPlatforms": [
		"MacNoEditor",
		"WindowsNoEditor"
	],
	"Plugins": [
		{
			"Name": "AirSim",
			"Enabled": true
		}
	]
}
</code></pre>

   * 비주얼 스튜디오와 Unreal Editor를 종료한 후, 프로젝트 폴더의 `LandscapeMountains.uproject` 파일에서 마우스 오른쪽 클릭하고 `Generate Visual Studio Project Files`를 실행한다.
     이 단계는 모든 플러그인과 소스파일을 체크하고 `.sln` 파일을 생성한다.  
> Tip: If the Generate Visual Studio Project Files option is missing you may need to reboot your machine for the Unreal Shell extensions to take effect. If it is still missing then open the LandscapeMountains.uproject in the Unreal Editor and select Refresh Visual Studio Project from the File menu.  

![Generate .sln file](https://github.com/Microsoft/AirSim/raw/master/docs/images/regen_sln.png)

   * 비주얼 스튜디오에서 `LandscapeMountains.sln` 을 열고 "DebugGame Editor", "Win64" 빌드 환경으로 선택한다.  
   * F5를 눌러 실행한다.  
