
-------------------------------------------------

			# VAGRANT-WORK #

-------------------------------------------------

########################################################
### Vagrant

https://www.vagrantup.com/

https://developer.hashicorp.com/vagrant/intro
https://developer.hashicorp.com/vagrant/tutorials/getting-started

    공식 box 사이트: https://app.vagrantup.com/boxes/search
    유저 box 사이트: http://www.vagrantbox.es/

https://www.virtualbox.org/

########################################################
### Reference

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

# Vagrant Install
공식 문서 참고 설치 
https://developer.hashicorp.com/vagrant/downloads

Ubuntu Linux
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant


# Vagrant 기본 명령어
vagrant init : 프로비저닝 하기 위한 초기 파일(Vagrantfile)을 생성
vagrant up : Vagrantfile을 바탕으로 프로비저닝을 진행
vagrant halt :가상머신을 종료
vagrant destroy : 가상머신을 삭제
vagrant ssh : 가상머신에 ssh로 접속
vagrant status : 가상머신 동작상태를 확인
vagrant provision : 가상머신의 설정을 변경하고 적용

