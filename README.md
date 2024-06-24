# 대한민국 전국 건물 데이터 수집 시스템

이 프로젝트는 data.go.kr의 건축물대장 표제부 API에서 데이터를 수집하고 처리하는 멀티스레드 환경을 위한 시스템입니다.
시스템은 대용량 데이터를 효율적으로 처리하고, 다시 시작할때 중단점 부터 시작할 수 있습니다.

## 목차

- [기능](#기능)
- [설치](#설치)
- [사용법](#사용법)
- [구성](#구성)
- [기여](#기여)
- [라이선스](#라이선스)

## 기능

- **멀티스레드 처리**: 여러 스레드를 사용하여 데이터를 효율적으로 처리합니다.
- **중단점 부터 시작**: 사용자 입력에 따라 멀티 쓰레딩을 즉시 종료할 수 있습니다.
- **에러 처리 및 로깅**: 원활한 운영을 위해 포괄적인 로깅 및 에러 처리 기능을 갖추고 있습니다.
- **진행 상황 추적**: `tqdm`을 사용하여 진행률 표시줄을 제공합니다.

## 설치

1. 레포지토리를 클론합니다:
    ```sh
    git clone https://github.com/realcoding2003/bunji-data-index.git
    cd bunji-data-index
    ```

2. 가상 환경을 생성하고 활성화합니다:
    ```sh
    python -m venv venv
    source venv/bin/activate  # 윈도우에서는 `venv\Scripts\activate` 사용
    ```

3. 필요한 패키지를 설치합니다:
    ```sh
    pip install -r requirements.txt
    ```

4. 루트 디렉토리에 `.env` 파일을 생성하고 필요한 환경 변수를 추가합니다:
    ```env
    MAX_THREADS=5
    SERVICE_KEY=your_service_key
    BASE_URL=http://apis.data.go.kr/1613000/BldRgstService_v2/getBrTitleInfo
    SIGUNGU=11110
    BJDONG=14000
    ```

5. `config` 디렉토리에 `address_code.json` 파일이 있는지 확인합니다:
    ```json
    {
        "1100000000": "서울특별시",
        "1111000000": "서울특별시 종로구"
    }
    ```

## 사용법 (단건 테스트)

데이터 수집 및 처리 시스템을 테스트 하려면 .env파일의 환경변수를 수정하고 다음 명령어를 사용하십시오:

```sh
python main.py
```

이 명령어는 `.env` 파일에 지정된 `SIGUNGU` 및 `BJDONG` 코드를 사용하여 데이터 처리를 시작합니다.

## 사용법 (전체 수집)

데이터 수집 및 처리 시스템을 테스트 하려면 다음 명령어를 사용하십시오:

```sh
python collect_all_data.py
```

이 명령어는 `data` 폴더에 데이터를 저장하고 `logs` 폴더에 오류 내용을 기록합니다.

## 구성

- **환경 변수**:
  - `MAX_THREADS`: 처리에 사용할 최대 스레드 수.
  - `SERVICE_KEY`: API 서비스 키.
  - `BASE_URL`: API 기본 URL.
  - `SIGUNGU`: 기본 시군구 코드.
  - `BJDONG`: 기본 법정동 코드.
 
- `SERVICE_KEY`: (https://www.data.go.kr/index.do)에 가입해서 키를 발급 받으세요.

- **address_code.json**: 주소 코드 매핑을 포함하는 JSON 파일
- 참고(https://gist.github.com/realcoding2003/64e1ea791a4cad8b6faf53d018edc4be).

## 기여

기여를 환영합니다! 다음 방법으로 도울 수 있습니다:

1. **레포지토리를 포크**하고, 브랜치를 만듭니다:
    ```sh
    git checkout -b feature/your-feature-name
    ```

2. **변경 사항을 적용**하고 테스트를 통과하는지 확인합니다.
3. **변경 사항을 커밋**하고 GitHub에 브랜치를 푸시합니다:
    ```sh
    git push origin feature/your-feature-name
    ```

4. **풀 리퀘스트를 생성**하고 변경 사항에 대한 상세 설명을 제공합니다.

### 이슈 보고

문제가 발생하면 GitHub에 이슈를 열고 문제를 상세히 설명해 주세요.

### 문서 개선

이 `README.md` 파일을 수정하거나 필요한 경우 새로운 문서 파일을 만들어 문서를 개선하는 데 도움을 줄 수 있습니다.

## 라이선스

이 프로젝트는 MIT 라이선스에 따라 라이선스가 부여됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하십시오.