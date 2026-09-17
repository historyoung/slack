# Google Calendar 일정 등록 가이드

Slack에서 Google Calendar와 연동하여 일정을 관리하고, 다량의 일정을 한 번에 등록하는 방법을 정리한 문서입니다.

## 1. Slack에 Google Calendar 앱 연동

1. Slack 앱 디렉터리(https://slack.com/apps)에서 "Google Calendar" 검색
2. "추가(Add to Slack)" 클릭 후 Google 계정 로그인·권한 승인
3. 연동이 완료되면 Google Calendar 봇이 DM으로 나타납니다.

연동 후에는 매일 오전 그날의 일정을 Slack DM으로 받아볼 수 있고, 새 회의 초대나 일정 변경 알림도 받을 수 있습니다.

## 2. `/gcal` 슬래시 명령어로 일정 추가

- `/gcal create` — 제목, 날짜·시간, 참석자, 설명을 입력하는 팝업이 뜨고 저장하면 Google Calendar에 바로 등록됩니다.
- 대화 메시지를 일정으로 만들려면: 해당 메시지 오른쪽 `⋯`(더보기) → "이벤트 만들기(Create an event)" 선택
- `/gcal today` — 오늘 일정 보기
- `/gcal help` — 전체 명령어 목록
- `/gcal connect` / `/gcal disconnect` — 계정 연결·해제

> 봇 이름은 워크스페이스에 따라 다를 수 있으니, 설치 후 `/gcal help`를 먼저 실행해 실제 사용 가능한 명령을 확인하세요.

## 3. 다량의 일정 한꺼번에 등록하기

`/gcal create`는 한 번에 하나씩만 만들 수 있어 대량 등록에는 적합하지 않습니다. 여러 개를 한꺼번에 등록하려면 Google Calendar 쪽 도구를 사용하는 것이 효율적입니다.

### 3-1. CSV 파일 가져오기 (일회성 대량 등록에 적합)

1. Google Calendar 웹 → 설정 → "가져오기/내보내기(Import & export)"
2. 아래 헤더로 일정을 정리한 CSV를 업로드하면 한 번에 등록됩니다.

```
Subject, Start Date, Start Time, End Date, End Time, All Day Event, Description, Location, Private
```

- 날짜 형식: `MM/DD/YYYY`
- 시간 형식: `HH:MM AM/PM` (미국식)
- 한국어 오전/오후나 요일 표기를 넣으면 오류가 나므로 위 형식을 그대로 따라야 합니다.
- 엑셀·스프레드시트에서 만든 표를 CSV로 저장해 올리면 됩니다.

### 3-2. 반복(recurrence) 옵션

매주/매월 같은 규칙적인 일정이면 CSV 대신 일정 하나를 만들 때 "반복" 설정으로 처리하는 것이 깔끔합니다.

### 3-3. 프로그래밍으로 자동화 (일정이 자주/많이 생기는 경우)

- Google Calendar API 또는 Apps Script로 배치 등록이 가능합니다. 스프레드시트에 일정 목록을 두고 Apps Script로 반복 삽입하는 방식이 흔합니다.
- Python `google-api-python-client`의 `events().insert()`를 루프로 돌리는 방법도 있습니다.

## 참고

- Slack 봇 자체에는 대량 생성 기능이 없습니다. Google Calendar에 CSV/API로 넣으면, 연동된 Slack에는 자동으로 알림·요약이 반영됩니다.

관련 Slack 스레드: https://siren-t1p9742.slack.com/archives/D0C2N8CEPKN/p1789644045913269?thread_ts=1789640915.560849&cid=D0C2N8CEPKN
