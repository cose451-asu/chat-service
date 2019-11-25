# chat-service
gRPC Protocol of chat-server

## Authentication Protocol
`service AuthService`를 통해 유저 가입 및 OAuth 토큰 갱신이 가능합니다.

Refreshing OAuth token or user sign up are possible through `service AuthService`.

## Chat Services
`service AuthService` 와 달리, `service UserService`, `service ChatRoomService`는 인증된 유저를 위한 API Service이기 때문에
요청의 gRPC Header에 `access-token` 필드가 존재해야 합니다. 
`access-token`의 유효기간이 약 1시간이기 때문에, 만약 토큰이 만료된 경우 `UNAUTHENTICATED(Status Code 16)` 이 반환됩니다.
해당 상황에서는 클라이언트가 `AuthService`의 `RefreshToken`을 수행한 후 갱신된 토큰으로 다시 한 번 API 요청을 수행해야 합니다. 

Unlike`service AuthService`, `service UserService` and `service ChatRoomService` are API Services for authorized users so `access-token` field should exist on the requested gRPC Header.
`access-token` is valid for one hour so if expired it returns `UNAUTHENTICATED(Status Code 16)`. In such case, client executes `RefreshToken` of `AuthService` and requests API with refreshed tokens again. 
