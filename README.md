# Le site web !!

Base de données: (à mettre dans un fichier ?)

```SQL

CREATE OR REPLACE TABLE event_types
(
    id   int AUTO_INCREMENT
        PRIMARY KEY,
    name varchar(255) NOT NULL,
    CONSTRAINT event_types_name_uindex
        UNIQUE (name)
);

CREATE OR REPLACE TABLE events
(
    id         int                          NOT NULL
        PRIMARY KEY,
    type_id    int                          NOT NULL,
    game_id    int                          NOT NULL,
    time_fired datetime                     NOT NULL,
    properties longtext COLLATE utf8mb4_bin NOT NULL COMMENT 'JSON',
    CONSTRAINT events_event_types_id_fk
        FOREIGN KEY (type_id) REFERENCES event_types (id)
);

CREATE OR REPLACE TABLE players
(
    id       int                  NOT NULL
        PRIMARY KEY,
    username varchar(255)         NOT NULL,
    password varchar(255)         NOT NULL,
    mail     varchar(255)         NOT NULL,
    enabled  tinyint(1) DEFAULT 1 NOT NULL,
    CONSTRAINT player_username_uindex
        UNIQUE (username)
);

CREATE OR REPLACE TABLE licenses
(
    player_id       int      NOT NULL
        PRIMARY KEY,
    expiration_time datetime NOT NULL,
    granted_time    datetime NOT NULL,
    CONSTRAINT licenses_players_id_fk
        FOREIGN KEY (player_id) REFERENCES players (id)
);

CREATE OR REPLACE TABLE servers
(
    name    varchar(255) NOT NULL
        PRIMARY KEY,
    address varchar(255) NOT NULL,
    port    int          NULL
);

CREATE OR REPLACE TABLE games
(
    id           int          NOT NULL
        PRIMARY KEY,
    player1_id   int          NOT NULL,
    player2_id   int          NOT NULL,
    time_started datetime     NOT NULL,
    winner_id    int          NOT NULL,
    server_name  varchar(255) NOT NULL,
    CONSTRAINT games_players_id_fk_1
        FOREIGN KEY (player1_id) REFERENCES players (id),
    CONSTRAINT games_players_id_fk_2
        FOREIGN KEY (player2_id) REFERENCES players (id),
    CONSTRAINT games_players_id_fk_winner
        FOREIGN KEY (winner_id) REFERENCES players (id),
    CONSTRAINT games_servers_name_fk
        FOREIGN KEY (server_name) REFERENCES servers (name)
);

```