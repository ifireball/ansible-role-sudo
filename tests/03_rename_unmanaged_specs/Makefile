all: syntax functional idempotency acceptance

syntax:
	ansible-playbook test.yml -i inventory --syntax-check

functional:
	ansible-playbook test.yml -i inventory -e "provision_docker__container_state=reloaded" --skip-tags=acceptance-test

idempotency:
	ansible-playbook test.yml -i inventory --skip-tags=pre-test,acceptance-test | tee /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_03_centos7.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_03_debian8.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& (echo 'Idempotency test: PASS' && exit 0)\
	|| (echo 'Idempotency test: FAIL' && exit 1)

acceptance:
	ansible-playbook test.yml -i inventory --tags=initialize-docker,acceptance-test

clean:
	ansible-playbook test.yml -i inventory -e "provision_docker__container_state=absent" --tags=initialize-docker

