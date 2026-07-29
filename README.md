# GVCS Planner – APK 빌드 방법 (플레이스토어 배포 없이)

이 프로젝트는 원본 GVCS Planner 웹앱(`www/index.html`)을 Capacitor로 감싼
안드로이드 앱 프로젝트입니다. 화면 너비가 700px 이하일 때 자동으로 모바일
레이아웃이 나오도록 되어 있는 원본 코드 그대로 사용했기 때문에, 폰 화면에서
실행하면 자연스럽게 모바일 UI로 보입니다.

이 작업 환경(샌드박스)에서는 구글 빌드 서버 접속이 막혀 있어서
APK를 직접 컴파일할 수 없습니다. 대신 **GitHub Actions로 클라우드에서
자동 빌드**하도록 준비해뒀습니다. 아래 순서대로 하면 안드로이드 스튜디오
설치 없이 APK 파일을 받을 수 있습니다.

## 1. GitHub에 올리기
1. github.com 에서 새 저장소(Repository)를 하나 만듭니다. (Public/Private 상관없음)
2. 이 폴더 전체를 그 저장소에 push 합니다.
   ```bash
   cd gvcs-app
   git init
   git add .
   git commit -m "init"
   git branch -M main
   git remote add origin <내_저장소_주소>
   git push -u origin main
   ```

## 2. 자동 빌드 확인
1. 저장소 페이지에서 **Actions** 탭으로 이동합니다.
2. "Build APK" 워크플로우가 자동으로 실행됩니다 (몇 분 소요).
3. 초록 체크가 뜨면 완료된 것입니다.

## 3. APK 다운로드
1. 완료된 워크플로우 실행 결과를 클릭합니다.
2. 아래쪽 **Artifacts** 항목에서 `gvcs-planner-apk`를 다운로드합니다.
3. 압축을 풀면 `app-debug.apk` 파일이 나옵니다.

## 4. 폰에 설치
1. `app-debug.apk` 파일을 폰으로 전송합니다 (카카오톡 나에게 보내기, 구글 드라이브, USB 등).
2. 폰에서 파일을 눌러 설치합니다.
3. "출처를 알 수 없는 앱 설치 차단" 경고가 뜨면 설정에서 허용 후 설치하면 됩니다.

## 참고
- 이 방식은 **디버그(debug) APK**입니다. 개인 설치용으로는 문제없지만,
  나중에 여러 사람에게 배포하려면 서명(release)된 APK로 바꾸는 게 좋습니다.
- 앱 이름/아이콘을 바꾸고 싶으면 `android/app/src/main/res` 폴더의 아이콘 파일과
  `strings.xml`의 `app_name`을 수정하면 됩니다.
- Supabase 로그인 등 네트워크 기능은 `AndroidManifest.xml`에 인터넷 권한이
  이미 포함돼 있어 그대로 동작합니다.
