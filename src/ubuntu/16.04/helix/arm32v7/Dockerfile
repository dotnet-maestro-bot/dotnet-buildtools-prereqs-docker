FROM arm32v7/ubuntu:16.04

# Install Helix Dependencies 

# Can remove the mono preview repo when we no longer depend on pre-release libgdiplus

RUN apt-get update && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    apt-get install -y apt-transport-https ca-certificates && \
    echo "deb https://download.mono-project.com/repo/ubuntu preview-xenial main" | tee /etc/apt/sources.list.d/mono-official-preview.list  && \
    apt-get update && \
    apt-get install -y \
        gss-ntlmssp \
        iputils-ping \
        libcurl3 \
        libffi-dev \
        libgdiplus \
        libicu-dev \
        libssl-dev \
        libunwind8 \
        libunwind-dev \
        lldb-3.9 \
        locales \
        locales-all \
        python3-dev \ 
        python3-pip \
        sudo \
        tzdata \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.utf8

RUN ln -sf /usr/bin/python3 /usr/bin/python && \
    python -m pip install --upgrade pip==19.2.2 && \
    python -m pip install \
                  applicationinsights==0.11.7 \
                  certifi==2018.11.29 \
                  cryptography==2.5 \
                  docker==3.6.0 \
                  ndg-httpsclient==0.5.1  \
                  psutil==5.4.8 \
                  pyasn1==0.4.5 \
                  pyopenssl==18.0.0 \
                  requests==2.21.0 \
                  six==1.12.0 \
                  virtualenv==16.2.0 \
                  azure-devops==5.0.0b9 \
                  future==0.17.1

RUN adduser --disabled-password --gecos '' --uid 1001 --shell /bin/bash --ingroup adm helixbot && \
    chmod -R +x /root && \
    echo 'helixbot ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER helixbot

RUN python -m virtualenv --no-site-packages /home/helixbot/.vsts-env


