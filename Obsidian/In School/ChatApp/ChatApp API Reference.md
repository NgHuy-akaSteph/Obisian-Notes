## Base Information  
  
- Base URL: `/api/v1`  
- Auth: Bearer JWT in `Authorization: Bearer <token>`  
- Default response wrapper: `ApiResponse<T>`  
- Swagger UI: `/api/v1/swagger-ui.html`  
- OpenAPI docs: `/api/v1/api-docs`  
  
## Access Rules  
  
- `Public`: no REST auth required by `SecurityConfig`  
- `Auth`: requires authenticated user (`USER` or `ADMIN`)  
- `Admin`: requires role `ADMIN`  
  
---  

## 1) Authentication  
  
| Method | Path                           | Access | Description          |     |
| ------ | ------------------------------ | ------ | -------------------- | --- |
| POST   | `/api/v1/auth/login`           | Public | Login                |     |
| POST   | `/api/v1/auth/register`        | Public | Register             |     |
| POST   | `/api/v1/auth/refresh`         | Public | Refresh access token |     |
| GET    | `/api/v1/auth/profile`         | Auth   | Current user profile |     |
| POST   | `/api/v1/auth/change-password` | Auth   | Change password      |     |
  
## 2) Users  
  
| Method | Path | Access | Description |  
|---|---|---|---|  
| POST | `/api/v1/users` | Auth | Create user |  
| GET | `/api/v1/users` | Auth | Search/list users |  
| GET | `/api/v1/users/{id}` | Auth | Get user by id |  
| PUT | `/api/v1/users/{id}` | Auth | Update user |  
| DELETE | `/api/v1/users/{id}` | Auth | Delete user |  
| GET | `/api/v1/users/{userId}/online-status` | Auth | Get online status |  
| POST | `/api/v1/users/online-status/bulk` | Auth | Get online status for many users |  
| PUT | `/api/v1/users/settings/online-status?hide={true|false}` | Auth | Hide/show online status |  
  
## 3) Conversations  
  
| Method | Path                                           | Access | Description                     |     |
| ------ | ---------------------------------------------- | ------ | ------------------------------- | --- |
| POST   | `/api/v1/conversations`                        | Auth   | Create 1-1 conversation         |     |
| GET    | `/api/v1/conversations/check?otherUserId={id}` | Auth   | Check existing 1-1 conversation |     |
| GET    | `/api/v1/conversations`                        | Auth   | Search conversations            |     |
| GET    | `/api/v1/conversations/{id}`                   | Auth   | Get conversation details        |     |
| PUT    | `/api/v1/conversations/{id}`                   | Auth   | Update conversation settings    |     |
| DELETE | `/api/v1/conversations/{id}`                   | Auth   | Delete conversation             |     |
| GET    | `/api/v1/conversations/{id}/members/online`    | Auth   | List online members             |     |
| GET    | `/api/v1/conversations/{id}/media`             | Auth   | Get media in conversation       |     |
  
## 4) Groups  
  
| Method | Path                                     | Access | Description         |     |     |
| ------ | ---------------------------------------- | ------ | ------------------- | --- | --- |
| POST   | `/api/v1/groups`                         | Auth   | Create group        |     |     |
| PUT    | `/api/v1/groups/{id}`                    | Auth   | Update group        |     |     |
| GET    | `/api/v1/groups/{id}`                    | Auth   | Get group details   |     |     |
| DELETE | `/api/v1/groups/{id}`                    | Auth   | Delete group        |     |     |
| POST   | `/api/v1/groups/{id}/members`            | Auth   | Add members         |     |     |
| DELETE | `/api/v1/groups/{id}/members/{memberId}` | Auth   | Remove member       |     |     |
| POST   | `/api/v1/groups/{id}/leave`              | Auth   | Leave group         |     |     |
| GET    | `/api/v1/groups/{id}/members`            | Auth   | Search/list members |     |     |
  
## 5) Messages  
  
