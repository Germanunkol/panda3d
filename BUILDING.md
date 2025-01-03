
Build the docker file panda3d_manylinux2014_x86_64_dockerfile.

or build dependencies in new docker:

    docker pull quay.io/pypa/manylinux2014_x86_64
    docker images
    docker run -it -v $(pwd):/io 90ac8ec

    # Dependencies:
    pip install cmake
    Then follow:
    https://github.com/panda3d/buildbot-panda3d/blob/main/dockerfiles/manylinux2014-x86_64

Then inside the docker:

# Compile panda:
git clone git@github.com:Germanunkol/panda3d.git /root/panda3d/source 
mkdir /root/panda3d/build
cd /root/panda3d/build
cmake ../source -DHAVE_BULLET=ON -DHAVE_OPENAL=ON -DHAVE_AUDIO=ON 
make -j8

# Make the wheel:
PY=/opt/python/cp311-cp311/
cd /root/panda3d/source
$PY/bin/python makepanda/makewheel.py --outputdir ../build/
