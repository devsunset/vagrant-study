
-------------------------------------------------

			# VAGRANT-WORK #

-------------------------------------------------

########################################################
### Vagrant

https://www.vagrantup.com/

https://developer.hashicorp.com/vagrant/intro
https://developer.hashicorp.com/vagrant/docs
https://developer.hashicorp.com/vagrant/tutorials/getting-started

    공식 box 사이트: https://app.vagrantup.com/boxes/search
    유저 box 사이트: http://www.vagrantbox.es/

https://www.virtualbox.org/

########################################################
### Reference

https://developer.hashicorp.com/vagrant/intro
https://developer.hashicorp.com/vagrant/docs
https://developer.hashicorp.com/vagrant/tutorials/getting-started

https://www.44bits.io/ko/post/vagrant-tutorial
https://judo0179.tistory.com/120
https://nearhome.tistory.com/92

########################################################
### Vagrant Guide

Vagrant의 사전적인 의미는 “부랑자”/“정처없는 사람”을 뜻한다

베이그런트(Vagrant)는 포터블 가상화 소프트웨어 개발 환경
(예: 개발 생산성 증가를 위해 가상화의 소프트웨어 구성 관리의 단순화를 시도하는 
버추얼박스, 하이퍼-V, 도커 컨테이너, VM웨어, AWS)의 생성 및 유지보수를 위한 
오픈 소스 소프트웨어 제품의 하나이다. 
베이그런트는 루비 언어로 작성되어 있지만 생태계는 몇 가지 언어로 개발을 지원한다.  - 위키백과

Vagrant는 운영체제 시스템에 대하여 쉬운 Provisioning 제공
가상머신을 생성하고 관리할 때 사용
가상머신을 사용자의 요구에 맞게 Host name, IP, Service Install 등 다양한 환경을 미리 설정하고
사용자가 원할 시 해당 시스템을 즉시 사용할 수 있도록 해주는 Provisioning 도구

Vagrant가 지원하는 가상화 기술
	VirtualBox
	VMware
	KVM
	Linux Container (LXC)
	Docker


# Vagrant Install
공식 문서 참고 설치 
https://developer.hashicorp.com/vagrant/downloads

Ubuntu Linux
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant

# 설치 버전 확인 
vagrant --version

# Box List 확인 
vagrant box list

# box 추가 삭제 
	-공식 box 추가
	vagrant box add centos/7

	-유저 box 추가
	vagrant box add centos66  https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.0.0/centos-6.6-x86_64.box

	우분투 Box 추가 
	vagrant box add bento/ubuntu-16.04	

	우분투 Box 삭제 
	vagrant box remove bento/ubuntu-16.04

# 가상 머신 설정 생성
	# mkdir create your project folder
	mkdir workdir
	cd workdir
	
	# 명령을 통해 Vagrantfile을 생성(별다른 명령 없이 실행하면 기본 값으로 파일 생성)
	vagrant init
		-Vagrantfile 파일 생성 됨 
		# -*- mode: ruby -*-
		# vi: set ft=ruby :

		Vagrant.configure("2") do |config|
		  config.vm.box = "base"
		end

		# config.vm.box = "base" 설정이 어떠한 이미지를 선택할지 정하는 것으로 이부분을 수정하면
		# Vagrant Cloud에서 만들어진 이미지를 다운로드 해서 실행

    # 초기화와 동시에 지정할 수 있는 방법
	vagrant init bento/ubuntu-16.04

		-Vagrantfile 파일 생성 됨 
		# -*- mode: ruby -*-
		# vi: set ft=ruby :

		Vagrant.configure("2") do |config|
		  config.vm.box = "bento/ubuntu-16.04"
		end


# 가상 머신 생성
vagrant up

# 생성된 가상 머신 접근
vagrant ssh

# 상태 확인
vagrant status

	Vagrant는 Vagrantfile가 존재하는 디렉터리에 의존적
	vagrant up 명령을 수행한 이후에는 가상 머신과 관련된 정보를 vagrant 디렉터리에 저장
	SSH 접속에 관한 인증 정보도 같이 포함되어 있기 때문에 이를 삭제하게 되면 Vagrant가 정상적으로 동작 안함

# 가상 머신 중지
vagrant halt

# 가상 머신 삭제
vagrant destroy  


### Vagrant 기본 명령어 ###
vagrant --version : 설치 버전 확인 
vagrant box list : Box list 확인 
vagrant box add : Box 추가 
vagrant box remove : Box 삭제 
vagrant init : 프로비저닝 하기 위한 초기 파일(Vagrantfile)을 생성
vagrant up : Vagrantfile을 바탕으로 프로비저닝을 진행
vagrant halt :가상머신을 종료
vagrant destroy : 가상머신을 삭제
vagrant reload : vagrant destory + vagrant up 같이 동작 
vagrant ssh : 가상머신에 ssh로 접속
vagrant status : 가상머신 동작상태를 확인
vagrant provision : 가상머신의 설정을 변경하고 적용
vagrant package :가상 머신을 박스 파일로 내보내기
vagrant suspend: 현재 프로젝트의 가상 머신을 중지
vagrant resume: 현재 프로젝트의 중지된 가상 머신을 재개
vagrant global-status: 베이그런트에서 실행된 모든 가상 머신들의 상태


