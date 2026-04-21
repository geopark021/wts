# Project: WTS (Web Trading System)

## Critical Rules (절대 규칙)
- .env, application.yml 시크릿 절대 커밋 금지
- main 브랜치 직접 push 금지 - PR을 통해 머지
- Redis/Kafka/WebSocket은 3주차 전까지 사용 금지
- MySQL 8.0 사용 (PostgreSQL 절대 아님)

## Architecture (아키텍처)
backend/   → Spring Boot 3.5.13, Java 21 (현재 작업 중)
frontend/  → React + Vite (1주차 목요일 예정)
docker/    → Redis, Kafka, MySQL (3주차 예정)
docs/      → 설계 문서

## Tech Stack (기술 스택)
- Backend: Java 21, Spring Boot 3.5.13, Gradle-Groovy
- DB: MySQL 8.0, Flyway Migration
- Cache: Redis (3주차)
- Event: Kafka (3주차)
- Frontend: React + Vite, TypeScript
- Monitoring: Prometheus + Grafana (4주차)

## Build Command (빌드 명령어)
```bash
# 백엔드
cd backend
./gradlew bootRun      # 개발 서버 실행
./gradlew build        # 빌드
./gradlew test         # 테스트

# 프론트엔드 
cd frontend
npm install
npm run dev
```

## Domain Context (도메인 컨텍스트)
- **Instrument**: 종목 (KOSPI/KOSDAQ)
- **Quote**: 현재 시세 (종목당 최신 1건 upsert)
- **TradingSession**: 거래 세션 (PREOPEN/REGULAR/CLOSED)
- **Order**: 주문 원장. 상태 6개 (ACCEPTED/PARTIALLY_FILLED/FILLED/CANCELED/REJECTED/EXPIRED)
- **Execution**: 체결 원장 (append-only)
- **CashBalance**: 예수금
- **Holding**: 보유 종목
- **PortfolioSnapshot**: 포트폴리오 read model

## 현재 개발 단계
1주차 - 백엔드 기반 구축 중