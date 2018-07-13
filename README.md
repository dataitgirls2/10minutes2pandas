# 10 Minutes to pandas 한글번역


## 목적 : 
* 해당 문서를 번역함으로서 판다스를 더 잘 이해하기 위함입니다.
* 다음으로 전체 문서를 함께 번역하는 작업을 통해 협업을 경험해 보고 깃헙을 좀 더 잘 활용해 보도록 합니다.
* 다른 조의 문서를 리뷰하면서 익혀봅니다. 이 때 오타나 문법오류 추가하면 좋을만한 내용이 있다면 개선해 봅니다. 
* 깃헙 페이지로 공개해서 판다스를 공부하는 사람들에게도 도움을 주도록 해요.
* 오픈소스에 기여하는 방법을 간접적으로 체험해 봅니다.

## 실습 및 과제 :
0. 해당 조의 번역 부분을 확인하고 개인별로 과업을 나눕니다.

1. 10minutes2pandas 리포를 Fork 하고 clone합니다.

`git clone git@github.com:자신의깃헙ID/10minutes2pandas.git`

`cd 10minutes2pandas` 로 클론 받은 폴더로 이동합니다.

2. 조별로 브랜치를 생성해 놓았습니다. git checkout 조별브랜치명 1_0_to_22
각자의 조별 브랜치로 이동합니다.

* A조: `git checkout 1_0_to_22`
* B조: `git checkout 2_23_to_54`
* C조: `git checkout 3_55_to_72`
* D조: `git checkout 4_73_to_90`
* E조: `git checkout 5_91_to_107`
* F조: `git checkout 6_108_to_126`
* G조: `git checkout 7_127_to_140`
* H조: `git checkout 8_141_to_Gotchas`

3. 해당 브랜치에 마스터 브랜치의 최신 내용을 가져와서 작업하도록 합니다.
`git pull --rebase origin master`

4. index.ipynb 파일을 열어 각자 조에서 맡은 부분을 코딩 및 번역하고 설명을 추가 합니다.
번역 외에 도움이 되는 설명을 추가해도 괜찮습니다.

5. 조별로 번역과정이 끝나면 `각자의 브랜치에 push` 하고 pull request를 보냅니다. 
 * 변경 내용을 add 하고 commit 할 때 터미널이 아니라 소스트리를 사용해 봅니다.

6. merge 는 변경된 조에서 번역 내용을 확인하고 반영합니다.
