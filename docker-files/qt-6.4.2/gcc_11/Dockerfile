# Environment settings
FROM gcc:11
WORKDIR /image
COPY . .

# Installing deps
RUN apt update && apt upgrade -y
RUN apt install -y cmake libclang-13-dev perl unzip git build-essential libfontconfig1-dev libfreetype6-dev libx11-dev libxext-dev libxfixes-dev libxi-dev libxrender-dev libxcb1-dev libx11-xcb-dev libxcb-glx0-dev libxcb-keysyms1-dev libxcb-image0-dev libxcb-shm0-dev libxcb-icccm4-dev libxcb-sync0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-randr0-dev libxcb-render-util0-dev libxcb-xinerama0-dev libxcb-util0-dev libxcb-xinput-dev libxcb-xkb-dev libxkbcommon-x11-dev libwayland-dev libwayland-egl1 libgl-dev libglu-dev libegl1-mesa-dev libgles2-mesa-dev libudev-dev libinput-dev libicu-dev libsqlite3-dev libssl-dev libpng-dev libjpeg-dev libgif-dev libwebp-dev liblzma-dev libzstd-dev libdouble-conversion-dev libpcre2-dev libharfbuzz-dev libxslt1-dev libxml2-dev libbz2-dev libz3-dev ninja-build
# llvm 

# Initialize the repo
RUN git clone git://code.qt.io/qt/qt5.git \
    && cd qt5 \
    && git checkout v6.4.2 \
    && perl init-repository

# Configure qt (no examples, nor tests)
RUN mkdir -p qt6-build \
    && cd qt6-build \
    && ../qt5/configure -prefix . -opensource -confirm-license -nomake examples -nomake tests

# Compile and install (only qtbase and qtscxml)
RUN cd qt6-build \
    && cmake --build . --target qtbase qtscxml --parallel \
    && cmake --install .

# Clear the image from building files
RUN rm -rf qt5 qt6-build

# Export paths
ENV QTDIR="/usr/local/Qt-6.4.2" \
    PATH="/usr/local/Qt-6.4.2/bin:$PATH" \
    CMAKE_PREFIX_PATH="/usr/local/Qt-6.4.2" \
    CMAKE_INCLUDE_PATH="${CMAKE_INCLUDE_PATH}:/usr/local/Qt-6.4.2/qtbase/include:/usr/local/Qt-6.4.2/qtbase/include/QtWidgets:/usr/local/Qt-6.4.2/qtbase/include/QtStateMachine" \
    LD_LIBRARY_PATH="/usr/local/Qt-6.4.2/lib:$LD_LIBRARY_PATH"

# Run program
CMD ["ls", "/usr/local/Qt-6.4.2"]