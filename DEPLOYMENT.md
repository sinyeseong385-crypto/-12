# Deployment Guide for 애니 메이션 티어표

## 1. 준비된 상태 확인
- GitHub 저장소에 코드가 올라가 있어야 합니다.
- `prisma/schema.prisma`는 PostgreSQL을 사용하도록 설정되어 있습니다.
- `.env.example` 파일이 준비되어 있습니다.

## 2. Vercel에 배포하기
1. Vercel에 로그인합니다.
2. `New Project`를 클릭합니다.
3. GitHub을 연결하고, 해당 저장소를 선택합니다.
4. 설정을 확인하고 `Import`를 누릅니다.

### 권장 빌드 설정
- 빌드 커맨드: `npm run build`
- 출력 디렉터리: 비워둡니다

## 3. 환경 변수 설정
Vercel Dashboard에서 프로젝트의 Settings → Environment Variables로 이동하여 다음을 추가합니다.

- `DATABASE_URL`
- `NEXTAUTH_URL` = `https://<your-vercel-domain>`
- `NEXTAUTH_SECRET` = 랜덤 긴 문자열

예시:
```env
DATABASE_URL="postgresql://user:password@host:5432/dbname"
NEXTAUTH_URL="https://your-site.vercel.app"
NEXTAUTH_SECRET="your_long_random_secret"
```

## 4. 배포 후 Prisma 마이그레이션
배포 DB에 연결하여 아래 명령을 실행합니다.

```bash
cd "c:\Users\Lim\Desktop\애니 메이션 티어표"
# 로컬에서 배포 DB를 사용할 경우
set DATABASE_URL="postgresql://..."
npx prisma migrate deploy
node prisma/seed.js
```

## 5. 확인할 것
- 사이트가 정상적으로 열리는지
- 로그인/로그아웃이 되는지
- `/admin` 페이지 접근이 되는지
- 티어 추가/삭제, 애니 추가가 동작하는지

## 6. 참고
- 저는 이 환경에서는 GitHub나 Vercel 계정에 접속하거나 직접 배포할 수 없습니다.
- 대신 위 단계를 따라 주시면 배포가 가능합니다.
- 원하시면 Vercel이나 PostgreSQL 서비스 선택까지 세부적으로 도와드릴 수 있습니다.
