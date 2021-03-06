FROM ubuntu:16.04  
LABEL maintainer="Martin Thomson <martin.thomson@gmail.com>"  
  
RUN apt-get update && apt-get install -y --no-install-recommends \  
ca-certificates coreutils curl git make mercurial ssh \  
python-minimal python-lxml python-pip python-setuptools python-wheel \  
mmark ruby \  
build-essential gyp ninja-build pkg-config zlib1g-dev \  
&& apt-get autoremove -y && apt-get clean -y \  
&& rm -rf /var/lib/apt/lists/*  
  
ENV USER idci  
ENV LOGNAME $USER  
ENV HOSTNAME $USER  
ENV HOME /home/$USER  
ENV SHELL /bin/bash  
  
RUN useradd -d "$HOME" -s "$SHELL" -m "$USER"  
WORKDIR $HOME  
USER $USER  
ENV BINDIR $HOME/bin  
RUN mkdir -p $BINDIR  
ENV PATH $BINDIR:/usr/local/bin:/usr/bin:/bin  
  
RUN set -e; tool_install() { \  
tool="$1";version="$2";sha="$3"; tmp=$(mktemp -t "${tool}XXXXX.tgz"); \  
curl -sSLf "https://tools.ietf.org/tools/${tool}/${tool}-${version}".tgz -o
"$tmp"; \  
[ $(sha256sum -b "$tmp" | cut -d ' ' -f 1 -) = "$sha" ]; \  
target="${BINDIR:-~/.local/bin}/${tool}"; \  
tar xzfO "$tmp" "${tool}-${version}/${tool}" >"$target"; rm -f "$tmp"; \  
chmod 755 "$target"; }; \  
tool_install idnits 2.15.00 \  
f655d06e7d3b1c35d7ca55f91243115359ae4fdd17553ea58a301091a07ed7ac && \  
tool_install rfcdiff 1.45 \  
82e449b7ee887074302b2050e41fc60d4b3bbec8c20e05ce2d7fab81b332771e  
  
RUN pip install --user --compile xml2rfc && \  
ln -s $HOME/.local/bin/xml2rfc $BINDIR  
RUN gem install --no-doc --user-install --bindir $BINDIR \  
certified kramdown-rfc2629 && \  
certified-update  
  
ENV KRAMDOWN_REFCACHEDIR=$HOME/.cache/xml2rfc  
RUN mkdir -p $KRAMDOWN_REFCACHEDIR  
  
RUN git clone \--mirror https://github.com/martinthomson/i-d-template
$HOME/i-d-template  
  
ENV NSS_BUNDLE $HOME/nss.bundle  
RUN hg clone https://hg.mozilla.org/projects/nss /tmp/nss \  
&& hg -R /tmp/nss bundle -a $NSS_BUNDLE \  
&& rm -rf /tmp/nss  
  
ENV NSPR_BUNDLE $HOME/nspr.bundle  
RUN hg clone https://hg.mozilla.org/projects/nspr /tmp/nspr \  
&& hg -R /tmp/nspr bundle -a $NSPR_BUNDLE \  
&& rm -rf /tmp/nspr  

