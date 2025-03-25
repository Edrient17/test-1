# Git, Github 사용하기

---

## 0. 깃의 핵심 기능
- 버전 관리
- 백업
- 협업

---

## 1. 깃 시작하기

```bash
git config --global user.name "___"       # 커밋 이름 설정
git config --global user.email "___"      # 커밋 이메일 설정
```

### 기본 명령어

```bash
pwd         # 현재 경로 표시
ls          # 디렉터리 및 파일 확인
ls -l       # 상세 정보 표시
ls -a       # 숨김 파일 표시
ls -r       # 정렬 역순
ls -t       # 파일 작성 시간순
clear       # 터미널 창 지우기
```

### 디렉터리 이동/관리

```bash
cd ..           # 상위 디렉터리
cd Users        # 하위 디렉터리, 현재 디렉터리의 Users로 이동
cd ~            # 홈 디렉터리
cd c:           # C 드라이브로 이동
mkdir test      # 디렉터리 생성
rm -r test      # 디렉터리 삭제
exit            # 터미널 종료
```

---

## 2. 깃으로 버전 관리하기

- 작업 트리: 파일 수정, 저장 등의 작업을 하는 디렉터리
- 스테이지: 버전으로 만들 파일이 대기하는 곳(a.k.a. 스테이징 영역)
- 저장소(repository): 스테이지에서 대기하고 있던 파일들을 버전으로 만들어(커밋) 저장하는 곳

```bash
git init                         # 초기화
git status                       # 상태 확인
git add hello.py                 # 특정 파일 스테이징
git add .                        # 모든 파일 스테이징
git commit -m "message1"         # 커밋
git commit --amend               # 메시지 수정
git commit -am "message2"        # add + commit
git log                          # 로그 확인
git log --stat                   # 파일 변경 확인
git log --oneline                # 한 줄 로그
git log --oneline --branches     # 브랜치별 최신 커밋 한눈에 보기
git log --oneline --branches --graph  # 브랜치 커밋 그래프 추가가
git log main..apple              # 브랜치 간 차이 보기, 왼쪽 기준, 오른쪽과 비교. main에는 없고 apple에만 있는 커밋을 보여준다.
git diff                         # 저장소의 최신 버전 파일과 방금 수정한 파일의 차이 보기, VSCODE는 우측 상단의 ‘변경 내용 열기’를 통해 확인 가능
```

- 버전을 한번이라도 만들었던 파일은 tracked, 반대는 untracked 상태이다.
- 버전 관리에서 제외하려면, .gitignore 파일에 명시해놓는다.

### 파일 상태 변화
- `unmodified → modified → staged`

### 상태 되돌리기

```bash
git restore hello.py                    # modified → unmodified
git restore --staged hello.py           # staged → modified
git reset HEAD^                         # 최신 커밋 되돌리기
git reset --soft HEAD^                 # 커밋 취소, staged 유지
git reset --mixed HEAD^                # 커밋 취소, unstaged 유지
git reset --hard <커밋 해시>            # 특정 커밋으로 복구
git revert <커밋 해시>                  # 커밋 되돌리기
```

---

## 3. 깃과 브랜치

- 브랜치 생성, 전환, 병합

```bash
git branch                 # 브랜치 확인
git branch apple           # 브랜치 생성
git switch apple           # 브랜치 전환
git merge o2               # 병합
git branch -d o2           # 브랜치 삭제
git cherry-pick <커밋 해시> # 커밋만 선택 병합
touch m1                   # 새 파일 생성
```

### 병합 케이스

- **자동 병합(Auto-merging)**: 다른 부분 수정
- **수동 병합(conflict)**: 같은 부분 수정 → 수락 버튼으로 조정 후 `add + commit` 필요

---

## 4. 깃허브 시작하기

```bash
git remote add origin <주소>     # 원격 저장소 연결
git remote -v                    # 연결 확인
git push -u origin main          # 최초 푸시
git push                         # 이후 푸시
git pull origin main             # 원격 커밋 가져오기
```

---

## 5. 깃허브로 협업하기

```bash
git clone <주소> .               # 원격 저장소 복제
git fetch                        # 원격 브랜치 정보 가져오기
git diff HEAD origin/main        # 차이 비교
git merge origin/main            # 병합
```

### 협업 절차
1. 저장소 생성
2. 팀원 추가
3. 브랜치별 작업 후 커밋 & 푸시
4. 풀 리퀘스트(PR) 요청
5. 코드 리뷰 및 병합

- 브랜치는 사용 후 삭제해도 복구 가능