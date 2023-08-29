# Use the NVIDIA CUDA base image
FROM nvidia/cuda:11.0.3-cudnn8-devel-ubuntu16.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt-get update && apt-get install -y \
    git \
    zsh \
    wget \
    sudo \
    libgl1-mesa-dev \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Create a new user named "vscode"
RUN useradd -m -s /bin/zsh vscode && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Switch to the new user
USER vscode
WORKDIR /home/vscode

# Install Anaconda
RUN wget https://repo.anaconda.com/archive/Anaconda3-2023.07-2-Linux-x86_64.sh && \
    bash Anaconda3-2023.07-2-Linux-x86_64.sh -b -p $HOME/anaconda3 && \
    rm Anaconda3-2023.07-2-Linux-x86_64.sh && \
    echo "export PATH=$HOME/anaconda3/bin:$PATH" >> $HOME/.zshrc

# Install powerlevel10k
RUN git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $HOME/powerlevel10k && \
    echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >> $HOME/.zshrc

# Set default shell to zsh
SHELL ["/bin/zsh", "-l"]

# Install VSCode Server
# RUN curl -fsSL https://code-server.dev/install.sh | sh
# 
# # Expose the port used by VSCode Server
# EXPOSE 8080
# 
# # Start VSCode Server
# ENTRYPOINT [ "code-server" ]
