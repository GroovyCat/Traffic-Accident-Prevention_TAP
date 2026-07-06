# 🚗 TAP - Traffic Accident Prevention System

> YOLO와 차선 인식을 활용한 교통사고 방지 시스템

<br>

## 📌 목차

- [프로젝트 개요](#-프로젝트-개요)
- [팀 구성 및 역할](#-팀-구성-및-역할)
- [기술 스택](#-기술-스택)
- [주요 기능](#-주요-기능)
- [시스템 아키텍처](#-시스템-아키텍처)
- [실험 결과](#-실험-결과)
- [실행 결과](#-실행-결과)
- [결론](#-결론)
- [논문](#-논문)
- [설치 및 실행 방법](#-설치-및-실행-방법)

<br>

## 📖 프로젝트 개요

<table>
  <thead>
    <tr>
      <th width="120" align="center">항목</th>
      <th>내용</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">프로젝트명</td>
      <td>TAP (Traffic Accident Prevention System)</td>
    </tr>
    <tr>
      <td align="center">개발 기간</td>
      <td>4학년 1학기</td>
    </tr>
    <tr>
      <td align="center">팀명</td>
      <td>허둥지둥</td>
    </tr>
    <tr>
      <td align="center">개발 인원</td>
      <td>3명</td>
    </tr>
    <tr>
      <td align="center">소속</td>
      <td>선문대학교 컴퓨터공학부</td>
    </tr>
    <tr>
      <td align="center">프로젝트 소개</td>
      <td>
        교통사고의 약 90%는 운전자의 부주의로 발생한다.<br>
        운전 중 운전자의 시야는 전방 일부에 집중되어 구석진 곳의 장애물을 인지하기 어려우며, 기존 블랙박스는 사고 예방보다 기록 용도에 그친다.<br>
        본 시스템은 YOLO 기반 장애물·보행자 인식과 가상 차선을 활용한 차선 인식을 결합하여, 충돌 위험 시 경고음을 출력하는 교통사고 방지 시스템이다.
      </td>
    </tr>
  </tbody>
</table>

<br>

## 👥 팀 구성 및 역할

<table>
  <thead>
    <tr>
      <th width="80" style="text-align:center">이름</th>
      <th width="100" style="text-align:center">역할</th>
      <th width="300" style="text-align:center">작업</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">채윤재</td>
      <td align="center">팀장</td>
      <td>프로젝트 설계, 보행자 인식 개선</td>
    </tr>
    <tr>
      <td align="center">박문영</td>
      <td align="center">팀원</td>
      <td>보행자 인식 - YOLOv3, YOLOv3-tiny</td>
    </tr>
    <tr>
      <td align="center">문태수</td>
      <td align="center">팀원</td>
      <td>차선 인식 - OpenCV</td>
    </tr>
  </tbody>
</table>

<br>

## 🛠 기술 스택

| 분류 | 기술 |
|------|------|
| 개발환경 | ![Windows](https://img.shields.io/badge/Windows_10-0078D6?style=flat-square&logo=windows&logoColor=white) ![VSCode](https://img.shields.io/badge/VSCode-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white) ![VisualStudio](https://img.shields.io/badge/Visual_Studio_2019-5C2D91?style=flat-square&logo=visualstudio&logoColor=white) |
| 언어 | ![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white) |
| AI | ![YOLO](https://img.shields.io/badge/YOLOv3-FF9E0F?style=flat-square&logoColor=white) ![YOLO](https://img.shields.io/badge/YOLOv3--tiny-FF6B35?style=flat-square&logoColor=white) |
| 영상처리 | ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white) |
| 하드웨어 | ![Camera](https://img.shields.io/badge/USB_WebCam-212121?style=flat-square&logoColor=white) |

<br>

## ✨ 주요 기능

### 1. 장애물 및 보행자 인식 (ODF)

YOLO v3-tiny 기반 딥러닝 객체 인식으로 전방의 장애물 및 보행자를 실시간으로 탐지한다.

- 이미지 데이터셋 확보 → 라벨링(labelImg) → 학습 가중치 생성 → 실시간 인식
- Bounding Box 좌표와 객체 클래스 확률을 예측·분류
- 모바일·소형 기기 환경을 고려해 YOLOv3-tiny 모델 채택

### 2. 차선 인식 (LDF)

가상 차선을 활용한 차선 인식으로 기존 차선 환경에 영향을 받지 않는 인식 방법을 제시한다.

```
ROI 지정
  → HSV 필터링 (흰색·노란색 차선 구분)
  → 노이즈 제거 + 이진화
  → Canny Edge 외곽선 검출
  → Hough Transform
  → 가상 차선 적용 → 차선 인식 완료
```

<img src="https://user-images.githubusercontent.com/15725909/105295961-16a99c80-5bfd-11eb-8047-1af6c59b7923.png" width="600"/>

### 3. 충돌 위험 경고음 출력

장애물·보행자의 Bounding Box가 가상 차선의 삼각형 영역에 진입하면 경고음을 출력한다.

- ODF + LDF 두 기능의 인식 영역 겹침 감지
- 충돌 위험 사전 경고로 운전자 부주의에 의한 사고 방지

<br>

## 🏗 시스템 아키텍처

<img src="https://user-images.githubusercontent.com/15725909/105293516-794e6880-5bfc-11eb-9c80-07d00ffbcd6b.jpg" width="600"/>

```
카메라 장치 (USB WebCam)
  → YOLO (ODF): 장애물·보행자 Bounding Box 인식
  → 차선 인식 (LDF): HSV 필터링 + Canny Edge + 가상 차선
  → 충돌 위험 판정 (Bounding Box ∩ 가상 차선 삼각형 영역)
  → 경고음 출력 시스템
```

<br>

## 📊 실험 결과

### YOLO v3 Average Precision

| 클래스 | Average Precision | MAP |
|---|---|---|
| person[1] | 99.62% | 95.18% |
| person[2] | 99.58% | |
| person[3] | 99.33% | |
| person[4] | 95.93% | |
| person[5] | 81.46% | |

### YOLO v3-tiny Average Precision

| 클래스 | Average Precision | MAP |
|---|---|---|
| person[1] | 71.69% | 64.37% |
| person[2] | 71.21% | |
| person[3] | 70.13% | |
| person[4] | 55.16% | |
| person[5] | 53.69% | |

> YOLOv3-tiny를 채택한 이유: 소형 기기 환경에서도 적당한 성능을 낼 수 있도록 경량화 모델을 선택하였으며, 차량 보조 장치 특성상 v3-tiny 모델이 적합하다고 판단하였다.

<br>

## 🖥 실행 결과

### 개발 환경

<img src="https://user-images.githubusercontent.com/15725909/105297600-7acc6080-5bfd-11eb-984b-5cd52a1cc7a0.png" width="600"/>

### 최종 인터페이스

<img src="https://user-images.githubusercontent.com/15725909/105293765-88351b00-5bfc-11eb-9400-97a821417c2a.png" width="600"/>

<br>

## 🔚 결론

- 장애물 및 보행자 인식과 차선 인식을 결합해 운전자 부주의로 인한 사고를 방지하는 충돌 위험 경고 시스템을 개발하였다.
- 향후 시스템을 개선해 실제 차량 탑재 또는 스마트폰 애플리케이션으로 제공될 것으로 예상된다.

<br>

## 📄 논문

[📎 논문 보기](docs/TAP.pdf)

<br>

## 🚀 설치 및 실행 방법

### 1. 레포 클론

```bash
git clone https://github.com/GroovyCat/Traffic-Accident-Prevention_TAP.git
cd Traffic-Accident-Prevention_TAP
```

### 2. 의존성 설치

- Visual Studio 2019 설치
- OpenCV 설치 및 환경변수 설정
- YOLO v3-tiny 가중치 파일 다운로드

### 3. 빌드 및 실행

Visual Studio 2019에서 프로젝트 열기 후 빌드 및 실행

```
USB 카메라 연결 후 실행 시 전방 인식 시작
```
