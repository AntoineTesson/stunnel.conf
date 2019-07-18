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


Save the file and start stunnel :

/etc/init.d/stunnel4 start

For running stunnel automated edit properties in /etc/default/stunnel4:

ENABLED=1

Conf file :

#Certificate

 cert = /opt/psa/var/modules/letsencrypt/etc/live/kergafa.com/cert.pem
 key = /opt/psa/var/modules/letsencrypt/etc/live/kergafa.com/privkey.pem

# Remove TCP delay for local and remote.

socket = l:TCP_NODELAY=1
socket = r:TCP_NODELAY=1
chroot = /var/run/stunnel4/
pid = /stunnel.pid

# Only use this options if for making it more secure after you get it to work.
# User id
# setuid = nobody
# Group id
# setgid = nobody

# IMPORTANT: If the websocketserver is on the same server as the webserver use this: local = my.domainname.com
# Insert here your domain that is secured with https.
local = kergafa.com

[websockets]

accept = 8080
connect = kergafa.com:8081

# IMPORTANT: If you use the local variable above, you have to add the domainname here aswell. connect = my.domainname.com:8888
# ALSO *: When starting your websocket server, you have to use the -a parameter to specify the domainname



