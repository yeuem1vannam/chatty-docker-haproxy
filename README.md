# Chatty behind HAProxy
Original source code from https://github.com/SophieDeBenedetto/action-cable-example
- Websocket
- ActionCable
- Rails 5

> Does websocket work well behind a load balancer?

Let's make a complex & scaleable Chatty using:
- Docker
- HAProxy

![https://i.gyazo.com/316ef2783bb3924d377ea7fdbb382b6a.jpg](https://i.gyazo.com/316ef2783bb3924d377ea7fdbb382b6a.jpg)


## Setup
```sh
git clone https://github.com/yeuem1vannam/chatty-docker-haproxy.git Chatty
cd Chatty/docker
docker-compose build
docker-compose up
# Wait until bundle is done, and puma server start successfully
# web_1          | Puma starting in single mode...
# web_1          | * Version 3.6.2 (ruby 2.3.1-p112), codename: Sleepy Sunday Serenity
# web_1          | * Min threads: 5, max threads: 5
# web_1          | * Environment: development
# web_1          | * Listening on tcp://0.0.0.0:80
# web_1          | Use Ctrl-C to stop

# in another tab of terminal
docker-compose exec web sh -c 'bundle exec rake db:create db:migrate --trace'
```

Now visit [http://localhost](http://localhost) and sign up an account, then create a channel, then join it. In another browser ( maybe Private mode of Chrome ) sign up a new account and join the channel created before. Now, let' chatting

## Scale Chatty
```sh
# cd Chatty/docker
docker-compose scale web=4
# Creating and starting docker_web_2 ... done
# Creating and starting docker_web_3 ... done
# Creating and starting docker_web_4 ... done
```
Then keep chatting, everything should work

*How about scale down?*
```sh
# cd Chatty/docker
docker kill docker_web_1 docker_web_2 docker_web_3
# docker_web_1
# docker_web_2
# docker_web_3
```

Again, keep chatting. Nothing different :D
