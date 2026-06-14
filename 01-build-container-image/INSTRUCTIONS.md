# go2rtc Mac Container Instructions

This guide explains how to build, run, and validate the `go2rtc` Docker image using Apple's native `container` CLI.

## 1. Build the Image
Compile the container image from the provided `Dockerfile`.
```bash
container build -t go2rtc:local .
```

## 2. Validate and Run (Interactive)
Run the container interactively to see the startup logs and ensure it initializes without errors. The `--rm` flag ensures the container is cleaned up when you stop it.
```bash
container run --rm -it \
  -p 1984:1984 \
  -p 8554:8554 \
  -p 8555:8555 \
  -p 8555:8555/udp \
  -v $(pwd):/config \
  go2rtc:local
```

## 3. Verify the Service
While the container is running, open a new terminal window and verify the API is responding:
```bash
curl -I http://127.0.0.1:1984
```
You should receive a `200 OK` response. You can also open your web browser and navigate to [http://127.0.0.1:1984](http://127.0.0.1:1984) to view the go2rtc dashboard.

*(Press `Ctrl+C` in the original terminal to stop the interactive container).*

## 4. Run in Background (Daemon mode)
Once you have validated the setup, you can run it continuously in the background using the `-d` flag:
```bash
container run -d \
  --name go2rtc \
  -p 1984:1984 \
  -p 8554:8554 \
  -p 8555:8555 \
  -p 8555:8555/udp \
  -v $(pwd):/config \
  go2rtc:local
```

### Useful Management Commands:
- **List running containers:** `container ls`
- **View logs:** `container logs go2rtc`
- **View resource usage:** `container stats go2rtc`
- **Stop the container:** `container stop go2rtc`
