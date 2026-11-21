# 생성형 AI 사용 기록

이 과제에서 생성형 AI(ChatGPT, Claude, Gemini, Copilot 등)를 쓸 때마다 아래 표에 **한 줄씩** 추가할 것.

- **날짜**: 사용한 날 (YYYY-MM-DD)
- **도구**: 사용한 AI 도구 이름
- **관련 기능**: F1–F5 중 무엇 (Git 사용법·README 등 기능과 무관하면 `기타`)
- **무엇을 물었나**: 질문·요청 내용을 구체적으로 (예: "pygame 에서 사각형 충돌을 확인하는 함수")
- **결과를 어떻게 반영/수정했나**: 받은 답을 그대로 썼는지, 어디를 고쳤는지, 쓰지 않았다면 왜인지

AI 를 전혀 쓰지 않았다면 표를 지우고 "이 과제에서 생성형 AI 를 사용하지 않았습니다." 라고 적을 것.
아래 `예시` 줄은 지우고 제출할 것.

| 날짜 | 도구 | 관련 기능 | 무엇을 물었나 | 결과를 어떻게 반영/수정했나 |
|---|---|---|---|---|
| 예시 2026-01-01 | ChatGPT | F1 | 방향키를 누르고 있는 동안 계속 움직이게 하는 방법 | `pygame.key.get_pressed()` 사용법만 참고, 화면 경계 처리는 직접 작성 |

