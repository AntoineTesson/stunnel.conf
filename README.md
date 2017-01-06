# stunnel.conf

Launch php app/console gos:websocket:server -a kergafa.com

The config of config.yml

# Web Socket Configuration
gos_web_socket:
    server:
        port: 8081        #The port the socket server will listen on
        host: 127.0.0.1  #The host ip to bind to
        router:
            resources:
                - '@SkiesAdherentBundle/Resources/config/pubsub/routing.yml'
    client:
        firewall: main
        session_handler: '@session.handler.pdo'
    pushers:
        wamp:
            host: 127.0.0.1
            port: 8081
