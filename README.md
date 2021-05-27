# raspberrypi-Pet-Detection-Twilio

TensorFlow MobileNet-SSD 모델을 사용하여 문 근처에 있는지 감지합니다. 
이미지에서 "내부"영역과 "외부"영역의 두 영역을 정의하여 한 지역에서 5 개 이상의 연속 프레임 동안 애완 동물이 감지되면 스크립트는 Twilio를 사용하여 내 휴대폰에 문자 메시지를 보냅니다.

# 실행 과정
1. Pet Detection 파일 다운로드
2. 파일 수정
3. 파일 실행

https://github.com/Ahn-MinHyun/raspberrypi-Object-Detection
프로젝트를 이어 진행한 프로젝트 입니다. 

https://golduny.tistory.com/135
블로그를 참고하여 Twilio에 회원가입을 한 후 나온 토큰과 씨드를 이용하여 코드를 작성합니다.

## 1. Pet Detection 파일 다운로드

현재 위치를 옮긴 후
```
cd /home/pi/tensorflow1/models/research/object_detection
```

파일을 다운로드 한다.
```
wget https://raw.githubusercontent.com/Ahn-MinHyun/raspberrypi-Pet-Detection-Twilio/main/Pet_detector.py
```

## 2. 파일 수정

```
sudo vim Pet_detector.py
```

- 65줄을 바꿔줍니다.
- 
![image](https://user-images.githubusercontent.com/78781222/119787323-0d627080-bf0c-11eb-9313-91d0ad3524d1.png)

```
from utils import visualization_utils1 as vis_util
```

- 38줄에 twilio사이트에서 받아온 자신의 정보를 입력한다.

![image](https://user-images.githubusercontent.com/78781222/119782959-bbb7e700-bf07-11eb-9e7c-219cdedd6a7d.png)

- 205줄과 219줄의 원하는 메세지를 입력한다.

![image](https://user-images.githubusercontent.com/78781222/119784868-9926cd80-bf09-11eb-8349-6af883a4b1aa.png)

- Pet_detector의 파일만 사용하는 유틸파일을 만들어 줍니다. 

```
cd /home/pi/tensorflow1/models/research/object_detection/utils/
```

```
cp visualization_utils.py visualization_utils1.py
```

```
sudo vim visualization_utils1.py
```
163줄을 바꿔줍니다.

![image](https://user-images.githubusercontent.com/78781222/119786858-8f9e6500-bf0b-11eb-98d5-5e8d010ec2a5.png)

```
# np.copyto(image, np.array(image_pil))
image = np.copy(np.array(image_pil))
```

## 3. 파일 실행
```
cd .. 
```
```
python3 Pet_detector.py
```
