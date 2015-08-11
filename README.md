Regular workflow
-----------
Ensure that you have the following programs installed globally:

   * git
   * vagrant

To get up and running:

    $ vagrant up

Șmecher workflow
-------------------------

In order to avoid reinstallation of packages and time consuming downloads for every `vagrant destroy && vagrant up`, you can run the following command when initially configuring your environment:

    $ BASIC_ONLY=true vagrant up

This will only install packages and do some basic configs and then stop the provisioning. When it's done you can run:

    $ vagrant package --base CUSTOM_vm --output custom_vm.box
    $ vagrant box add custom_base_box ./custom_vm.box && rm ./custom_vm.box

Now when you do `vagrant destroy && vagrant up`, only the configuration done in the second part of the provisioning will be destroyed. The first part of the configuration will be preserved in the box and the first part of the provisioning won't be necessary, saving you some valuable time.
