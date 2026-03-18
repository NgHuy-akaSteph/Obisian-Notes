
## 1. Muc tieu  
  
- Tao mot ban thiet ke tai lieu tong hop cho ChatApp.  
- Dinh nghia cach chia he thong thanh 3 services: `user`, `chat`, `media`.  
- Mapping API hien tai (`API.md`) vao module/service tuong ung.  
- Tao nen tang cho migration an toan tu monolith sang microservices.  
  
## 2. Pham vi  
  
Tai lieu nay cover:  
- Kien truc hien tai (monolith Spring Boot).  
- Kien truc dich (microservices + gateway + async events).  
- Boundary va ownership cua tung service.  
- Mapping endpoint -> service.  
- Data ownership, security, observability, deployment, migration roadmap.  
  
Khong cover chi tiet implementation tung class/dto.  
  
## 3. Hien trang (As-Is)  
  
- 1 ung dung Spring Boot monolith.  
- API base path: `/api/v1`.  
- Auth: JWT Bearer.  
- WebSocket STOMP endpoint: `/api/v1/ws`.  
- Domain hien co: auth, user, friend, notification, conversation, group, message, file, admin/report, health.  
  
## 4. Kien truc dich (To-Be)  
  
## 4.1 Logical architecture  
  
- `API Gateway`  
  - Xac thuc token (hoac introspection), rate limit, request routing.  
  - Route toi `user-service`, `chat-service`, `media-service`.  
- `user-service`  
  - Auth, profile, friendship, notification, user moderation/admin user ops.  
- `chat-service`  
  - Conversation, group, message, read/typing, websocket realtime hub.  
- `media-service`  
  - Upload/download/delete file, metadata, signed URL, anti-virus scan hook.  
- `Event Bus` (Kafka/RabbitMQ) (khuyen nghi)  
  - Dong bo su kien giua services: user-updated, message-created, media-uploaded.  
  
## 4.2 Suggested network/API layout  
  
- Public entry: `https://api.chatapp.com`  
- Internal routes (qua gateway):  
  - `/api/v1/user/**` -> `user-service`  
  - `/api/v1/chat/**` -> `chat-service`  
  - `/api/v1/media/**` -> `media-service`  
  
Luu y: de giam break change, co the giu nguyen duong dan cu trong giai doan dau, gateway map path cu sang service moi.  
  
## 5. Service boundaries va trach nhiem  
  
## 5.1 user-service  
  
Owner domains:  
- Identity: login/register/refresh/password/profile.  
- User profile + online status preference.  
- Friendship va friend request.  
- Notification (in-app).  
- User report submission (nguoi dung gui report).  
- Admin dashboards/reports/sync lien quan user lifecycle.  
  
DB ownership de xuat:  
- `users`, `credentials`, `user_settings`, `friendships`, `friend_requests`, `notifications`, `reports`, `admin_actions`.  
  
## 5.2 chat-service  
  
Owner domains:  
- Conversation 1-1, group chat, membership.  
- Messages (CRUD, search, pin, unread, read receipt).  
- Realtime websocket (chat.send, typing, read).  
  
DB ownership de xuat:  
- `conversations`, `conversation_members`, `messages`, `message_reads`, `pinned_messages`, `typing_state`.  
  
## 5.3 media-service  
  
Owner domains:  
- File upload/download/delete/list/folder.  
- Media metadata va object-storage abstraction.  
- Malware scan/transcoding hooks (future).  
  
DB ownership de xuat:  
- `media_files`, `media_acl`, `upload_sessions`.  
- Object storage bucket: avatars, chat attachments, temp uploads.  
  
## 6. API mapping (Endpoint -> Service)  
  
Nguon mapping: `API.md`.  
  
## 6.1 user-service mapping  
  
