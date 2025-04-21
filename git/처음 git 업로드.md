1. 원하는 폴더에 진입하여 `git bash` 실행
2. `git init`
	- git 저장소로 초기화
	- `.git` 폴더가 생기고 여기서 버전 관리 됨
1. `git remote add origin git주소`
2. `git add`
3. `git commit -m "commit메세지 작성"`
4. `git branch -M main`
	- 처음 올리는 경우 main 으로 브랜치 설정
5. `git push -u origin main`
	- `-u` 옵션은 이 브랜치를 기본 브랜치로 설정 다음부터는 `git push`만해도 된다.