########################################################
### Vagrantfile

--------------------------------------------------------
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
--------------------------------------------------------

# Vagrant.configure("2")의 경우 Vagrant 설정 형식 버전 2를 사용한다는 의미
하위 버전과 호환을 위해 사용하지만 메이저 버전은 버전 2를 사용하는 것이 일반적
현재 지원하는 버전은 "1" 과 "2" 두 가지 
버전 "1"은 Vagrant 1.0.x 구성을 나타내고, "2"는 2.0.x 까지 이어지는 1.1+ 의 구성을 나타냄
단일 구성 섹션 내에서 단일 버전만 사용할 수 있음 


# do...end 안에 Vagrant를 통해 설정할 정보를 입력(모든 설정 정보는 do...end 블록 안에 작성)

# 특정 Box버젼 사용 하려면 아래와 같이 설정 
	Vagrant.configure("2") do |config|
	  config.vm.box = "ubuntu/bionic64"
	  config.vm.box_version = "20210119.1.0"
	end

# VM 성능에 관련된 설정을 변경
	Vagrant.configure("2") do |config|
	  config.vm.box = "ubuntu/bionic64"
	  config.vm.box_version = "20210119.1.0"

	  config.vm.provider "virtualbox" do |machine|
	    machine.memory = 4096
	    machine.cpus = 4
	  end
	end


# Vagrant로 멀티 VM 생성

 프런트엔드 - 벡엔드 - 데이터베이스 - 파일서버 4개의 VM을 동시에 올리는 예제

    프런트엔드 : Ubuntu 18.04 LTS
        CPU : v1 Core
        RAM : 1GB
    벡엔드 : Ubuntu 20.04 LTS
        CPU : v2 Core
        RAM: 2GB
    데이터베이스 : Fedora 33
        CPU: v4 Core
        RAM : 4GB
    파일서버 : Centos 8
        CPU: v2 Core
        RAM : 2GB

--------------------------------------------------------
Vagrant.configure("2") do |config|

  config.vm.define "frontend" do |frontend|
    frontend.vm.box = "ubuntu/bionic64"
    frontend.vm.host_name = "front"
    frontend.vm.provider :virtualbox do |spec|
      spec.cpus = 1
      spec.memory = 1024
  end
end

  config.vm.define "backend" do |backend|
    backend.vm.box = "ubuntu/focal64"
    backend.vm.host_name = "api"
    backend.vm.provider :virtualbox do |spec|
      spec.cpus = 2
      spec.memory = 2048
  end
end

  config.vm.define "db" do |db|
    db.vm.box = "generic/fedora33"
    db.vm.host_name = "db"
    db.vm.provider :virtualbox do |spec|
      spec.cpus = 4
      spec.memory = 4096
  end
end

  config.vm.define "file" do |file|
    file.vm.box = "generic/centos8"
    file.vm.host_name = "file"
    file.vm.provider :virtualbox do |spec| 
      spec.cpus = 2
      spec.memory = 2048
  end
end
end
--------------------------------------------------------

$ vagrant up
# 각각의 VM에 접속
$ vagrant ssh frontend
$ vagrant ssh backend
$ vagrant ssh db
$ vagrant ssh file 


# 특정 VM에 사양을 조정하고 전체 VM에는 일괄적으로 성능을 정해야 한다면 다음과 같이 작성

--------------------------------------------------------
Vagrant.configure("2") do |config|

  config.vm.define "master_server" do |master|
    master.vm.box = "ubuntu/focal64"
    master.vm.host_name = "master"
    master.vm.provider :virtualbox do |spec|
      spec.cpus = 4
      spec.memory = 4096
    end
  end


  config.vm.define "slave_server" do |slave|
    slave.vm.box = "ubuntu/focal64"
    slave.vm.host_name = "slave"
  end

  # 따로 cpu 갯수와 memory를 적지 않았다면, 기본으로 설정될 값
  config.vm.provider "virtualbox" do |spec|
       spec.cpus = 2
       spec.memory = 1024
  end
end
--------------------------------------------------------

# 네트워크 설정 

--------------------------------------------------------
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 # kube-master VM
 config.vm.define "kube-master" do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kube-master"
    vb.cpus = 1
    vb.memory = 1000
  end
  config.vm.hostname = "kube-master"
  config.vm.network "private_network", ip: "192.168.0.100"
 end

# kube-worker1 VM
 config.vm.define "kube-worker1" do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kube-worker1"
    vb.cpus = 1
    vb.memory = 1000
  end
  config.vm.hostname = "kube-worker1"
  config.vm.network "private_network", ip: "192.168.0.101"
 end

# kube-worker2 VM
 config.vm.define "kube-worker2" do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kube-worker2"
    vb.cpus = 1
    vb.memory =1000
  end
  config.vm.hostname = "kube-worker2"
  config.vm.network "private_network", ip: "192.168.0.102"
 end

