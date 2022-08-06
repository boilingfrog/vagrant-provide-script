## vagrant 使用 vmware 构建 centos  

### 如何使用

#### 下载

除了要下载 vmware ，还需要安装 Vagrant VMware 插件  

```
vagrant plugin install vagrant-vmware-desktop
```

安装 `vmware Utility`   

具体参见[vagrant-vmware-utility](https://www.vagrantup.com/docs/providers/vmware/vagrant-vmware-utility)  

#### 启动

这里的 Vagrantfile 已经写好了，直接在 Vagrantfile 当前目录，导入对应的 box，启动即可     

下载 box   

```
wget https://app.vagrantup.com/centos/boxes/7/versions/1905.1/providers/vmware_desktop.box 
```

导入 box    

```
vagrant box add centos-vm-7.2 CentOS-7-x86_64-Vagrant-1905_01.VMwareFusion.box
```  

启动   

```
vagrant up
```  


网络设置  

> Starting with the Big Sur release VMware Fusion is no longer able to create network devices with custom subnet and mask settings to attach to guests. This means custom IP addresses are not valid when creating a private network. When creating a private network device to attach to a guest, simply define it with no options:

从Big Sur发布开始，就不支持自定义私有网络了，只需要设置 `node_config.vm.network :private_network` 即可。  