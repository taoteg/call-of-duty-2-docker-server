FROM ubuntu:14.04

#Install dependencies
RUN apt-get update
RUN apt-get install -y \
	nodejs \
	nodejs-legacy \
	npm \
	git

# add our private github SSH key
RUN mkdir -p /root/.ssh
ADD id_rsa /root/.ssh/id_rsa
RUN chmod 700 /root/.ssh/id_rsa

# Create known hosts & add github key
RUN touch /root/.ssh/known_hosts
RUN ssh-keyscan github.org >> /root/.ssh/known_hosts

# Clone our GitHub Repository
RUN git clone <YOUR_GITHUB_REPOSITORY_HERE>.git /app

# Install node modules
RUN cd /app; npm install

# expose app port (depending on node application)
EXPOSE 3000

# Start app
WORKDIR /app
ENTRYPOINT ["npm", "start"]