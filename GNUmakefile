

.PHONY: all
all: help

.PHONY: help
help:
	@echo "Usage: make [ TARGET ... ]";
	@echo "";
	@echo "TARGET:";
	@echo "";
	@echo "  help      - show this help message";
	@echo "  rpm       - package as RPM file (in builder)";
	@echo "  deb       - package as DEB file (in builder)";
	@echo "  run       - install and run the package (in runner)";
	@echo "  stop      - stop builder/runner instances";
	@echo "  clean     - delete all generated files";
	@echo "  distclean - delete all generated files and caches";
	@echo "";
	@echo "Default TARGET is 'help'.";


.PHONY: clean
clean: stop
	[ -e rpm.make ] && $(MAKE) -f rpm.make rpm-clean;

.PHONY: distclean
distclean: clean
	rm -f rpm.make;

.PHONY: rpm
rpm: roles rpm.make
	vagrant up --no-provision
	vagrant provision --provision-with builder;
	vagrant ssh -c 'make -C /vagrant couchdb.rpm;';

.PHONY: run
run: roles
	vagrant up --no-provision
	vagrant provision --provision-with runner;

.PHONY: stop
stop:
	vagrant destroy --force;

.PHONY: couchdb.rpm
couchdb.rpm: export RPM_DISTS_DIR := files
couchdb.rpm: export RPM_NAME      := couchdb
couchdb.rpm: export RPM_VERSION   := 1.6.1
couchdb.rpm: export RPM_PACKER    :=
couchdb.rpm: export RPM_SOURCE0   := apache-couchdb-1.6.1.tar.gz
couchdb.rpm: export RPM_SOURCE1   := couchdb.init.in
couchdb.rpm: rpm.make
	mkdir -p $(RPM_DISTS_DIR);
	$(MAKE) -f rpm.make rpm-pack;

.PHONY: roles
roles: roles/jeffhung.couchdb/tasks/main.yml \
       roles/jeffhung.localrepo/tasks/main.yml

roles/jeffhung.couchdb/tasks/main.yml:
	ansible-galaxy install --roles-path=roles jeffhung.couchdb

roles/jeffhung.localrepo/tasks/main.yml:
	ansible-galaxy install --roles-path=roles jeffhung.localrepo

rpm.make:
	curl -L -o rpm.make https://bit.ly/rpm-make;

