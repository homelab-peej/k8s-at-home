# Self-hosted

### [Actual](https://github.com/actualbudget/actual)
Actual is a local-first personal finance tool. It is 100% free and open-source, written in NodeJS, it has a synchronization element so that all your changes can move between devices without any heavy lifting.

### [Home Assistant](https://github.com/home-assistant/core)
Home Assistant is a home automation toolkit that lets you automate and control your home. Changes to `configuration.yaml` are required if you want to place Home Assistant behind a proxy. When doing the first-time install, disable the mount that maps the configmap to the pod. Let the deployment create the directory and necessary files first, then reconfigure the deployment to use your configmap which can be updated as needed. Reloader will take care of restarting it if you do any further configuration changes. Use `ws://localhost:3000` for the web-socket address in the z-wave integration instead of the detected IP address since the pod IP can change with restarts.

### [Homepage](https://github.com/gethomepage/homepage)
A modern, fully static, fast, secure fully proxied, highly customizable application dashboard with integrations for over 100 services and translations into multiple languages. Easily configured via YAML files or through docker label discovery.

### [Jellyfin](https://github.com/jellyfin/jellyfin/)
Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media. It is an alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps.

### [Mealie](https://github.com/mealie-recipes/mealie/)
Mealie is a self-hosted recipe manager, meal planner, and shopping list application.

### [Tautulli](https://github.com/Tautulli/Tautulli)
Tautulli is a web application for monitoring and providing analytics and notifications for your Plex server.

### [Z-Wave JS UI](https://github.com/zwave-js/zwave-js-ui)
Z-Wave control panel and MQTT gateway. Either can be enabled separately or both together. I've paired this with Home Assistant so I can control z-wave switches and outlets around the home via [this dongle](https://a.co/d/9HZfxjH). By running this in the same pod as Home Assistant, it's still accessible from HA via localhost and keeps the services and ingresses simple.
