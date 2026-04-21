# WTS Backend

## Critical Rules (절대 규칙)
- MySQL 8.0 사용 (PostgreSQL 절대 아님)
- Redis / Kafka / WebSocket 3주차 전까지 사용 금지
- .env, application.yml 시크릿 절대 커밋 금지
- main 브랜치 직접 push 금지
- executions ↔ holdings FK 설정 금지 (서비스 레이어에서 연결)
- ddl-auto: create/update 사용 금지 (반드시 Flyway로만 스키마 관리)

## Architecture (아키텍처)
베이스 패키지: com.github.geopark021.wts
도메인 패키지: market / order / execution / portfolio / ops / common

## Build Command (빌드/테스트)
- 실행: ./gradlew bootRun
- 빌드: ./gradlew build
- 테스트: ./gradlew test

## Domain Context (도메인 컨텍스트)
- Instrument: 종목 (KOSPI/KOSDAQ)
- Quote: 현재 시세 (종목당 최신 1건 upsert)
- TradingSession: 거래 세션 (PREOPEN/REGULAR/CLOSED)
- Order: 주문 원장. 상태 6개 (ACCEPTED/PARTIALLY_FILLED/FILLED/CANCELED/REJECTED/EXPIRED)
- Execution: 체결 원장 (append-only)
- CashBalance: 예수금 (available_cash / reserved_cash)
- Holding: 보유 종목
- PortfolioSnapshot: 포트폴리오 read model
- orders.price: DECIMAL(18,2) NULL (시장가는 NULL)
- holdings: UNIQUE KEY uq_holding (account_id, instrument_id)
- orders: UNIQUE KEY uq_client_order (account_id, client_order_id)

## Coding Convention (코딩 컨벤션)
- 엔티티: Lombok 사용 (@Getter, @NoArgsConstructor)
- API 응답: ApiResponse<T> { code, message, data } 형태로 통일
- 예외: BusinessException 상속 → GlobalExceptionHandler에서 처리
- DB 접근: 반드시 Repository 패턴을 통해서만
- 트랜잭션 경계: Service 레이어에서만 설정
- Flyway 파일명: V{숫자}__{설명}.sql
- DB PK: BIGINT AUTO_INCREMENT
- DB 시각 컬럼: created_at, updated_at DATETIME
- Soft delete 없음
- 커밋 메시지: Conventional Commits (feat:, fix:, chore:)
- 코드 주석: 한국어 허용

## 현재 개발 단계
1주차 - 기반 구축 중