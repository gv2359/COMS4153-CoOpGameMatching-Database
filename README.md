# COMS4153-CoOpGameMatching-Database
Database layer for Co-Op Game Matching web application.

The database instance contains four different databases: UserProfile, Notfication, Game, and MatchRequest.

For User profile there are two tables, below are the data structure:
```
CREATE TABLE if not exists user_info (
    userId CHAR(36) PRIMARY KEY DEFAULT (UUID()),
    password VARCHAR(255),
    email VARCHAR(255) NOT NULL UNIQUE,
    accessToken VARCHAR(1024) NULL,
    displayName VARCHAR(100),
    steamID VARCHAR(100)
);

CREATE TABLE if not exists user_favored_games (
    userId CHAR(36),
    gameId CHAR(36),
    matchRequestId CHAR(36),
    PRIMARY KEY (userId, gameId),
    FOREIGN KEY (userId) REFERENCES user_info(userId)
);
```

For Game:

```
CREATE TABLE if not exists game_info (
    gameId CHAR(36) PRIMARY KEY DEFAULT (UUID()),
    image BLOB,
    title VARCHAR(255),
    description TEXT
);
```

For MatchRequest:
```
CREATE TABLE match_request (
    userId CHAR(36),
    gameId CHAR(36),
    matchRequestId CHAR(36) PRIMARY KEY DEFAULT (UUID()),
    expireDate DATE,
    isActive BOOL,
    isCancelled BOOL
);
```

For Notification:
```
CREATE TABLE expired_notification (
    userId CHAR(36),
    gameId CHAR(36),
    user_email VARCHAR(255) NOT NULL UNIQUE,
    notificationId INT AUTO_INCREMENT PRIMARY KEY,
    content TEXT,
    timestamp Date
);

CREATE TABLE match_notification (
    userId1 CHAR(36),
    userId2 CHAR(36),
    gameId CHAR(36),
    user1_email VARCHAR(255) NOT NULL UNIQUE,
    user2_email VARCHAR(255) NOT NULL UNIQUE,
    notificationId INT AUTO_INCREMENT PRIMARY KEY,
    content TEXT,
    timestamp Date
);
```
