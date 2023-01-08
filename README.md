# Home Server

this repo is Infrastructure as Code for my home server

everything is in a docker container and can be started with docker compose 

## Setup

### 1. install [docker](https://docs.docker.com/get-docker/)

### 2. set environment variable (you can save everything in a `.env` file)

- `SERVICE_DIR` your content **NOTE** the layout has to be like shown below
- `PHOTOPRISM_ADMIN_USER` 
- `PHOTOPRISM_ADMIN_PASSWORD`
- `NEXTCLOUD_ADMIN_USER` 
- `NEXTCLOUD_ADMIN_PASSWORD`
- `DB_PHOTOPRISM_PASSWORD` 
- `DB_PHOTOPRISM_ROOT_PASSWORD`
- `DB_NEXTCLOUD_PASSWORD`
- `DB_NEXTCLOUD_ROOT_PASSWORD`

### 3. SERVICE_DIR

set the `SERVICE_DIR` environment variable to the `root` of **your** folder structure 

```
root
├── gitlab
│   ├── config
│   ├── logs
│   └── data
├── jellyfin
│   ├── config
│   ├── Movies
│   ├── Shows
│   ├── Music
│   └── Books
├── photoprism
│   ├── originals
│   ├── storage
│   └── db
└── nextcloud
    ├── data
    └── db
```

### 4. run `docker-compose up -d`

get gitlab password with `docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password`

the username is `root`

- photoprism: `http://localhost:2342/`
- nextcloud: `http://localhost:8080/`
- gitlab: `http://localhost:8929/` (gitlab could take a while to start)
- jellyfin: `http://localhost:8096/`

## layout

1. put all your photos into `photoprism/originals`

2. `jellyfin` media layout 

```
jellyfin
├── Movies
│   ├── Film (1990).mp4
│   ├── Film (1994).mp4
│   ├── Film (2008)
│   │   └── Film.mkv
│   └── Film (2010)
│       ├── Film-cd1.avi
│       └── Film-cd2.avi
├── Shows
│   ├── Series (2010)
│   │   ├── Season 00
│   │   │   ├── Some Special.mkv
│   │   │   ├── Episode S00E01.mkv
│   │   │   └── Episode S00E02.mkv
│   │   ├── Season 01
│   │   │   ├── Episode S01E01-E02.mkv
│   │   │   ├── Episode S01E03.mkv
│   │   │   └── Episode S01E04.mkv
│   │   └── Season 02
│   │       ├── Episode S02E01.mkv
│   │       └── Episode S02E02.mkv
│   └── Series (2018)
│       ├── Episode S01E01.mkv
│       ├── Episode S01E02.mkv
│       ├── Episode S02E01-E02.mkv
│       └── Episode S02E03.mkv
├── Music
│   ├── Artist
│   │   ├── Album 1
│   │   │   ├── Disc 1
│   │   │   │   ├── 01 - Song.mp3
│   │   │   │   └── 02 - Song.mp3
│   │   │   └── Disc 2
│   │   │       ├── 01 - Song.mp3
│   │   │       └── 02 - Song.mp3
│   │   ├── Album 2
│   │   │   ├── 01 - Song.flac
│   │   │   └── 02 - Song.flac
│   │   └── 08 - Song.ogg
│   └── 09 - Song.ogg
└── Books
    ├── Audiobooks
    │   ├── Author
    │   │   ├── Book1.flac
    │   │   └── Book2.flac
    │   └── Book
    │       ├── Chapter1.flac
    │       └── Chapter2.flac
    └── Books
        └── Author
            ├── Book1.epub
            ├── Book2.epub
            ├── Book
            │   ├── Book1.epub
            │   ├── cover.ext
            │   └── metadata.opf
            └── Book3.mp3
```