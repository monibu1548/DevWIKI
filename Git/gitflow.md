# Git Flow

- 표준으로 사용하는 규약

## Main Branch
- master : 다양한 브랜치가 Merge 되는 브랜치
- develop : 개발할 때 사용되는 브랜치

## Supporting Branch
### feature branch
- 추가 기능이 있는 경우
- develop branch 를 기초로 생성
- 완료 후 develop branch 로 Merge
- 완료 후 branch 제거

### release branch
- 배포 직전 테스트 브랜치
- README 등 수정
- develop branch를 기초로 생성
- 완료 후 master와 develop 으로 Merge
- 완료 후 삭제
- version 을 남김

### hotfix branch
- 배포 후 버그 발견시 생성
- master branch 를 기초로 생성
- 완료 후 master와 develop으로 Merge
- 완료 후 삭제
