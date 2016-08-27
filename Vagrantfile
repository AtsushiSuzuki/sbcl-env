Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell", inline: <<-SCRIPT
    apt-get update
    apt-get upgrade -y

    curl -sSL -O http://prdownloads.sourceforge.net/sbcl/sbcl-1.3.8-x86-64-linux-binary.tar.bz2
    tar xf sbcl-1.3.8-x86-64-linux-binary.tar.bz2
    pushd sbcl-1.3.8-x86-64-linux; ./install.sh; popd
  SCRIPT
  config.vm.provision "shell", privileged: false, inline: <<-SCRIPT
    curl -sSL -O https://beta.quicklisp.org/quicklisp.lisp
    sbcl --load quicklisp.lisp --eval "(progn (quicklisp-quickstart:install) (exit))"
    echo "(load \"~/quicklisp/setup.lisp\")" > ~/.sbclrc
  SCRIPT
end
