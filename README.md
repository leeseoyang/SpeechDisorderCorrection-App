# 🗣️ Speech Disorder Correction App (PyQt5 기반)

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![PyQt5](https://img.shields.io/badge/PyQt5-41CD52?style=flat&logo=qt&logoColor=white)
![SpeechRecognition](https://img.shields.io/badge/Speech_Recognition-FFAA00?style=flat)
![OfflineApp](https://img.shields.io/badge/Offline-Application-green)

이 프로젝트는 **음성 인식 + TTS + Altino 로봇 연동**을 통해  
**발음 재활 훈련**을 돕기 위한 **오프라인 음성 보정 지원 애플리케이션**입니다.

---

## 🎯 주요 기능

- 🎤 실시간 음성 인식 (SpeechRecognition)
- 🧠 음성 비교 → 정답 여부 판별
- 🗣️ 음성 피드백 (TTS로 음성 출력)
- 💾 로그 저장 기능 (정답/오답 통계)

---

## 🖥️ 실행 환경

| 항목       | 설명                                      |
|------------|-------------------------------------------|
| OS         | Windows 10 이상                           |
| 언어       | Python 3.8 이상                           |
| GUI        | PyQt5                                     |
| 음성인식   | SpeechRecognition + Google Web API 사용   |
| TTS        | pyttsx3 또는 gTTS                         |   |

---

## ▶️ 실행 방법

```bash
# 1. 가상환경 생성 (선택)
python -m venv venv
source venv/Scripts/activate  # Windows 기준

# 2. 필요 패키지 설치
pip install -r requirements.txt

# 3. 실행
python main.py
````

---

## 📁 프로젝트 구조

```
SpeechDisorderCorrection-App/
├── main.py                       # 앱 실행 진입점
├── speech_module.py             # 음성 인식 및 평가
├── ui/
│   └── main_window.ui           # PyQt Designer UI
├── images/
│   ├── banner.jpg
│   └── demo.jpg
├── requirements.txt             # 필요 라이브러리 목록
└── README.md
```

---

## 🔍 MainActivity 실행 흐름 설명 (Android)

`MainActivity.java`는 이 앱의 핵심 로직을 담당하며, 다음과 같은 흐름으로 동작합니다:

### 📌 실행 구조 요약

1. **앱 초기화**
   - 권한 확인 (`RECORD_AUDIO`)
   - UI 구성 요소 초기화: 텍스트뷰, 버튼 등
   - `SpeechRecognizer` 인스턴스 생성 및 리스너 등록

2. **음성 인식 시작**
   - `시작 버튼` 클릭 시 `startSpeechRecognition()` 호출
   - `RecognizerIntent`를 통해 한국어 음성 인식 시작

3. **음성 인식 결과 처리**
   - 사용자의 발화 결과를 `onResults()`에서 수신
   - 가장 유사한 결과 텍스트를 `TextView`에 출력
   - `compareResults()`를 통해 타겟 문장과 비교

4. **발음 정확도 계산**
   - `calculateEditDistance()`를 이용해 레벤슈타인 거리 기반 유사도 계산
   - 일치율(%)을 계산하여 토스트로 사용자에게 피드백 제공

5. **Firebase에 결과 저장**
   - 현재 날짜 기준으로 `user123/learning_data/yyyy-MM-dd`에 정확도 업로드
   - 성공/실패 여부에 따라 사용자에게 메시지 출력

---

### 🧠 흐름도

```

\[버튼 클릭]
↓
음성 입력 → RecognizerIntent 실행
↓
결과 수신 (onResults)
↓
정답 문장과 비교 (Edit Distance)
↓
정확도 계산 (%)
↓
Firebase에 저장 + 토스트 메시지 출력

```

---

### 🔧 핵심 함수 설명

| 함수명 | 역할 |
|--------|------|
| `startSpeechRecognition()` | 음성 인식 시작 |
| `onResults()` | 인식 결과 수신 |
| `calculateEditDistance()` | 문자열 유사도 계산 |
| `calculateSimilarity()` | 정확도(%) 계산 |
| `saveLearningData()` | Firebase DB에 결과 저장 |
| `compareResults()` | 전체 흐름 통합 |

---

### 🛠 사용 기술 스택

- Android SDK (Java)
- Android SpeechRecognizer API
- Firebase Realtime Database
- 레벤슈타인 거리 기반 정확도 계산

---

이 구조는 **음성 재활 훈련 앱**에서 사용자 발음의 정확도를 실시간으로 확인하고  
피드백을 제공하며 학습 이력을 클라우드에 저장하는 데 최적화된 구조입니다.
```

---


## 🛠 사용 기술 스택

* Python 3.8
* PyQt5
* SpeechRecognition
* pyttsx3 (또는 gTTS)

---

## 📜 라이선스

이 프로젝트는 [MIT License](https://opensource.org/licenses/MIT)를 따릅니다.


---

> ⭐️ 이 프로젝트가 도움이 되셨다면 상단 오른쪽 Star를 눌러주세요!