| Group | Method | Path |  
|---|---|---|  
| Authentication | POST | `/api/v1/auth/login` |  
| Authentication | POST | `/api/v1/auth/register` |  
| Authentication | POST | `/api/v1/auth/refresh` |  
| Authentication | GET | `/api/v1/auth/profile` |  
| Authentication | POST | `/api/v1/auth/change-password` |  
| Users | POST | `/api/v1/users` |  
| Users | GET | `/api/v1/users` |  
| Users | GET | `/api/v1/users/{id}` |  
| Users | PUT | `/api/v1/users/{id}` |  
| Users | DELETE | `/api/v1/users/{id}` |  
| Users | GET | `/api/v1/users/{userId}/online-status` |  
| Users | POST | `/api/v1/users/online-status/bulk` |  
| Users | PUT | `/api/v1/users/settings/online-status?hide={true|false}` |  
| Friends | POST | `/api/v1/friends/requests` |  
| Friends | POST | `/api/v1/friends/requests/{requestId}/accept` |  
| Friends | POST | `/api/v1/friends/requests/{requestId}/reject` |  
| Friends | DELETE | `/api/v1/friends/requests/{requestId}` |  
| Friends | GET | `/api/v1/friends/search` |  
| Friends | DELETE | `/api/v1/friends/{friendId}` |  
| Friends | GET | `/api/v1/friends/requests/received` |  
| Friends | GET | `/api/v1/friends/requests/sent` |  
| Friends | GET | `/api/v1/friends/requests/count` |  
| Friends | GET | `/api/v1/friends/{id}` |  
| Friends | GET | `/api/v1/friends/search-users` |  
| Friends | PUT | `/api/v1/friends/{friendId}/nickname` |  
| Friends | GET | `/api/v1/friends/online` |  
| Notifications | GET | `/api/v1/notifications` |  
| Notifications | GET | `/api/v1/notifications/unread-count` |  
| Notifications | PUT | `/api/v1/notifications/{notificationId}/read` |  
| Notifications | PUT | `/api/v1/notifications/mark-all-read` |  
| Notifications | DELETE | `/api/v1/notifications/{notificationId}` |  
| Reports | POST | `/api/v1/reports` |  
| Reports | GET | `/api/v1/reports/my` |  
| Admin Dashboard | GET | `/api/v1/admin/dashboard/stats` |  
| Admin Dashboard | GET | `/api/v1/admin/dashboard/recent-users` |  
| Admin Dashboard | GET | `/api/v1/admin/dashboard/recent-groups` |  
| Admin Dashboard | GET | `/api/v1/admin/dashboard/recent-actions` |  
| Admin Dashboard | GET | `/api/v1/admin/dashboard/attendance?year={yyyy}` |  
| Admin Dashboard | POST | `/api/v1/admin/dashboard/refresh` |  
| Admin Reports | GET | `/api/v1/admin/reports` |  
| Admin Reports | GET | `/api/v1/admin/reports/{id}` |  
| Admin Reports | POST | `/api/v1/admin/reports/{id}/actions` |  
| Admin Sync | POST | `/api/v1/admin/sync/user/{userId}/avatar` |  
| Admin Sync | POST | `/api/v1/admin/sync/user/{userId}` |  
| Admin Sync | POST | `/api/v1/admin/sync/recent?hoursAgo={n}` |  
| Admin Sync | POST | `/api/v1/admin/sync/all` |  
  
## 6.2 chat-service mapping  
  
| Group | Method | Path |  
|---|---|---|  
| Conversations | POST | `/api/v1/conversations` |  
| Conversations | GET | `/api/v1/conversations/check?otherUserId={id}` |  
| Conversations | GET | `/api/v1/conversations` |  
| Conversations | GET | `/api/v1/conversations/{id}` |  
| Conversations | PUT | `/api/v1/conversations/{id}` |  
| Conversations | DELETE | `/api/v1/conversations/{id}` |  
| Conversations | GET | `/api/v1/conversations/{id}/members/online` |  
| Conversations | GET | `/api/v1/conversations/{id}/media` *(join voi media-service)* |  
| Groups | POST | `/api/v1/groups` |  
| Groups | PUT | `/api/v1/groups/{id}` |  
| Groups | GET | `/api/v1/groups/{id}` |  
| Groups | DELETE | `/api/v1/groups/{id}` |  
| Groups | POST | `/api/v1/groups/{id}/members` |  
| Groups | DELETE | `/api/v1/groups/{id}/members/{memberId}` |  
| Groups | POST | `/api/v1/groups/{id}/leave` |  
| Groups | GET | `/api/v1/groups/{id}/members` |  
| Messages | POST | `/api/v1/messages` |  
| Messages | GET | `/api/v1/messages` |  
| Messages | GET | `/api/v1/messages/cursor` |  
| Messages | GET | `/api/v1/messages/{messageId}` |  
| Messages | POST | `/api/v1/messages/read` |  
| Messages | DELETE | `/api/v1/messages/{messageId}` |  
| Messages | PUT | `/api/v1/messages/{messageId}/pin?pinned={true|false}` |  
| Messages | GET | `/api/v1/messages/search` |  
| Messages | GET | `/api/v1/messages/pinned?conversationId={id}` |  
| Messages | GET | `/api/v1/messages/unread/summary` |  
| Messages | GET | `/api/v1/messages/unread/conversations` |  
| Messages | GET | `/api/v1/messages/unread/count` |  
| Messages | GET | `/api/v1/messages/unread/count/{conversationId}` |  
| Messages | POST | `/api/v1/messages/upload` *(orchestrate voi media-service)* |  
  
