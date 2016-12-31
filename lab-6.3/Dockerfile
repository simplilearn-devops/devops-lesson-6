FROM alpine:latest
RUN apk update
RUN apk add openssh git
RUN adduser -g "Git User" -D git
RUN mkdir /home/git/.ssh
ADD authorized_keys /home/git/.ssh
RUN mkdir /home/git/project.git && \
    cd /home/git/project.git && \
    echo "Initial readme" > readme.txt && \
    git init --bare && \
    git config user.email "git@gitrepo.org" && \
    git config user.name "Git"
RUN chown -R git.git /home/git && \
    chmod 600 /home/git/.ssh/authorized_keys
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -q -N ""
VOLUME /home/git
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

