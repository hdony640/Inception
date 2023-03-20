FROM debian:buster

# Executes commands during the image build process
RUN apt-get -y update

RUN apt-get -y install nginx \
    openssl
 
# Copy the new configuration inside my container
COPY nginx.conf /etc/nginx/conf.d/default.conf

# command to generate the Certificate Signing Request
# x509 is for self-signed ssl certificate
RUN openssl req -x509 -nodes \
    -days 365 \
    -subj "/C=BE/ST=Brussels/L=Brussels/O=19, Inc./OU=19/CN=hdony.42.fr" \
    -newkey rsa:2048 \
    -keyout /etc/ssl/hdony.42.fr.key \
    -out /etc/ssl/hdony.42.fr.pem
 
# The EXPOSE instruction informs Docker that the nginx container (the webserver) listens on port 443
# The EXPOSE instruction exposes the specified port and makes it available only for inter-container communication
# EXPOSE 443

WORKDIR /var/www/html/
# For Docker containers, the daemon off; directive tells Nginx to stay in the foreground. 
# The -g option specifies a directive to Nginx.
# The reason we run the process in the foreground is to attach the console process
# to standard input, output, and error.
CMD ["nginx", "-g", "daemon off;"]