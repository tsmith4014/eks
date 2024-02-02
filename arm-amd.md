# arm-amd

If anyone is using an M1/M2 chip you might have some issues when building your images locally and pushing to your Docker-hub and then trying to pull those images into an Ubuntu server --> From what I have found its differences in architecture and you will get an odd error and the "crashloopbackoff" :
"ubuntu@ip-10-0-3-74:~$ kubectl logs dojo-app-598dcfb467-5vklhexec /docker-entrypoint.sh: exec format error".
So I was able to build the images the following way and it makes them multi-architectured and the application to works now.
docker buildx create --name mymultiarchbuilder --use
docker buildx inspect --bootstrap
docker buildx build --platform linux/amd64,linux/arm64 -t tsmith4014/dojo-app:latest --push . --build-arg PORT_BACKEND=80
