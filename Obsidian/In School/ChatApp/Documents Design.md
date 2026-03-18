## 1) Base fields dung chung  
  
Da so document ke thua `BaseDocument` va co cac truong chung:  
  
- `id` (`@Id`)  
- `version` (`@Version`) - optimistic locking  
- `isDeleted`  
- `createdAt`, `updatedAt`  
- `createdBy`, `updatedBy`  
- `filter` (ho tro search)  
  
`UserActivityLog` khong ke thua `BaseDocument`.  
  
## 2) Danh sach documents chinh  
  
| Class | Collection | Repository | Muc dich | Truong chinh |  
|---|---|---|---|---|  
| `User` | `users` | `UserRepository` | Luu thong tin tai khoan nguoi dung | `username`, `email`, `password`, `role`, `status`, `lastActiveAt`, `unlockTime`, `blockedUsers`, `favoriteChats` |  
| `Conversation` | `conversations` | `ConversationRepository` | Luu hoi thoai direct/group | `type`, `groupId`, `memberIds`, `lastMessageTimestamp`, `lastMessage` |  
| `Message` | `messages` | `MessageRepository` | Luu tin nhan | `conversationId`, `senderId`, `content`, `rawContent`, `type`, `readByUserIds`, `attachment`, `reactions` |  
| `MemberInfo` | `member_infos` | `MemberInfoRepository` | Trang thai user trong conversation | `userId`, `conversationId`, `lastReadMessageId`, `unreadCount`, `muted`, `pinned`, `archived`, `favorite` |  
| `Group` | `groups` | `GroupRepository` | Metadata nhom chat | `name`, `adminId`, `avatarUrl`, `description`, `inviteLink`, `isPublic` |  
| `Files` | `files` | `FilesRepository` | Luu metadata file dinh kem | `fileUrl`, `thumbnailUrl`, `fileName`, `fileType`, `fileSize`, `mimeType`, `conversationId` |  
| `Notification` | `notifications` | `NotificationRepository` | Thong bao cho user | `recipientId`, `senderId`, `type`, `title`, `content`, `isSeen`, `relatedId` |  
| `Report` | `reports` | `ReportRepository` | Bao cao vi pham | `reporterId`, `targetUserId`, `violationType`, `status`, `adminNote`, `resolvedBy`, `resolvedAt` |  
| `AdminLog` | `admin_logs` | `AdminLogRepository` | Audit hanh dong admin | `adminId`, `actionType`, `targetUserId`, `reportId`, `reason`, `metadata` |  
| `Friends` | `friends` | `FriendsRepository` | Quan he ban be da chap nhan | `userId`, `friendId`, `friendDisplayName`, `friendAvatarUrl`, `becameFriendsAt`, `isFavorite` |  
| `PendingFriends` | `pending_friends` | `PendingFriendsRepository` | Loi moi ket ban dang cho | `senderId`, `receiverId`, `status`, `message`, `processedAt`, `expiresAt` |  
| `UserActivityLog` | `user_activity_logs` | `UserActivityLogRepository` | Log lich su user active | `id`, `userId`, `activityDate`, `activityType`, `metadata` |  
  
## 3) Model nhung (embedded)  
  
Cac class duoi day duoc dung nhu embedded sub-document (khong co repository rieng):  
  
- `LastMessageInfo`: preview tin nhan cuoi trong `Conversation.lastMessage`  
- `FavoriteChat`: danh sach chat yeu thich trong `User.favoriteChats`  
- `MessageReaction`: reaction trong `Message.reactions`  
- `BlockedUser`: dang duoc khai bao `@Document` nhung hien tai chu yeu nam trong `User.blockedUsers` va khong co repository rieng  
  
## 4) Indexes dang khai bao trong model  
  
### `User`  
- Trong model: chua thay `@Indexed` field-level.  
- Trong `MongoDbInitializer`: `username` unique, `email` unique, `status + lastActiveAt`, `fullName` (vi collation), `status + unlockTime`.  
  
### `Conversation`  
- Compound: `lastMessageTimestamp`, `memberIds + lastMessageTimestamp`, `type + memberIds`.  
- Field: `groupId` indexed.  
  
### `Message`  
- Compound: `conversationId + createdAt`, `senderId + conversationId + createdAt`, `conversationId + rawContent(text)`, `repliedToMessageId`.  
- Field: `conversationId`, `senderId` indexed.  
  
### `MemberInfo`  
- Unique compound: `userId + conversationId`.  
- Compound: `userId + updatedAt`, `userId + unreadCount`.  
- Field: `userId`, `conversationId` indexed.  
  
### `Group`  
- Field: `name`, `adminId` indexed.  
  
### `Notification`  
- Compound: `recipientId + createdAt`, `recipientId + isSeen`.  
- Field: `recipientId`, `type` indexed.  
  
### `Report`  
- Compound: `status + createdAt`, `targetUserId + status`, `reporterId + createdAt`, `reporterId + targetUserId + status`.  
- Field: `reporterId`, `targetUserId`, `violationType` indexed.  
  
### `AdminLog`  
- Compound: `targetUserId + createdAt`, `adminId + createdAt`.  
- Field: `adminId`, `actionType`, `targetUserId` indexed.  
  
### `Friends`  
- Unique compound: `userId + friendId`.  
- Compound: `userId + createdAt`.  
- Field: `userId`, `friendId` indexed.  
  
### `PendingFriends`  
- Unique compound: `senderId + receiverId`.  
- Compound: `receiverId + status + createdAt`, `senderId + status + createdAt`.  
- Field: `senderId`, `receiverId`, `status` indexed.  
- Trong `MongoDbInitializer` co them TTL index cho `expiresAt`.  
  
### `UserActivityLog`  
- Compound: `userId + activityDate`.  
- Field: `userId`, `activityDate` indexed.  
- Trong `MongoDbInitializer` co them index `activityDate`.  
  
## 5) Mapping nhanh quan he  
  
- `User` 1-n `Conversation` qua `Conversation.memberIds`  
- `Conversation` 1-n `Message` qua `Message.conversationId`  
- `Conversation` 1-n `MemberInfo` (moi user trong 1 conversation co 1 record)  
- `User` 1-n `Notification` qua `Notification.recipientId`  
- `User` 1-n `Report` (reporter), va cung la target cua report (`targetUserId`)  
- `User` 1-n `AdminLog` (target), `Admin` 1-n `AdminLog` (adminId)  
- `User` n-n `Friends` (luu thanh 2 ban ghi theo tung chieu tuy theo service)  
  
## 6) Ghi chu hien trang  
  
- `MongoDbInitializer` dang goi `initUserIndexes`, `initFriendsIndexes`, `initPendingFriendsIndexes`, `initNotificationIndexes`, `initReportIndexes`, `initAdminLogIndexes`, `createUserActivityLogsIndexes`.  
- Cac ham `initConversationIndexes`, `initMessageIndexes`, `initGroupIndexes` dang bi comment trong `initIndexes()`.  
- Vi vay, index thuc te con phu thuoc vao: annotation-level index creation + initializer dang bat.