## 6.3 media-service mapping  
  
| Group | Method | Path |  
|---|---|---|  
| Files | GET | `/api/v1/files/test-connection` |  
| Files | POST | `/api/v1/files/upload` |  
| Files | DELETE | `/api/v1/files/{fileId}` |  
| Files | GET | `/api/v1/files` |  
| Files | GET | `/api/v1/files/{fileId}` |  
| Files | GET | `/api/v1/files/folders` |  
  
## 6.4 Shared/System endpoints  
  
| Group | Method | Path | Owner |  
|---|---|---|---|  
| Health | GET | `/api/v1/health` | Gateway + each service health contributor |  
| Health | GET | `/api/v1/health/ws` | chat-service |  
| Health | GET | `/api/v1/db/test-connection` | tung service expose rieng (`/health/db`) |  
  
## 6.5 WebSocket mapping  
  
- Owner: `chat-service`  
- Client -> server (`/app`):  
  - `/app/chat.send`  
  - `/app/chat.typing`  
  - `/app/chat.read`  
- Server -> client:  
  - `/topic/conversations/{conversationId}`  
  - `/topic/conversations/{conversationId}/typing`  
  - `/topic/conversations/{conversationId}/read`  
  - `/topic/user-status` *(co the consume user-status event tu user-service)*  
  - `/topic/keep-alive`  
  - `/user/queue/messages`  
  - `/user/queue/ack`  
  - `/user/queue/errors`  
  - `/user/queue/system`  
  
## 7. Luong nghiep vu chinh  
  
## 7.1 Send text message  
  
1. Client goi `chat-service` send message.  
2. `chat-service` validate membership + persist message.  
3. `chat-service` publish websocket event den subscribers.  
4. `chat-service` emit `message.created` event cho notification pipeline.  
  
## 7.2 Send file message  
  
1. Client upload file qua `media-service` (hoac endpoint orchestration cua `chat-service`).  
2. `media-service` luu object + metadata, tra `fileId`/URL.  
3. `chat-service` tao message type `FILE` tham chieu `fileId`.  
4. `chat-service` push realtime event; user click message se fetch metadata/file URL tu `media-service`.  
  
## 7.3 User profile update  
  
1. User update profile tai `user-service`.  
2. `user-service` emit `user.updated` event.  
3. `chat-service` cap nhat cache denormalized (displayName/avatar snapshot neu can).  
  
## 8. Security design  
  
- JWT ky boi auth provider (trong user-service hoac central auth).  
- Gateway verify JWT va pass trusted headers (`x-user-id`, `x-roles`) cho downstream.  
- Service-to-service auth dung mTLS hoac signed internal JWT.  
- RBAC:  
  - `USER`: app user operations.  
  - `ADMIN`: moderation/report/admin endpoints.  
- Media security:  
  - Signed URL het han ngan.  
  - Validate content-type + max size + optional malware scan.  
  
## 9. Observability  
  
- Centralized logging: traceId, userId, conversationId.  
- Metrics (Prometheus/OpenTelemetry):  
  - request latency/error rate per endpoint.  
  - websocket active sessions.  
  - upload success/fail ratio.  
- Distributed tracing cho flow: gateway -> service -> event bus -> service.  
- Alerting:  
  - p95 latency vuot nguong.  
  - websocket disconnect spike.  
  - upload failure spike.  
  
## 10. Deployment model  
  
- Moi service dockerized, deploy rieng.  
- 1 gateway + 3 services + backing stores.  
- Recommendation:  
  - `user-service` + `chat-service`: MongoDB collections tach ownership.  
  - `media-service`: MongoDB metadata + S3-compatible object storage.  
- Cache/queue (optional): Redis + Kafka/RabbitMQ.  
  
## 11. Migration roadmap  
  
## Phase 0 - Preparation  
- Define contracts (OpenAPI, events, error model).  
- Introduce gateway truoc, route ve monolith.  
  
## Phase 1 - Extract media-service first  
- Tach file APIs sang `media-service`.  
- Monolith/chat goi media thong qua internal API.  
  
## Phase 2 - Extract user-service  
- Tach auth/users/friends/notifications/reports/admin user flows.  
- Add event `user.updated`, `friendship.updated`.  
  
## Phase 3 - Extract chat-service  
- Tach conversation/group/message/websocket.  
- Chuyen unread/read counters ve chat DB ownership.  
  
## Phase 4 - Stabilize and optimize  
- Remove old monolith endpoints.  
- Harden SLO, autoscaling, resilience tests.  
  
---  
