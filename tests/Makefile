all: main


main: main_syntax main_functional main_idempotency main_acceptance

main_syntax:
	# syntax check
	ansible-playbook main.yml -i inventory --syntax-check

main_functional:
	# functional test
	ansible-playbook main.yml -i inventory -e "provision_docker__container_state=reloaded" --skip-tags=acceptance-test

main_idempotency:
	# idempotency test
	ansible-playbook main.yml -i inventory --skip-tags=pre-test,acceptance-test | tee /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_main_centos7.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_main_debian8.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& (echo 'Idempotency test: PASS' && exit 0)\
	|| (echo 'Idempotency test: FAIL' && exit 1)

main_acceptance:
	# acceptance test
	ansible-playbook main.yml -i inventory --tags=initialize-docker,acceptance-test


cleanall: clean_main

clean_main:
	# remove docker containers
	ansible-playbook main.yml -i inventory -e "provision_docker__container_state=absent" --tags=initialize-docker

