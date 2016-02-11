# acng-container-util

An interactive utility to use apt-cacher-ng ("acng" in short) docker container [minimum2scp/apt-cacher-ng:latest](https://hub.docker.com/r/minimum2scp/apt-cacher-ng/).

## Requirements

 * ruby
 * bundler
 * docker
 * docker-compose
 * peco

## Installation

### Checkout the code

```shell
git clone https://github.com/minimum2scp/acng-container-util.git /path/to/acng-container-util
```

### bundle install

```
cd /path/to/acng-container-util
mkdir -p vendor/bundle
bundle install --path vendor/bundle
```

### Configure shell

Add the initialization code to your zshrc

```shell
export PATH=/path/to/acng-container-util/bin:$PATH
eval "$(acng init)"
```

or

```shell
export PATH=/path/to/acng-container-util/bin:$PATH
acng_precmd_hook (){
  if [ -f /tmp/apt-cacher-ng.${USER}/http_proxy.sh ]; then
    . /tmp/apt-cacher-ng.${USER}/http_proxy.sh
  fi
}
autoload -Uz add-zsh-hook
add-zsh-hook precmd acng_precmd_hook
```

## Usage

```
% bin/acng
Commands:
  acng help [COMMAND]  # Describe available commands or one specific command
  acng init            # define acng shell function for bashrc, zshrc
  acng log             # view apt-cacher-ng container logs
  acng set             # set environment variable http_proxy (to eval)
  acng start           # start apt-cacher-ng container
  acng status          # status apt-cacher-ng container
  acng stop            # stop apt-cacher-ng container
  acng unset           # unset environment variable http_proxy (to eval)

```

### Use apt-cacher-ng with apt-get

```
% acng start
% acng set
% sudo http_proxy=${http_proxy} apt-get update
% sudo http_proxy=${http_proxy} apt-get dist-upgrade
```

### Use apt-cacher-ng with docker build

```
% acng start
% acng set
% cd /path/to/your-docker-image
% docker build --build-arg http_proxy=${http_proxy} .
```