| Method | Path                                             | Access  | Description                              |                   |     |
| ------ | ------------------------------------------------ | ------- | ---------------------------------------- | ----------------- | --- |
| POST   | `/api/v1/messages`                               | Auth    | Send message                             |                   |     |
| GET    | `/api/v1/messages`                               | Auth    | List messages (page-based)               |                   |     |
| GET    | `/api/v1/messages/cursor`                        | Auth    | List messages (cursor-based)             |                   |     |
| GET    | `/api/v1/messages/{messageId}`                   | Auth    | Get message by id                        |                   |     |
| POST   | `/api/v1/messages/read`                          | Auth    | Mark messages as read                    |                   |     |
| DELETE | `/api/v1/messages/{messageId}`                   | Auth    | Delete message                           |                   |     |
| PUT    | `/api/v1/messages/{messageId}/pin?pinned={true   | false}` | Auth                                     | Pin/unpin message |     |
| GET    | `/api/v1/messages/search`                        | Auth    | Search messages                          |                   |     |
| GET    | `/api/v1/messages/pinned?conversationId={id}`    | Auth    | Get pinned messages                      |                   |     |
| GET    | `/api/v1/messages/unread/summary`                | Auth    | Unread summary                           |                   |     |
| GET    | `/api/v1/messages/unread/conversations`          | Auth    | Conversations with unread messages       |                   |     |
| GET    | `/api/v1/messages/unread/count`                  | Auth    | Total unread count                       |                   |     |
| GET    | `/api/v1/messages/unread/count/{conversationId}` | Auth    | Unread count by conversation             |                   |     |
| POST   | `/api/v1/messages/upload`                        | Auth    | Upload and send file message (multipart) |                   |     |
  
## 6) Friends  
  
| Method | Path                                          | Access | Description                     |     |
| ------ | --------------------------------------------- | ------ | ------------------------------- | --- |
| POST   | `/api/v1/friends/requests`                    | Auth   | Send friend request             |     |
| POST   | `/api/v1/friends/requests/{requestId}/accept` | Auth   | Accept request                  |     |
| POST   | `/api/v1/friends/requests/{requestId}/reject` | Auth   | Reject request                  |     |
| DELETE | `/api/v1/friends/requests/{requestId}`        | Auth   | Cancel request                  |     |
| GET    | `/api/v1/friends/search`                      | Auth   | Search friends                  |     |
| DELETE | `/api/v1/friends/{friendId}`                  | Auth   | Remove friend                   |     |
| GET    | `/api/v1/friends/requests/received`           | Auth   | Received requests               |     |
| GET    | `/api/v1/friends/requests/sent`               | Auth   | Sent requests                   |     |
| GET    | `/api/v1/friends/requests/count`              | Auth   | Pending request count           |     |
| GET    | `/api/v1/friends/{id}`                        | Auth   | Friend profile                  |     |
| GET    | `/api/v1/friends/search-users`                | Auth   | Search users for adding friends |     |
| PUT    | `/api/v1/friends/{friendId}/nickname`         | Auth   | Update friend nickname          |     |
| GET    | `/api/v1/friends/online`                      | Auth   | Online friends                  |     |
  
## 7) Notifications  
  
| Method | Path                                          | Access | Description                |     |
| ------ | --------------------------------------------- | ------ | -------------------------- | --- |
| GET    | `/api/v1/notifications`                       | Auth   | List notifications         |     |
| GET    | `/api/v1/notifications/unread-count`          | Auth   | Unread notifications count |     |
| PUT    | `/api/v1/notifications/{notificationId}/read` | Auth   | Mark one as read           |     |
| PUT    | `/api/v1/notifications/mark-all-read`         | Auth   | Mark all as read           |     |
| DELETE | `/api/v1/notifications/{notificationId}`      | Auth   | Delete notification        |     |
  
## 8) Reports (User)  
  
| Method | Path                 | Access | Description             |     |
| ------ | -------------------- | ------ | ----------------------- | --- |
| POST   | `/api/v1/reports`    | Auth   | Create violation report |     |
| GET    | `/api/v1/reports/my` | Auth   | List my reports         |     |
  
## 9) Admin - Dashboard  
  
