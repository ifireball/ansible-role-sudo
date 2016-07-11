all: 01 02 03


01:
	$(MAKE) -C 01_basic

02:
	$(MAKE) -C 02_purge_unmanaged_specs

03:
	$(MAKE) -C 03_rename_unmanaged_specs

clean:
	$(MAKE) -C 01_basic clean
	$(MAKE) -C 02_purge_unmanaged_specs clean
	$(MAKE) -C 03_rename_unmanaged_specs clean
