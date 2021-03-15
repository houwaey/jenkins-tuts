FROM debian

RUN apt-get update && apt-get install openssh-server --yes

RUN useradd -m -d /home/ssh_user/ -s /bin/bash -G sudo ssh_user && \
    echo "ssh_user:1234" | chpasswd && \
    mkdir /home/ssh_user/.ssh && \
    chmod 700 /home/ssh_user/.ssh

COPY remote-key.pub /home/ssh_user/.ssh/authorized_keys

RUN chown ssh_user:ssh_user -R /home/ssh_user/.ssh/ && \
    chmod 600 /home/ssh_user/.ssh/authorized_keys

RUN mkdir -p /run/sshd && \
    chmod -R 755 /run/sshd

RUN ssh-keygen -A

CMD /usr/sbin/sshd -D
