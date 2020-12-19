<h1 align="">ELK stack 👋</h1>
<p>
</p>

> My ELK stack on CentOS 7 using Ansible + Vagrant

![Ansible](/.github/assets/img/elastic-stack.png)

<div align=>
	<img align="right" width="200px" src=/.github/assets/img/ansible-new-logo.png>
</div> 

## Table of Contents

* **ELK**
  * [Offical Website](https://www.elastic.co)
  * [Offical Docs](https://www.elastic.co/guide/index.html)
  * [Official Github](https://github.com/elastic)
* **Ansible**
  * [Official Website](https://www.ansible.com)
  * [Official Docs](https://docs.ansible.com)
  * [Official Github](https://github.com/ansible/ansible)
  * [installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

## Requirements 
* Vagrant 2.2.6;
* Ansible 2.10.3

## Usage

```
vagrant up
```

```
ansible-playbook -i hosts main.yml --tags "java"
ansible-playbook -i hosts main.yml --tags "elasticsearch"
ansible-playbook -i hosts main.yml --tags "kibana"
ansible-playbook -i hosts main.yml --tags "logstash"
```

Voilá! 

## Author

👤 **Tadeu Bernacchi**

* Website: http://www.tadeubernacchi.com.br/
* Twitter: [@tadeuuuuu](https://twitter.com/tadeuuuuu)
* Github: [@tbernacchi](https://github.com/tbernacchi)
* LinkedIn: [@tadeubernacchi](https://linkedin.com/in/tadeubernacchi)

## Show your support

Give a ⭐️ if this project helped you!

***
_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
