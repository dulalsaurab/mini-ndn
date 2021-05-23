# Mini-NDN in [VirtualBox](https://www.virtualbox.org/) using [vagrant](https://www.vagrantup.com/).

We have a Mini-NDN pre-installed in a vagrant box. The box can be found [here](https://app.vagrantup.com/ashiq/boxes/minindn). For suggested Mini-NDN resource allocation, Here's an example [`Vagrantfile`](https://github.com/dulalsaurab/mini-ndn-11th-ndn-hackathon/tree/master/container/Vagrantfile):
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "ashiq/minindn"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4192"
    vb.cpus = "4"
    vb.name = "mini-ndn_box"
  end
end
```

### Building from scratch with `vagrant` and VirtualBox containing Mini-NDN

* Start by downloading and installing Vagrant and VirtualBox
  * https://www.vagrantup.com/downloads
  * https://www.virtualbox.org/wiki/Downloads

* To create and start fresh virtual machine:
  * Create a file called "Vagrantfile" with this basic setup:
    ```ruby
    # -*- mode: ruby -*-
    # vi: set ft=ruby :
    Vagrant.configure("1") do |config|
      config.vm.box = "bento/ubuntu-21.04"
      config.vm.provider "virtualbox" do |vb|
        vb.memory = 4095
        vb.cpus = 3
        vb.name = "mini-ndn_box"
      end
    end
    ```
  * Open your terminal or command line in the directory that has Vagrantfile
  * Start the virtual machine with,
    `$ vagrant up`
  * The username/password for the vm are both `vagrant`.

* To install mini-ndn, use the commands:
    ```bash
    git clone https://github.com/named-data/mini-ndn.git
    cd mini-ndn
    git pull https://github.com/dulalsaurab/mini-ndn-11th-ndn-hackathon.git
    ./install.sh -a
    ```
    * The install script may ask for input. At those times, press ENTER to select the default values. In the future, the `git pull` command will not be needed, as the improvements from the hackathon will be applied directly to the [`named-data/mini-ndn`](https://github.com/named-data/mini-ndn) repo.
* To test mini-ndn:
    * while still in the `mini-ndn` directory, enter
      ```bash
      sudo python3 examples/ndnedit.py
      sudo python3 examples/nlsr/pingall.py
      ```
    * If it worked, it should be in the mini-ndn command line once finished for both commands. Enter `exit` to close the CLI.
* To clean and export vm as Vagrant Box:
    * while in vm, enter these to clean:
      ```bash
      cd
      sudo apt-get clean
      sudo dd if=/dev/zero of=/EMPTY bs=1M
      sudo rm -f /EMPTY
      cat /dev/null > ~/.bash_history && history -c && exit
      ```
    * Close the vm window and open a terminal in the same directory as the `Vagrantfile`.
    * In the terminal, type this command where `vb_name` is the name of the vm defined in `Vagrantfile`, and `box_name` any name for the output `.box` file
      ```bash
      vagrant package --base vb_name --output box_name.box
      ```

### Notes:
* [WIP] There might be error showing up regarding `infoedit` which can be resolved by running `./install -a` (once or twice). We're working on a fix.