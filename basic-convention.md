# CLAUDE.md

## 코드 스타일

- 모든 파일 저장 시 EOF 개행(newline) 필수

---

## 작업 전 필수 확인

파일 수정/생성/설정 변경 전 반드시 먼저 설명할 것:

1. 변경의 목적과 의도
2. 변경될 구체적인 파일과 코드
3. 아키텍처 및 모듈 독립성에 미치는 영향

→ **사용자 승인 후에만 구현 진행**

---

## 행동 가이드라인 Karpathy-Inspired Claude Code Guidelines

1. **코딩 전 사고** — 가정을 명시적으로 드러내고, 불확실하면 질문
2. **단순함 우선** — 요청 범위를 벗어난 기능/추상화/유연성 추가 금지
3. **외과적 변경** — 요청된 것만 수정, 인접 코드 "개선" 금지
4. **목표 중심 실행** — 성공 기준을 정의하고 검증까지 완료

---

## Java & Spring 코딩 컨벤션

### 네이밍 규칙

| 대상 | 규칙 | 비고 |
|---|---|---|
| 클래스 / 인터페이스 | `UpperCamelCase` | 테스트 클래스는 `Test`로 종료 |
| 메서드 / 변수 | `lowerCamelCase` | 메서드는 동사/전치사로 시작 |
| 상수 | `UPPER_SNAKE_CASE` | |
| boolean 변수 | `is` / `can` / `has` 등 prefix | |

- 임시 변수 외 1글자 변수명 금지

### 코드 스타일

- 와일드카드(`*`) import 절대 금지
- K&R 중괄호 스타일 사용 (조건/반복문에 중괄호 필수)
- 배열 대괄호는 타입 뒤에 선언 (`String[] arr`)
- `Long` 타입 리터럴은 대문자 `L` 사용 (`1000L`)

### 객체지향 & 클린 코드 (생활 체조 원칙)

- 들여쓰기(Indent)는 **2단계까지만 허용** (3단계 이상 금지)
- `else` 예약어 금지 — Early Return 지향, 부정문보다 긍정문 지향
- `Setter` 사용 지양 — 상태 변경은 `change`, `update` 등 의도가 담긴 메서드명 사용
- 메서드 체이닝 시 반드시 줄바꿈으로 절차 표현

### Spring 컴포넌트

- DTO / VO는 `record` 사용 (`~RequestDto`, `~ResponseDto`)
- Controller는 `~RestController`, UseCase는 `~UseCase` 컨벤션 적용
- Service 클래스 레벨에 `@Transactional(readOnly = true)` 선언, CUD 메서드에만 `@Transactional` 명시
- 의존성 주입: `@RequiredArgsConstructor`, `@NoArgsConstructor` 사용 (`@AllArgsConstructor` 금지)

---

## 테스트 컨벤션

- 테스트 메서드명은 **한국어** 작성 (예: `~_예외가_발생한다()`, `~_생성한다()`)
- `@DisplayName` 생략 (클래스 레벨 설정으로 대체)
- 빈 주입은 필드 주입(`@Autowired`) 사용
- `// given`, `// when`, `// then` 주석을 명시적으로 구분 작성
- Mockito BDD 스타일: `given(...)` 셋업, `then(...).should(...)` 검증
- 유닛 테스트: `@ExtendWith(MockitoExtension.class)`
- 통합 테스트: `@SpringBootTest` + H2 인메모리 DB

---

## API 명세

- Swagger: 컨트롤러와 Swagger(API 명세) 인터페이스를 **분리**하여 구현
- 로그: `@Slf4j` 사용

---

## Git 커밋 컨벤션

커밋 메시지 형식 (Udacity 스타일):

```
prefix: 커밋 핵심 내용

본문에 상세 해결 내용 작성
```

- **scope 작성 금지** — `feat(admin):` 대신 `feat:` 형태

### Prefix 목록

| Prefix | 설명 |
|---|---|
| `feat` | 새로운 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 변경 |
| `refactor` | 리팩토링 (기능 변경 없음) |
| `hotfix` | 긴급 수정 |
| `test` | 테스트 코드 추가/수정 |
| `chore` | 빌드, 설정 변경 등 기타 |
| `style` | 코드 포맷팅, 세미콜론 누락 등 |
| `build` | 빌드 시스템 또는 외부 의존성 변경 |
| `ui/ux` | UI/UX 변경 |

[//]: # (---)

[//]: # ()
[//]: # (## 브랜치 전략)

[//]: # ()
[//]: # (- `main` — 배포용)

[//]: # (- `dev` — 개발용)

[//]: # (- 작업 브랜치 네이밍: `{prefix}/{package-name}/{branch-keyword}/{issue-number}`)

[//]: # (    - 예: `feature/user/login/12`)

[//]: # ()
[//]: # (### PR & Merge)

[//]: # ()
[//]: # (- PR 제목: `브랜치명 : PR 요약`)

[//]: # (- Rebase 머지 금지 — 기본 **Merge Commit** 사용 &#40;제목, 내용 디폴트&#41;)

