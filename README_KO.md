# 문장 교정기 Android 프로젝트

## 구현 기능
- Android 문서 선택기를 통한 `.txt` 파일 선택
- 11가지 문장 교정 원칙을 적용한 AI 문맥 기반 교정
- 교정 결과 미리보기 및 저장 전 사용자의 직접 수정
- Android 폴더 선택기를 통한 저장 폴더 지정
- `원본파일명_교정.txt`로 별도 저장
- UTF-8 읽기/쓰기, UTF-8 BOM 제거
- 원본 파일은 덮어쓰지 않음
- API 키는 앱 실행 중 메모리에만 두며 로컬에 저장하지 않음

## 필요한 환경
- Android Studio (권장: 최신 안정판)
- JDK 17
- Android SDK Platform 35
- 인터넷 연결 및 OpenAI 호환 Chat Completions API 키

## APK 빌드 방법
1. Android Studio에서 이 프로젝트 폴더 `TextProofreaderAndroid`를 엽니다.
2. Gradle 동기화를 완료합니다. 최초 빌드 시 Android Gradle Plugin과 Kotlin 플러그인을 내려받아야 합니다.
3. `Build > Build Bundle(s) / APK(s) > Build APK(s)`를 선택합니다.
4. APK는 일반적으로 `app/build/outputs/apk/debug/app-debug.apk`에 생성됩니다.
5. APK를 Android 기기로 옮겨 설치합니다. 설치 시 출처를 알 수 없는 앱 설치 허용이 필요할 수 있습니다.

## 앱 사용 방법
1. 앱에서 `텍스트 파일 선택`을 누르고 UTF-8 텍스트 파일을 선택합니다.
2. AI 서비스 API 키를 입력합니다. 기본 주소는 `https://api.openai.com/v1/chat/completions`, 기본 모델명은 `gpt-4o-mini`입니다. 사용하는 서비스에 따라 주소와 모델을 변경하세요.
3. `AI 문장 교정 시작`을 누릅니다.
4. 결과를 확인하고 필요하면 미리보기 상자에서 직접 수정합니다.
5. `저장 폴더 지정`으로 폴더를 선택하고 `교정된 파일 저장`을 누릅니다.

## 보안 및 제한
- 이 앱은 AI 교정을 위해 원문 텍스트 전체를 설정한 API 서버에 전송합니다. 개인정보나 민감한 내용은 전송 전에 확인하세요.
- API 키는 앱에 저장하지 않지만, 네트워크 요청 시 메모리에서 사용됩니다. APK에 키를 하드코딩하지 마세요.
- API 사용료가 발생할 수 있습니다.
- 매우 긴 파일은 모델의 입력/출력 한도 또는 서비스 비용에 걸릴 수 있습니다. 긴 파일은 여러 파일로 나누어 교정하는 것이 안전합니다.
- 이 실행 환경에는 Android SDK와 Gradle이 설치되어 있지 않고 인터넷 연결도 되지 않아 APK를 직접 빌드할 수 없었습니다. 이 폴더는 Android Studio에서 빌드할 수 있는 프로젝트 소스입니다.

## GitHub Actions로 APK 자동 빌드
1. GitHub에서 새 저장소(repository)를 만듭니다.
2. 이 프로젝트 폴더 안의 파일과 폴더를 저장소 루트에 업로드합니다. `app`, `.github`, `build.gradle.kts`, `settings.gradle.kts`가 저장소 최상위에 있어야 합니다.
3. `Actions` 탭에서 `Build Android APK` 워크플로를 선택합니다.
4. `Run workflow`를 누르거나 `main`/`master` 브랜치에 코드를 push하면 빌드가 시작됩니다.
5. 빌드가 성공하면 실행 결과 페이지 아래 `Artifacts`에서 `textproofreader-debug-apk`를 다운로드합니다.
6. ZIP 압축을 풀면 `app-debug.apk`가 있습니다. 이 파일을 Android 기기로 옮겨 설치하세요.

참고: 이 워크플로는 디버그 APK를 만듭니다. Google Play 배포용 서명 APK/AAB는 별도의 서명 설정이 필요합니다. API 키는 GitHub 저장소나 소스 코드에 넣지 마세요.