| Method | Path                                             | Access | Description             |     |
| ------ | ------------------------------------------------ | ------ | ----------------------- | --- |
| GET    | `/api/v1/admin/dashboard/stats`                  | Admin  | Overview metrics        |     |
| GET    | `/api/v1/admin/dashboard/recent-users`           | Admin  | Recent users            |     |
| GET    | `/api/v1/admin/dashboard/recent-groups`          | Admin  | Recent groups           |     |
| GET    | `/api/v1/admin/dashboard/recent-actions`         | Admin  | Recent admin actions    |     |
| GET    | `/api/v1/admin/dashboard/attendance?year={yyyy}` | Admin  | Monthly attendance      |     |
| POST   | `/api/v1/admin/dashboard/refresh`                | Admin  | Refresh dashboard cache |     |
  
## 10) Admin - Reports  
  
| Method | Path                                 | Access | Description                                        |     |
| ------ | ------------------------------------ | ------ | -------------------------------------------------- | --- |
| GET    | `/api/v1/admin/reports`              | Admin  | List reports (filter by `status`, `violationType`) |     |
| GET    | `/api/v1/admin/reports/{id}`         | Admin  | Report details                                     |     |
| POST   | `/api/v1/admin/reports/{id}/actions` | Admin  | Process report action                              |     |
  
## 11) Admin - Sync  
  
| Method | Path                                      | Access | Description                 |     |
| ------ | ----------------------------------------- | ------ | --------------------------- | --- |
| POST   | `/api/v1/admin/sync/user/{userId}/avatar` | Admin  | Sync user avatar            |     |
| POST   | `/api/v1/admin/sync/user/{userId}`        | Admin  | Sync full cached user info  |     |
| POST   | `/api/v1/admin/sync/recent?hoursAgo={n}`  | Admin  | Sync recently updated users |     |
| POST   | `/api/v1/admin/sync/all`                  | Admin  | Full sync all users         |     |
  
## 12) Files  
  
| Method | Path                            | Access | Description                    |     |
| ------ | ------------------------------- | ------ | ------------------------------ | --- |
| GET    | `/api/v1/files/test-connection` | Auth   | Test object storage connection |     |
| POST   | `/api/v1/files/upload`          | Auth   | Upload file (multipart)        |     |
| DELETE | `/api/v1/files/{fileId}`        | Auth   | Delete file                    |     |
| GET    | `/api/v1/files`                 | Auth   | List all files                 |     |
| GET    | `/api/v1/files/{fileId}`        | Auth   | Get file by id                 |     |
| GET    | `/api/v1/files/folders`         | Auth   | List available folders         |     |
  
## 13) System / Health  
  
| Method | Path                         | Access | Description              |     |
| ------ | ---------------------------- | ------ | ------------------------ | --- |
| GET    | `/api/v1/health`             | Public | General health           |     |
| GET    | `/api/v1/health/ws`          | Public | WebSocket health         |     |
| GET    | `/api/v1/db/test-connection` | Public | Database connection test |     |
  
---  
  
## 14) WebSocket (STOMP)  
  
### Connection  
  
- Endpoint: `/api/v1/ws` (SockJS enabled)  
- Header required on `CONNECT`: `Authorization: Bearer <token>`  
  
### Client -> Server destinations (`/app` prefix)  
  
| STOMP destination  | Purpose            |     |
| ------------------ | ------------------ | --- |
| `/app/chat.send`   | Send message       |     |
| `/app/chat.typing` | Send typing status |     |
| `/app/chat.read`   | Send read receipt  |     |
  
### Server -> Client destinations  
  
| STOMP destination                              | Purpose                              |     |
| ---------------------------------------------- | ------------------------------------ | --- |
| `/topic/conversations/{conversationId}`        | New message events in a conversation |     |
| `/topic/conversations/{conversationId}/typing` | Typing events                        |     |
| `/topic/conversations/{conversationId}/read`   | Read receipt events                  |     |
| `/topic/user-status`                           | User online/offline status           |     |
| `/topic/keep-alive`                            | Keep-alive heartbeat payload         |     |
| `/user/queue/messages`                         | Personal message notifications       |     |
| `/user/queue/ack`                              | ACK for sent message                 |     |
| `/user/queue/errors`                           | Error events                         |     |
| `/user/queue/system`                           | System/welcome messages              |     |
  
---  
  
