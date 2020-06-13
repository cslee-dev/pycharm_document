# 파이참(Pycharm) 도커(Docker)를 통한 파이썬 인터프리터 설정

 어느 환경에서나 동일한 파이썬 환경을 가지고 싶어 파이참의 도커 기능을 통해 파이썬 인터프리터를 

1. 도커를 설치한다. 

   - 윈도우 :  [docker for Windows설치](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
   - 맥 : [docker for Mac 설치](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)

2. 도커 설치에 필요한 기타 설정 ( Windows OS )

   1. BIOS 가상화 enabled 하기
      1. 인텔 : VT-x 
      2. AMD : SVM
   2. WSL2 설치 
   3. 도커 클라이언트 settings > General 의 tcp 데몬을 활성화 한다. ( 파이참 도커 서비스와 통신할 프로토콜임. )

   

3. 파이썬 이미지를 받아온다.

   ```
   docker pull python:3.7.7
   ```

   

4. 파이참 도커 서비스 생성하기

   1. settings( preference ) > Build, Execution, Deployment > Docker 메뉴로 들어간다.

      ![Docker settings image](.\images\docker_service_setting.jpg)

   2. +버튼을 눌러 도커 서비스를 추가하고 아래와 같이 생성해준다. 이름은 아무렇게 입력해도 상관 없다.

      ![pycharm create docker service](.\images\create_docker_service.jpg)

   3. 맥같은 경우는 docker for mac 항목이 존재하며 해당 항목을 선택후 ok버튼을 누르면 된다.

   

   

   도커 서비스를 성공적으로 생성 했다면.  도커와 파이참을 성공적으로 연결시킨 것이다. 이제 파이참은 도커를 활용할 준비가 되었고 도커를 이용하면 된다. 

   

5. 파이참 도커 인터프리터를 생성하기

   파이참이 도커를 활용해서 인터프리터를 생성하는 것이기 때문에 도커의 룰에 벗어나지 않는다는 점을 명심해야한다. 즉 도커에서 호스트OS(윈도우, 맥)의 프로젝트에 접근해서 파이썬 인터프리터를 활용한다는 것은 해당 디렉토리를 공유하고 있다는 것이다. 

   

     도커에서 호스트OS의 프로젝트 디렉토리를 사용하기 위해서는 공유 설정을 해야한다는 사실을 기억하며 도커 인터프리터를 생성하도록 한다.

   1. settings( preference ) > project: <프로젝트 디렉토리 이름> > Project Interpreter 메뉴로 이동

      ![pycharm project interpreter](.\images\pycarh_project_interpreter.jpg)

   2. 톱니바퀴 버튼을 눌러 Add 버튼을 눌러주고 아래와 같이 설정한다.

      ![create python interpreter](.\images\create_docker_interpreter.jpg)

      - Server : 도커 서버를 의미한다.

      - Image name : 파이썬 도커 이미지를 의미한다.

      - Python interpreter path는 도커 이미지에 존재할 파이썬 경로를 의미한다.

        

   3. path mapping 

      도커 파이썬 인터프리터가 프로젝트 디렉토리인지할 수 있도록 매핑해줘야 한다.

      ![empty path mapping](.\images\empty_path_mapping.jpg)

      위와 같이 (Empty) 상태를 변경해줘야한다. path mappings의 디렉토리 표시를 눌러 추가해준다.

      ![add path mapping](.\images\add_path_mapping.jpg)

      - Local Path : 프로젝트 루트 절대경로이다.
      - Remote Path : 파이참에서 프로젝트디렉토리를 읽기 위해 사용하는 경로이다.

   

   도커 인터프리터가 정상적으로 설치 되었다. 테스트를 해보자.

   

6. 도커 인터프리터 테스트

   1. 파이참 파이썬 콘솔 

      ![test python console](.\images\test.jpg)

      정상적으로 동작하는 모습을 볼 수 있다.

   2. 파이썬 모듈 구동

      파이썬 인터프리터에서 설정한 프로젝트에 study_test.py 스크립트를 생성해 구동해 보도록한다. 코드는 아래와 같이 간단히 프린트 한다.

      ```
      print("hello world!")
      ```

      간단히 만든 스크립트를 실행을 해보도록 하자.

      ![test cript](.\images\run_script.jpg)

      스크립트 실행 결과

      ![result script](.\images\result_script.jpg)





이렇게 성공적으로 도커 이미지를 통해 파이썬 인터프리터를 생성하였다. 

