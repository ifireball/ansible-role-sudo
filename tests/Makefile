all: main purge_unmanaged_specs rename_unmanaged_specs


main: main_syntax main_functional main_idempotency main_acceptance

main_syntax:
	ansible-playbook t1_main.yml -i inventory --syntax-check

main_functional:
	ansible-playbook t1_main.yml -i inventory -e "provision_docker__container_state=reloaded" --skip-tags=acceptance-test

main_idempotency:
	ansible-playbook t1_main.yml -i inventory --skip-tags=pre-test,acceptance-test | tee /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t1_centos7.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t1_debian8.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& (echo 'Idempotency test: PASS' && exit 0)\
	|| (echo 'Idempotency test: FAIL' && exit 1)

main_acceptance:
	ansible-playbook t1_main.yml -i inventory --tags=initialize-docker,acceptance-test
	

purge_unmanaged_specs: purge_unmanaged_specs_syntax purge_unmanaged_specs_functional purge_unmanaged_specs_idempotency purge_unmanaged_specs_acceptance

purge_unmanaged_specs_syntax:
	ansible-playbook t2_purge_unmanaged_specs.yml -i inventory --syntax-check

purge_unmanaged_specs_functional:
	ansible-playbook t2_purge_unmanaged_specs.yml -i inventory -e "provision_docker__container_state=reloaded" --skip-tags=acceptance-test

purge_unmanaged_specs_idempotency:
	ansible-playbook t2_purge_unmanaged_specs.yml -i inventory --skip-tags=pre-test,acceptance-test | tee /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t2_centos7.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t2_debian8.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& (echo 'Idempotency test: PASS' && exit 0)\
	|| (echo 'Idempotency test: FAIL' && exit 1)

purge_unmanaged_specs_acceptance:
	ansible-playbook t2_purge_unmanaged_specs.yml -i inventory --tags=initialize-docker,acceptance-test

	
rename_unmanaged_specs: rename_unmanaged_specs_syntax rename_unmanaged_specs_functional rename_unmanaged_specs_idempotency rename_unmanaged_specs_acceptance

rename_unmanaged_specs_syntax:
	ansible-playbook t3_rename_unmanaged_specs.yml -i inventory --syntax-check

rename_unmanaged_specs_functional:
	ansible-playbook t3_rename_unmanaged_specs.yml -i inventory -e "provision_docker__container_state=reloaded" --skip-tags=acceptance-test

rename_unmanaged_specs_idempotency:
	ansible-playbook t3_rename_unmanaged_specs.yml -i inventory --skip-tags=pre-test,acceptance-test | tee /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t3_centos7.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& grep -E 'test_sudo_t3_debian8.*changed=0.*unreachable=0.*failed=0' /tmp/ansible_idempotency_test.txt\
	&& (echo 'Idempotency test: PASS' && exit 0)\
	|| (echo 'Idempotency test: FAIL' && exit 1)

rename_unmanaged_specs_acceptance:
	ansible-playbook t3_rename_unmanaged_specs.yml -i inventory --tags=initialize-docker,acceptance-test


cleanall: clean_main clean_purge_unmanaged_specs clean_rename_unmanaged_specs

clean_main:
	ansible-playbook t1_main.yml -i inventory -e "provision_docker__container_state=absent" --tags=initialize-docker
	
clean_purge_unmanaged_specs:
	ansible-playbook t2_purge_unmanaged_specs.yml -i inventory -e "provision_docker__container_state=absent" --tags=initialize-docker
	
clean_rename_unmanaged_specs:
	ansible-playbook t2_rename_unmanaged_specs.yml -i inventory -e "provision_docker__container_state=absent" --tags=initialize-docker

