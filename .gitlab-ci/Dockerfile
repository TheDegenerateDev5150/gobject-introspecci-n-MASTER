FROM fedora:41

RUN dnf -y install \
    autoconf \
    autoconf-archive \
    automake \
    bison \
    cairo-devel \
    cairo-gobject-devel \
    ccache \
    chrpath \
    desktop-file-utils \
    elfutils-libelf-devel \
    flex \
    fontconfig-devel \
    freetype-devel \
    gcc \
    gcc-c++ \
    gettext \
    git \
    glib2-devel \
    glibc-devel \
    glibc-headers \
    gtk-doc \
    itstool \
    libattr-devel \
    libffi-devel \
    libmount-devel \
    libselinux-devel \
    libtool \
    libXfixes-devel \
    libXft-devel \
    libxml2-devel \
    libxslt \
    make \
    mesa-libGL-devel \
    ninja-build \
    openssl-devel \
    pcre-devel \
    python3 \
    python3-devel \
    python3-lxml \
    python3-mako \
    python3-markdown \
    python3-packaging \
    python3-pip \
    python3-setuptools \
    python3-rnc2rng \
    python3-wheel \
    readline-devel \
    redhat-rpm-config \
    sudo \
    sqlite-devel \
    systemtap-sdt-devel \
    zlib-devel \
 && dnf clean all

RUN sed -i -e 's/# %wheel/%wheel/' -e '0,/%wheel/{s/%wheel/# %wheel/}' /etc/sudoers

ARG HOST_USER_ID=5555
ENV HOST_USER_ID ${HOST_USER_ID}
RUN useradd -u $HOST_USER_ID -G wheel -ms /bin/bash user

USER user
WORKDIR /home/user

ENV LANG C.UTF-8
ENV PATH="/usr/bin:/home/user/.local/bin"

RUN pip3 install --user meson==1.4.2

ENV PYENV_ROOT /home/user/.pyenv
ENV PATH="${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}"
ENV PYTHON_CONFIGURE_OPTS="--enable-shared"
RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
RUN pyenv install 3.8.17
