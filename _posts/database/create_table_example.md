```sql
CREATE TABLE zerot.`User` (
	`user_id`	INT	NOT NULL	PRIMARY KEY auto_increment,
	`nickname`	VARCHAR(20)	NULL,
	`active`	BOOL	NOT NULL	DEFAULT 1,
	`regdate`	DATETIME	NOT NULL,
	`sleepdate`	DATETIME	NULL,
	`withdrawdate`	DATETIME	NULL
);

CREATE TABLE zerot.`Receipts` (
	`receipt_id`	INT	NOT NULL	PRIMARY KEY   auto_increment,
	`date`	DATETIME	NULL,
	`place`	VARCHAR(100)	NULL,
	`address`	VARCHAR(200)	NULL,
	`telephone`	VARCHAR(30)	NULL,
	`register`	INT		NOT NULL,
	`regdate`	DATETIME	NOT NULL,
	`updater`	INT	  NULL,
	`updated`	DATETIME	NULL,
	`board_id`	INT	NOT NULL,
	`country`	VARCHAR(50)	NULL,
	`currency`	VARCHAR(20)	NULL,
	`image`	  VARCHAR(2000)	 NULL,
    FOREIGN KEY (`register`) REFERENCES zerot.User(`user_id`),
    FOREIGN KEY (`updater`) REFERENCES zerot.User(`user_id`),
    FOREIGN KEY (`board_id`) REFERENCES zerot.Boards(`board_id`)
);

CREATE TABLE zerot.`Boards` (
	`board_id`	INT	NOT NULL	PRIMARY KEY	auto_increment,
	`title`	VARCHAR(200)	NOT NULL,
	`startdate`	DATE	NULL,
	`enddate`	DATE	NULL,
	`description`	TEXT	NULL,
	`register`	INT	NOT NULL,
	`regdate`	DATETIME	NOT NULL,
	`updater`	INT	NULL,
	`updated`	DATETIME	NULL,
    FOREIGN KEY (`register`) REFERENCES zerot.User(`user_id`),
    FOREIGN KEY (`updater`) REFERENCES zerot.User(`user_id`)
);

CREATE TABLE zerot.`Rate` (
	`rate_id`	INT	NOT NULL	PRIMARY KEY  auto_increment,
	`date`	DATE	NOT NULL,
	`usa`	FLOAT	NULL,
	`jpa`	FLOAT	NULL,
	`cha`	FLOAT	NULL,
	`way`	VARCHAR(20)	NULL, -- selling or buying
	`register`	INT	NOT NULL,
	`regdate`	DATETIME	NOT NULL,
	`updater`	INT	NOT NULL,
	`updated`	DATETIME	NOT NULL,
    FOREIGN KEY (`register`) REFERENCES zerot.User(`user_id`),
    FOREIGN KEY (`updater`) REFERENCES zerot.User(`user_id`)
);

CREATE TABLE zerot.`Items` (
	`item_id`	INT	NOT NULL	PRIMARY KEY auto_increment,
	`receipt_id`	INT	NOT NULL,
	`origin_name`	VARCHAR(50)	NULL,
	`trans_name`	VARCHAR(50)	NULL,
	`price`	FLOAT	NULL,
	`units`	INT	NULL,
	FOREIGN KEY (`receipt_id`) REFERENCES zerot.Receipts(`receipt_id`)
);

CREATE TABLE zerot.`Board_User` (
	`id`	INT	NOT NULL auto_increment PRIMARY KEY,
	`board_id`	INT	NOT NULL,
	`user_id`	INT	NOT NULL,
    FOREIGN KEY (`board_id`) REFERENCES zerot.Boards(`board_id`),
    FOREIGN KEY (`user_id`) REFERENCES zerot.User(`user_id`)
);
```