| 2026-11-18 | ChatGPT | F1 | 방향키를 누르고 있는 동안 플레이어를 움직이고 화면 밖으로 나가지 않게 하는 방법 | `keys[pygame.K_LEFT]`, `keys[pygame.K_RIGHT]`로 입력을 확인하고 `self.rect.x`를 변경하는 코드와 `left`, `right`로 화면 경계를 제한하는 코드를 참고 |
| 2026-11-18 | ChatGPT | F2 | `shoot()`의 `return None`은 무슨 뜻이고, 총알의 시작 좌표는 왜 `centerx`와 `top`을 쓰는지 | `None`의 의미를 확인하고, 비행기의 위쪽 가운데에서 총알이 출발하도록 `return Bullet(self.rect.centerx, self.rect.top)`을 작성하는 방법을 참고 |
| 2026-11-18 | ChatGPT | F2 | 스페이스 키로 만든 총알을 왜 두 그룹에 넣는지 | `shoot()`를 한 번 호출한 뒤 같은 총알을 `self.bullets`에 넣어 이동·충돌을 처리하고 `self.all_sprites`에 넣어 화면에 그리는 방식을 참고 |
| 2026-11-21 | ChatGPT | F2 | `and not self.game_over`와 `if bullet is not None`이 모두 필요한지 | 게임 오버 중 발사를 막는 조건은 유지하고, 완성된 `shoot()`가 항상 총알을 반환하므로 `None` 검사는 생략할 수 있음을 확인 |
| 2026-11-21 | ChatGPT | F2 | 게임 시작 후 스페이스를 두 번째 눌렀을 때 발사가 제대로 되지 않는 이유 | 두 번째 스페이스부터 `shoot()`가 호출된다는 점과 `Bullet.update()`에서 `self.rect.y`를 줄여 총알을 위로 이동시키는 방법을 참고 |
| 2026-11-19 | ChatGPT | F3 | 총알과 적이 충돌하면 둘 다 사라지는 코드가 있는지 | `pygame.sprite.groupcollide(self.enemies, self.bullets, True, True)`의 두 `True`가 각각 충돌한 적과 총알을 제거한다는 점을 확인 |
| 2026-11-19 | ChatGPT | F3 | 적을 맞혔을 때 `+= 1`로 점수를 올려도 되는지, 어떤 점수가 증가하는지 | `SCORE_PER_ENEMY`는 적 한 마리의 배점이고 `self.score`가 누적 점수임을 확인. 맞힌 적 수만큼 반영하려고 `len(killed_enemies) * SCORE_PER_ENEMY`를 사용 |
| 2026-11-20 | ChatGPT | F3 | 현재 점수를 화면 왼쪽 위에 `SCORE: 120` 형태로 표시하는 방법 | 기존 `LIVES` 표시 코드를 참고해 `self.draw_text(f"SCORE: {self.score}", self.font, WHITE, topleft=(10, 10))`으로 현재 점수를 표시 |
| 2026-11-20 | ChatGPT | F4 | 플레이어가 적과 충돌했을 때 `-= len(...)` 대신 `-= 1`을 써도 되는지 | `spritecollide()`로 닿은 적을 제거하고, `if damaged_by_enemies:`일 때만 `self.lives -= 1`을 실행하도록 작성. 여러 적이 동시에 닿아도 해당 프레임에는 생명 1개만 감소하도록 선택 |
| 2026-11-19 | ChatGPT | F4 | 적이 화면 아래로 지나가거나 생명이 0 이하가 됐을 때 어떻게 처리하는지 | 화면을 벗어난 적마다 `enemy.kill()`과 생명 감소를 처리하고, `for`문 밖에서 `if self.lives <= 0:`으로 `self.end_game()`을 호출하는 위치를 확인 |
| 2026-11-21 | ChatGPT | F4·F5 | 게임 오버 화면 가운데에 이번 점수, 최고 점수, 재시작 안내를 표시하는 방법 | `draw_game_over()`에서 `self.draw_text()`를 사용하고, 같은 가로 중심 좌표에 서로 다른 세로 좌표를 주어 네 줄을 배치하는 코드를 참고 |
| 2026-11-21 | ChatGPT | F5 | `HIGHSCORE_FILE`로 최고 점수를 읽는 코드가 왜 틀렸고, `try`와 `except` 없이 어떻게 작성하는지 | 파일 경로와 파일 내용의 차이를 확인. `os.path.isfile()`로 파일을 검사하고 `read().strip()`과 `isdecimal()`로 내용을 확인한 뒤 정수로 변환하는 방식을 참고 |
| 2026-11-19 | ChatGPT | F5 | 점수 파일이 없을 때 `return 0`이 실행되는지 | `if score.isdecimal():`을 파일 존재 검사 안에 넣고, 마지막 `return 0`을 바깥에 두어 파일이 없거나 내용이 잘못된 경우를 처리 |
| 2026-11-21 | ChatGPT | F5 | 이번 점수가 기존 최고 점수보다 높을 때 기록을 갱신하고 저장하는 방법 | `end_game()`에서 두 점수를 비교해 `self.high_score`를 갱신하고, `save_high_score()`에서 `"w"` 모드와 `file.write(str(score))`로 저장하는 코드를 참고 |
| 2026-11-21 | ChatGPT | F5 | 게임 오버 상태에서 R 키로 새 판을 시작하는 방법 | `event.key == pygame.K_r and self.game_over` 조건에서 `self.reset()`을 호출해 점수와 생명을 초기화하는 방법을 참고 |
| 2026-11-21 | ChatGPT | 실행 환경 | `pygame` 설치가 실패하고 `main.py`를 찾을 수 없다는 오류를 해결하는 방법 | 프로젝트 폴더로 이동하고 Python 3.12 환경에 Pygame을 설치한 뒤 `py -3.12 main.py`로 실행. 실행 기록에서 Python 3.12.10과 Pygame 2.6.1 사용을 확인 |
| 2026-11-21 | ChatGPT | F2·F5 디버깅 | 게임 시작 시 `AttributeError: 'pygame.event.Event' object has no attribute 'key'`가 발생하는 이유 | 키보드 외의 이벤트도 들어온다는 점을 확인하고, `pygame.KEYDOWN` 조건 안에서만 ESC·스페이스·R 키를 검사하도록 들여쓰기를 점검 |
| 2026-11-21 | ChatGPT | F4·F5 디버깅 | 게임 오버 직후 창이 닫히고 `NameError: name 'cx' is not defined`가 발생하는 이유 | 오류가 발생한 `draw_game_over()` 안에서 `cx = WIDTH // 2`와 `cy = HEIGHT // 2`를 먼저 정의하도록 수정 방법을 확인 |

커밋 날짜와 시간이 안 맞는 경우는, 제가 브랜치 커밋을 안하고 이틀간 과제를 진행하다, 19일부터 다 지우고 다다시 코드를 업데이트 시켰기 떄문입니다. 그리고 인공지능으로 각종 함수와, 처리 방법을 물어보았지만, 원리를 이해하고, 코드를 작성하였습니다. 그리고 main 마지막 커밋의 경우 수정한 코드를 일괄 다운 받고, vs 코드에서 여러번 수정을 가하다보니, 특정한 피쳐의 값이 고쳐졌다곤 말하기 그래서 F0로 처리하였으며, 에러 커밋 메세지도 모호합니다. 
