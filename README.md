> ⚠️ **WARNING:** This project has been archived \
> Due to xiaomi login restriction
> ![Screenshot](99-reference/Screenshot%202026-06-14%20at%2013.37.44.png)

# Introduction

This repo tries to capture camera stream from 'xiaomi camera 3 3k'.

![小米智能摄像机3 3K版示意图](99-reference/607551387-6f65c711-a63b-489b-b5b4-1a68f62342d2.png)




# Running the Project

To start the containers defined in the `docker-compose.yaml` file, run:

```bash
# Run in the background (detached mode)
docker compose up -d
```

To view logs if running in detached mode:
```bash
docker compose logs -f
```

To stop and remove the containers:
```bash
docker compose down
```

# Reference

1. [AlexxIT/go2rtc](https://github.com/AlexxIT/go2rtc)