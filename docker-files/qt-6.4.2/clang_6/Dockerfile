# Environment settings
FROM silkeh/clang:6
WORKDIR /image
COPY . .

# Install deps and Qt
RUN apt update && apt install -y \
    cmake libclang-13-dev perl unzip git build-essential libfontconfig1-dev libfreetype6-dev libx11-dev libxext-dev libxfixes-dev libxi-dev libxrender-dev libxcb1-dev libx11-xcb-dev libxcb-glx0-dev libxcb-keysyms1-dev libxcb-image0-dev libxcb-shm0-dev libxcb-icccm4-dev libxcb-sync0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-randr0-dev libxcb-render-util0-dev libxcb-xinerama0-dev  libxcb-util0-dev libxcb-xinput-dev libxcb-xkb-dev libxkbcommon-x11-dev libwayland-dev libwayland-egl1 libgl-dev libglu-dev libegl1-mesa-dev libgles2-mesa-dev libudev-dev libinput-dev libicu-dev libsqlite3-dev libssl-dev libpng-dev libjpeg-dev libgif-dev libwebp-dev liblzma-dev libzstd-dev libdouble-conversion-dev libpcre2-dev libharfbuzz-dev libxslt1-dev libxml2-dev libbz2-dev libz3-dev ninja-build \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* \
    && git clone git://code.qt.io/qt/qt5.git \
    && cd qt5 \
    && git checkout v6.4.2 \
    && perl init-repository \
    && cd .. \
    && mkdir -p qt6-build \
    && cd qt6-build \
    && ../qt5/configure -prefix /usr/local/Qt-6.4.2 -opensource -confirm-license -nomake examples -nomake tests \
    && cmake --build . --parallel \
    && cmake --install . \
    && cd .. \
    && rm -rf qt5 qt6-build \
    && apt-get purge -y --auto-remove build-essential git ninja-build

# Export paths
ENV CMAKE_PREFIX_PATH="/usr/local/Qt-6.4.2"
ENV LD_LIBRARY_PATH="/usr/local/Qt-6.4.2/lib:$LD_LIBRARY_PATH"

# Run program
CMD ["ls", "/usr/local/Qt-6.4.2/include/QtCore"]