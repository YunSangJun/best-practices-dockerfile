# 빌드 이미지 선언(최종 이미지에는 포함되지 않음)
FROM golang:latest AS builder

# Working directory 지정
WORKDIR /go/src/

# 소스코드 복사
COPY src/app.go .

# 소스코드 빌드
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

# Base 이미지 선언(최종 이미지)
FROM alpine:latest

# 인증서 추가
RUN apk --no-cache add ca-certificates

# Working directory 지정
WORKDIR /root/

# Build 결과 복사(빌드 이미지로 부터)
COPY --from=builder /go/src/app .

# 바이너리 실행 
CMD ["./app"]
