---
title: "Progress Control"
categories:
  - Design
tags:
  - UI&UX
  - Design
toc: true
toc_sticky: true
---

진행률 컨트롤 (Progress control)은 긴 작업을 진행중인 사용자에게 피드백을 제공한다. 진행률 표시가 표시될 때 사용자가 앱을 조작할 수 없다는 의미이며 사용되는 표시기에 따라 대기 시간을 예측할 수 있다는 의미이다.

## 진행률 유형

작업 진행을 표시하기 위해 ProgressBar 또는 ProgressRing 두가지 컨트롤을 사용

- **ProgressBar _확정 (Determinate)_**
  - 작업의 완료율을 표시
  - 기간을 알 수 있는 작업 중 사용
  - 진행률이 사용자의 앱 조작을 차단하지 않음
- **ProgressBar _미확정(Indeterminate)_**
  - 작업이 진행중임을 표시
  - 완료 시간을 알 수 없다는 의미
  - 사용자의 앱 조작을 차단하지 않음
- **PrigressRing _미확정(Indeterminate)_**
  - 작업이 완료될 때까지 사용자의 앱 조작을 차단함

## 각 컨트롤 사용 시기

현재 상태를 표시할 때, 사용할 컨트롤  또는 상태(확정, 미확정)가 항상 명확한 것은 아니다. 떄로는 진행률 컨트롤이 필요하지 않을 정도로 작업이 명확하거나 진행률 컨트롤이 사용되더라도 사용자에게 작업이 진행중임을 설명하는 텍스트가 필요할 수 있다.

### ProgressBar

- **컨트롤에 기간 또는 예측 가능한 종료 시점이 정의되어 있는가?**

  확정 ProgressBar를 사용하고 백분율 또는 값을 적절히 업데이트 한다

- **사용자가 작업의 진행률을 모니터링하지 않고 계속 진행할 수 있는가?**

  ProgressBar를 사용중일 때 작업이 완료될 때까지 사용자가 차단되지 않으며 해당 상태가 완료되기 전에도 다른 방법으로 앱을 계속 사용할 수 있다는것을 의미한다

- **키워드**

  작업에서 다음 키워드가 사용되거나 다음 키워드와 일치하는 진행률 작업과 함께 텍스트를 표시하는 경우 ProgressBar를 사용하는것이 좋다

  - 로드 중...
  - 검색 중
  - 작업 중...

### ProgressRing

- **작업으로 인해 사용자가 계속 대기중인가?**

  작업이 완료될 때까지 모든(또는 상당 부분) 앱 조작을 대기해야하는 경우 ProgressRing을 사용하는것이 더 좋다. ProgressRing 컨트롤은 모달 조작에 사용되며 이는 ProgressRing이 사라질 때까지 사용자가 차단된다는 의미이다.

- **사용자 작업이 완료될 때까지 앱이 대기하는가?**

  이 경우 사용자에 대한 알 수 없는 대기 시간을 나타낸다는 의미이므로 ProgressRing을 사용한다.

- **키워드**

  작업에서 다음 키워드가 사용되거나 다음 키워드와 일치하는 진행률 작업과 함께 텍스트를 표시하는 경우 ProgressRing을 사용하는 것이 좋다.

  - 새로고침 중
  - 로그인 중
  - 연결하는 중

### 진행률 표시가 필요하지 않음

- **어떤 일이 일어나고 있는지 사용자가 알아야 하는가?**

  예를들어 앱이  백그라운드에서 다운로드하고 있을 때 사용자가 다운로드를 시작하지 않았다면 사용자는 이를 알 필요가 없다

- **컴퓨터 작업이 사용자 작업을 차단하지 않으며 사용자와 거의 무관한 백그라운드 작업인가?**

  항상 보일 필요는 없지만 상태를 표시할 필요가 있는 작업을 앱이 수행하고 있을 때는 텍스트를 사용한다

- **사용자에게 작업의 완료 여부만 필요한가?**

  경우에 따라 작업이 완료될 때만 알림을 표시하거나 작업이 완료된 즉시 시각적으로 표시하고 백그라운드에서 완료 작업을 실행하는것이 좋을 때가 있다

## 진행률 컨트롤 모범 사례

- ProgressBar - 확정
  - 작업 기간을 알고 있는 경우
  - 설치, 다운로드, 설정 하는 경우 등에 확정 ProgressBar가 적합

![ProgressBar - 확정 예시 이미지 ](https://docs.microsoft.com/ko-kr/windows/uwp/design/controls-and-patterns/images/pb_determinateexample.png)

- ProgressBar - 미확정
  - 작업 기간을 알 수 없는 경우
  - 미확정 ProgressBar는 가상화된 목록을 채운다
  - 미확정 ProgressBar에서 확정 ProgressBar로의 자연스러운 시각 전환을 만들때 좋다

![ProgressBar - 미확정 예시 이미지](https://docs.microsoft.com/ko-kr/windows/uwp/design/controls-and-patterns/images/pb_indeterminateexample.png)

- ProgressRing - 미확정
  - 사용자의 추가 조작이 중단될 경우
  - 앱이 사용자가 계속 입력하기를 기다릴 때

![ProgressRing - 미확정 예시 이미지](https://docs.microsoft.com/ko-kr/windows/uwp/design/controls-and-patterns/images/pr_indeterminateexample.png)



## 📖 참고 자료

[Windows 개발자 센터: Progress controls](https://docs.microsoft.com/ko-kr/windows/uwp/design/controls-and-patterns/progress-controls)