# Hostmanager Plugin
config.hostmanager.enabled = true
config.hostmanager.manage_guest = true

# Provision
 config.vm.provision "shell", inline: <<-SHELL
  sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config
  sed -i 's/archive.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
  sed -i 's/security.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
  systemctl restart ssh
  apt update
  apt install -y chrony
 SHELL
end
--------------------------------------------------------

# https://developer.hashicorp.com/vagrant/docs/vagrantfile/machine_settings
config.vm.box(문자열) - 가상머신에 가져올 상자를구성.여기의 값은 설치된 상자의 이름이거나 
						HashiCorp의 Vagrant Cloud에있는 상자의 축약형 이름
config.vm.provider - 프로비저닝에 사용할 하이퍼바이저 제공자를 선택
config.vm.network -기기에 네트워크를 구성

# 네트워크 관련된 설정으로 호스트와 가상 머신 사이에 포트 포워딩을 할 수 있습니다.
  가상 머신의 80 포트를 호스트의 8080 포트에 연결하려면 다음 설정을 추가
  config.vm.network "forwarded_port", guest: 80, host: 8080

# 127.0.0.1로 IP를 강제하면, 호스트에 포트 포워딩이 되더라도 호스트 머신 밖에서는 가상 머신에 접근하는 것이 불가능
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

# private_network를 사용해 호스트에서만 접근 가능한 아이피 값을 추가적으로 지정하는 것도 가능
config.vm.network "private_network", ip: "192.168.33.10"

# public_network를 지정하면 브릿지를 통해 마치 내부 망의 물리머신에 있는 머신처럼 사용
config.vm.network "public_network", :bridge => 'en0'

# vagrant-hostmanager 는 게스트머신에서 호스트파일을 관리하는 플러그인
1.5.0 버전부터 vagrant up 으로 프로비저닝이 발생하기 전에 hostmanager를 실행하기 때문에 사전에 설치
up 명령으로 작성한 Vagrantfile 을 바탕으로 프로비저닝을 진행

$ vagrant plugin install vagrant-hostmanager
$ vagrant up


########################################################
### Etc

# Minimum Vagrant Version
버전 호환성 이슈를 최소화 하기 위해서 vagrant 최소 요구 버전을 맨 위에 명시
Vagrant.require_version ">= 1.3.5"
Vagrant.require_version ">= 1.3.5", "< 1.4.0"

# Loop Over VM Definitions
여러 같은 종류의 머신의 경우 반복문으로 설정

	(1..3).each do |i|
	  config.vm.define "node-#{i}" do |node|
	    node.vm.provision "shell",
	      inline: "echo hello from node #{i}"
	  end
	end

	# THIS DOES NOT WORK!
	for i in 1..3 do
	  config.vm.define "node-#{i}" do |node|
	    node.vm.provision "shell",
	      inline: "echo hello from node #{i}"
	  end
	end

# Vagrant는  기본적으로 프로젝트 디렉터리를 가상 머신의 /vagrant에 마운트시켜줍니다
이를 기반으로 게스트에서 개발 서버를 실행하고, 호스트 상에서 IDE나 텍스트 에디터로 
코드를 편집하면서 개발을 하는 것이 가능

synced_folder 옵션을 통해서 추가적인 디렉터리를 마운트
첫 번째 인자는 호스트의 디렉터리를 의미하고, 두 번째 인자는 가상 머신 상의 디렉터리를 의미
config.vm.synced_folder "../data", "/vagrant_data"


# 개발 환경 구축을 위한 프로비저너
프로바이더Provider와 프로비저너Provisioner
- 프로바이더는 가상 머신 기능을 제공하는 소프트웨어를 의미 (virtualbox)
- 프로비저너는 가상 머신의 개발 환경을 셋업해주는 역할 (vagrant  다양한 프로비저닝 툴을 지원)

우분투에 도커 설치 
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provision "shell", inline: "wget -qO- https://get.docker.com/ | sh"
  config.vm.provision "shell", inline: "usermod -aG docker vagrant"
end

shell 프로비저너를 사용해서 inline으로 명령어 지정 (셸 스크립트는 멱등성을 보장해주지 않음)
이 프로비저닝 내용은 맨 처음 vagrant up을 실행할 때만 동작
따라서 이미 베이그런트로 가상 머신이 실행되어있는 경우 vagrant provision 명령어를 명시적으로 실행하거나,
vagarnt reload --provision과 같이 reload에 --provision 옵션을 명시적으로 붙여주어야 함 


# 가상 머신을 다시 박스로 만들어주는 package
가상 머신을 박스 파일로 내보내기하려면 package 서브 커맨드를 사용
vagrant package

package.box라는 이름으로 새로운 베이그런트 박스 파일이 생성
* 이 박스가 자동으로 로컬 환경에 설치되지는 않습니다. 
이 박스를 사용하려면 vagrant add 명령어로 박스를 등록해주어야합니다.

vagrant box add ubuntu/bionic64/docker ./package.box

* --output 옵션을 사용해 내보내는 파일의 이름을 지정 가능 